---
title: "Google AI Process"
date: 2022-04-26T19:02:08+02:00
draft: false
weight: 20
pre: "<b>B. </b>"
---

### The Google AI Task

The first thing that happens when a picture is submitted is that we execute a "Submit to Google AI" external task. This task takes the provided picture, submits it to Google's Vision AI API, and returns the evaluated results to the model.

To do this, we will submit the picture to Google's Vision AI API. This is why we all enabled that API in our Google Console back in Exercise 1!

If you're not interested in how this whole process works, you can simply build and start the [exercise-6.go](exercise-6.go) task worker as is with the following command in your terminal:

```shell
$ go mod init exercise-6
$ go mod tidy
$ go build
$ ./exercise-6
```

Much of the Golang code in this Task Worker will look vary familiar from previous exercises. We start a Task Worker using our Camunda Platform 8 credentials, which listens for tasks with the ID `DoPictureAI`. When it finds one, it gets the process variable `imageLoc`, downloads the picture at that location, and submits it to the Google Vision AI for processing.

```go
jobKey := job.GetKey()
	_, err := job.GetCustomHeadersAsMap()
	if err != nil {
		// failed to handle job as we require the custom job headers
		failJob(client, job)
		return
	}
	jobVars := JobVars{}
	err = job.GetVariablesAs(&jobVars)
	if err != nil {
		failJob(client, job)
		return
	}
	dPrintf("%+v\n", jobVars)
	if jobVars.ImageLoc == "" {
		failJob(client, job)
		return
	}
	// Get the image from the storage
	resp, err := http.Get(jobVars.ImageLoc)
	if err != nil {
		failJob(client, job)
		return
	}
	defer resp.Body.Close()
  emote := doAIOnPic(&resp.Body)
  ```

That last bit is where the actual work takes place, so let's look a little more closely at that.

```go
  client, err := vision.NewImageAnnotatorClient(ctx, options)
	if err != nil {
		log.Fatalf("Failed to create client: %v", err)
	}
	defer client.Close()
	im, err := vision.NewImageFromReader(io.Reader(*image))
	if err != nil {
		log.Fatalf("Failed to create image: %v", err)
	}
	emotions := Emotions{}
  annotations, err := client.DetectFaces(ctx, im, nil, 10)
	if err != nil {
		fmt.Println("No faces found.")
		emotions.IsPicture = false
		log.Fatalf("Failed to detect faces: %v", err)
	}
```

We first create a Google Vision API `client` which we will use to submit the image, once we have that, we will create the new image from the URL we got as part of the process variables. This actually saves us some memory because we don't download the image, and then submit it but rather send a reference to the `Reader` object directly to the Google Vision API `NewImageFromReader` method. We also create a `emotions` variable to store the results of the Google Vision API.

When we submit the image to Google, we will get back an `annotations` object from Google. We are not interested in everything in this object, so I created an `interestingAnnotations` JSON object that has the parameters we will use to dispense candy:

```go
type interestingAnnotations struct {
	DetectionConfidence    float64 `json:"detection_confidence"`
	LandmarkingConfidence  float64 `json:"landmarking_confidence"`
	JoyLikelihood          int     `json:"joy_likelihood"`
	SorrowLikelihood       int     `json:"sorrow_likelihood"`
	AngerLikelihood        int     `json:"anger_likelihood"`
	SurpriseLikelihood     int     `json:"surprise_likelihood"`
	UnderExposedLikelihood int     `json:"under_exposed_likelihood"`
	BlurredLikelihood      int     `json:"blurred_likelihood"`
	HeadwearLikelihood     int     `json:"headwear_likelihood"`
}
```

We can then go through the larger `annotations` object and gather the things we want:

```go
  for i, annotation := range annotations {
		goodStuff := interestingAnnotations{}
		data, err := json.Marshal(annotation)
		if err != nil {
			log.Fatal(err)
		}
		err = json.Unmarshal(data, &goodStuff)
		if err != nil {
			log.Fatal(err)
		}
		dPrintln("  Face", i)
		emotions.Anger = annotation.AngerLikelihood.String()
		emotions.AngerNumber = goodStuff.AngerLikelihood
		dPrintln("    Anger:", annotation.AngerLikelihood)
		emotions.Joy = annotation.JoyLikelihood.String()
		emotions.JoyNumber = goodStuff.JoyLikelihood
		dPrintln("    Joy:", annotation.JoyLikelihood)
		emotions.Surprise = annotation.SurpriseLikelihood.String()
		emotions.SurpriseNumber = goodStuff.SurpriseLikelihood
		dPrintln("    Surprise:", annotation.SurpriseLikelihood)
		emotions.Sorrow = annotation.SorrowLikelihood.String()
		emotions.SorrowNumber = goodStuff.SorrowLikelihood
		dPrintln("    Sorrow:", annotation.SorrowLikelihood)
	}
```

We will then return this `emotions` object, from which we will submit the task variables:

```go
  variables := make(map[string]interface{})
	variables["isPicture"] = emote.IsPicture
	variables["Joy"] = emote.Joy
	variables["JoyNumber"] = emote.JoyNumber
	variables["Anger"] = emote.Anger
	variables["AngerNumber"] = emote.AngerNumber
	variables["Surprise"] = emote.Surprise
	variables["SurpriseNumber"] = emote.SurpriseNumber
	variables["Sorrow"] = emote.Sorrow
	variables["SorrowNumber"] = emote.SorrowNumber
	dPrintf("%+v\n", variables)
	request, err := client.NewCompleteJobCommand().JobKey(jobKey).VariablesFromMap(variables)
	if err != nil {
		failJob(client, job)
		return
	}
	dPrintln("Complete job", jobKey, "of type", job.Type)
	ctx := context.Background()
	_, err = request.Send(ctx)
	if err != nil {
		panic(err)
	}
```

I'm returning the `String` values, but when we look at the DMN table you will see that they are unused. We could use them in the process if we wanted to, but for this exercise we will just use the `Number` values.
