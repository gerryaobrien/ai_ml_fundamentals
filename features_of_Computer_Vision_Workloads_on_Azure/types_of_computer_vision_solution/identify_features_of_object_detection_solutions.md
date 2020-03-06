# Identify Features of Object Detection Solutions

Object detection is the process where distinct items, or objects, are detected in an image.  As an example, consider this image of a person sitting in front of a computer in what appears to be a kitchen setting.  How many distinct objects can you identify in this image?

![person sitting in front of a laptop, small kitchen appliances in the background](images/object_detect.png)

For the average person, you might easily identify the following objects:

- mobile phone
- computer/laptop
- mug/coffee cup
- pen
- cooking pot
- cutting board
- toaster
- canisters of some type

In a manner similar to the face detection algorithms discussed in the topic on facial recognition, the object detection API will return a JSON response with rectangle (bounding box) coordinates for the detected objects.  The API can also place tags in the response, based on teh objects, including living things, that are identified in the image.  An example of the JSON that is returned from the Detect API is shown here.  You will note that not every object is listed and, perhaps the tags are not precisely what you might have used.

```json

{
   "objects":[
      {
         "rectangle":{
            "x":730,
            "y":66,
            "w":135,
            "h":85
         },
         "object":"kitchen appliance",
         "confidence":0.501
      },
      {
         "rectangle":{
            "x":523,
            "y":377,
            "w":185,
            "h":46
         },
         "object":"computer keyboard",
         "confidence":0.51
      },
      {
         "rectangle":{
            "x":471,
            "y":218,
            "w":289,
            "h":226
         },
         "object":"Laptop",
         "confidence":0.85,
         "parent":{
            "object":"computer",
            "confidence":0.851
         }
      },
      {
         "rectangle":{
            "x":654,
            "y":0,
            "w":584,
            "h":473
         },
         "object":"person",
         "confidence":0.855
      }
   ],
   "requestId":"a7fde8fd-cc18-4f5f-99d3-897dcd07b308",
   "metadata":{
      "width":1260,
      "height":473,
      "format":"Jpeg"
   }
}
```

Notice that the API has detected a person, a "kitchen appliance", a laptop, and a keyboard.  The kitchen appliance and computer keyboard only have roughly a 50% confidence.  The Detect API is 85% certain there is a laptop and a person in the image.  

It's also important to be aware of some limitations on the Detect API to ensure that you are setting your expectations accordingly, when using the service.  Here are some the most common areas to be aware of:

- objects that are less than 5% of the image, based on size, will not likely be detected
- objects that are very close together, a stack of plates for example, may not be detected
- specific brand information or product names do not differentiate objects in the image.  There is a Brand detection feature however, that can be used to extract brand information from the objects.  This is not discussed here.

Object detection is actually a feature and is part of the Analyze Image API within Azure Computer Vision.  Essentially, you are calling the analyze image API and telling it you want Objects, as the visualFeatures parameter.  You will form the REST API request in the form of a URL having the following format:

https://{endpoint}/vision/v2.0/analyze?visualFeatures=Objects&language=en

You replace the {endpoint} portion with the URL endpoint for your Cognitive Services account. 

You also need to supply the service with an image through one of the supported methods:

- upload an image directly to the service, with your API call
- specify a URL where the image is located.   This must be publicly accessible or the service won't be able to read the image.

    >[!NOTE:]The Object visual feature is optional and if you do not provide this feature in the request URL, the default response will be to return image categories.   Be sure you use the visualFeatures=Object parameter in your request.
