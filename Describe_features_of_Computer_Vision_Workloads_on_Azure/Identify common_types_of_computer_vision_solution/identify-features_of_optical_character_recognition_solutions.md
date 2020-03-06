# Identify Features of Optical Character Recognition Solutions

Optical Character Recognition (OCR), is the concept of recognizing text in images.  After successfully evaluating an image that contains text, the service will return the recognized characters, in the image, as a machine-readable character stream.  Your application can then parse and read that character stream.

## The OCR API

The service can be consumed as a REST API service and therefore, you provide specific information in a request URL, then collect the results in a response object.  The service requires you to specify the following information:

- endpoint URL - this is the URL endpoint for your Cognitive Service
- orientation - you need to use the detectOrientation parameter even if you set it to false.  When set to true, it tells the service to detect the orientation of the text in the image and correct the orientation if necessary.  This might be required if an image was scanned upside down and then saved in that orientation
- language - an optional parameter indicating the language in the image.  If you don't know, or the image may contain multiple languages, don't include this parameter and the service will default to 'unk', unknown.

The request body must containan image stream that holds the binary information for the image.  When the service is called, the code in your application should look for a status code or error.  If the status code is 200, the request was successful and a character stream should be returned within JSON formated response.  Creating supporting classes in your code will allow you to deserialize the JSON easily, and then extract the underlying text.   An example of a result is shown here:

```json

{
  "language": "en",
  "textAngle": -2.0000000000000338,
  "orientation": "Up",
  "regions": [
    {
      "boundingBox": "462,379,497,258",
      "lines": [
        {
          "boundingBox": "462,379,497,74",
          "words": [
            {
              "boundingBox": "462,379,41,73",
              "text": "A"
            },
            {
              "boundingBox": "523,379,153,73",
              "text": "GOAL"
            },
            {
              "boundingBox": "694,379,265,74",
              "text": "WITHOUT"
            }
          ]
        },
        {
          "boundingBox": "565,471,289,74",
          "words": [
            {
              "boundingBox": "565,471,41,73",
              "text": "A"
            },
            {
              "boundingBox": "626,471,150,73",
              "text": "PLAN"
            },
            {
              "boundingBox": "801,472,53,73",
              "text": "IS"
            }
          ]
        },
        {
          "boundingBox": "519,563,375,74",
          "words": [
            {
              "boundingBox": "519,563,149,74",
              "text": "JUST"
            },
            {
              "boundingBox": "683,564,41,72",
              "text": "A"
            },
            {
              "boundingBox": "741,564,153,73",
              "text": "WISH"
            }
          ]
        }
      ]
    }
  ]
}

```

The OCR API does have some requirements and limitations that you need to be aware of.

- image format - JPEG, PNG, GIF, and BMP formats are supported
- image size - must be between 50 x 50 and 4200 x 4200 pixels
- rotation angle - the text in the image can be rotated 0, 90, 180, 270 degrees and small angles up to 40 degrees
- dominant text - if text is quite dominant in the image, false positives may occur from partially recognized words

## The Read API

As you have read in the OCR section, that method can have issues with false positives when the image is considered text-dominate.  The Read API uses the latest recognition models and is optimized for images that have lots of text or have a lot of visual noise.  It is a better option for scanned document that have lots of text.  The Read API also has the ability to automatically determine the proper recognition model to use, taking into consideration lines of text and supporting images with printed text as well as recognizing handwriting.

Because the Read API cna with larger documents, it works asynchronously so as not to block your application while it is reading the content and returning results to your applicaiton.  It can also maintain word groups in the same lines as the image.  Each line will be indicated by bounding box coordinates and each word in the line will have its own coordinates as well.  An example of an output from the Read API is shown here for reference, in JSON format:

```json

{
  "status": "succeeded",
  "createdDateTime": "2019-10-03T14:32:04.236Z",
  "lastUpdatedDateTime": "2019-10-03T14:38:14.852Z",
  "analyzeResult": {
    "version": "v3.0",
    "readResults": [
      {
        "page": 1,
        "language": "en",
        "angle": 49.59,
        "width": 600,
        "height": 400,
        "unit": "pixel",
        "lines": [
          {
            "boundingBox": [
              202,
              618,
              2047,
              643,
              2046,
              840,
              200,
              813
            ],
            "text": "Our greatest glory is not",
            "words": [
              {
                "boundingBox": [
                  204,
                  627,
                  481,
                  628,
                  481,
                  830,
                  204,
                  829
                ],
                "text": "Our",
                "confidence": 0.164
              },
              {
                "boundingBox": [
                  519,
                  628,
                  1057,
                  630,
                  1057,
                  832,
                  518,
                  830
                ],
                "text": "greatest",
                "confidence": 0.164
              },
              {
                "boundingBox": [
                  1114,
                  630,
                  1549,
                  631,
                  1548,
                  833,
                  1114,
                  832
                ],
                "text": "glory",
                "confidence": 0.164
              },
              {
                "boundingBox": [
                  1586,
                  631,
                  1785,
                  632,
                  1784,
                  834,
                  1586,
                  833
                ],
                "text": "is",
                "confidence": 0.164
              },
              {
                "boundingBox": [
                  1822,
                  632,
                  2115,
                  633,
                  2115,
                  835,
                  1822,
                  834
                ],
                "text": "not",
                "confidence": 0.164
              }
            ]
          }
        ]
      }
    ]
  }
}

```

>[!NOTE:]This is only a snippet from a much larger JSON result to conserve space and make the review easier.

A quick review of the JSON shows an initial bounding box that contains the line "Our greatest glory is not".  Scrolling through the JSON you will note that each word in that phrase (line), also has its own bounding box.  Again, recall that these bounding boxes are merely coordinates letting you know, where in the image, the text was located.

Like the OCR option, there are specific requirements around the images that the service can work with.  The Read API formats are expanded over OCR as listed here:

- image format - supported formats are JPEG, PNG, BMP, PDF, TIFF
- image size - for images, 50 x 50 and 10000 x 10000 pixels.  PDF pages must be 17 x 17 or smaller
- file size - less than 20MB

    >[!NOTE:]If you are using the free-tier subscription, only th efirst two pages of a PDF or TIFF documents will be processed.  Paid subscriptions support up to 200 pages and a maximum of 300 lines per page.