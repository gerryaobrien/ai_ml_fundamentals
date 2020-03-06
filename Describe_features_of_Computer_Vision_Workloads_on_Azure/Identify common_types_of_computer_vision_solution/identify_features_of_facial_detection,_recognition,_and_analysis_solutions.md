# Identify Features of Facial Detection, Recognition, and Analysis Solutions

When it comes to facial detection, Microsoft offers the Azure Face service as well as the ability to perform face detection using the Computer Vision API.  But what is face detection.  The service offers pre-built algorithms that anybody can use to detect, recognize, and analyze human faces in the images that you send to the service.  In terms of face detection, you can ask the service to return the rectangle coordinates for any human faces that are found in an image.  Another option is to request a series of attributes related to faces such as:

- the head pose - orientation in a 3D space
- the gender of the detected faces
- a guess at an age
- what emotion is displayed
- if there is facial hair or the person is wearing glasses
- whether the face in the image has makeup applied
- whether the person in the image is smiling
- blur - how blurry the image is
- exposure - aspects such as underexposed or over exposed.  Note that this applies to the face in the image and not the overall image exposure
- noise - this refers to visual noise in the image.  If you have taken a photo with a high ISO setting for darker settings, you would notice this noise in the image.  The image looks grainy or full of tiny dots that make the image less clear
- occlusion - determines if there may be objects blocking the face in the image

Let's look a little deeper into face detection. One key aspect we noted earlier was that each face that is detected in an image, has a corresponding rectangle associated with it.  The rectangle consists of pixel coordinates for the left, top, width, and height parameters for each face detected.  You can use these coordinates for many purposes such as drawing a bounding box around the image, locating where in the overall image the face appears, or any other number of ways to use the face data. When faces are detected the response returned will contain a list of rectangle coordinates for all detected faces, in order from the largest face to the smallest.

You will also find that you can make use of face landmarks.  These landmarks relate to specific points on a face that are easily distinguishable, such as pupils of the eye or the outer side of an eyebrow.  An example of the 27 predefined landmarks are shown in the following image.  The service will return the coordinates of the points using units of pixels.

![Image showing facial landmarks related to lips, eyes, nose, etc](images/landmarks.1.png)

## Tips for More Accurate Results

When you decide on images to use, there are some considerations that can help improve the accuracy of the detection in the images.  

### Still Image Considerations

For still images, such as photographs, consider the following:

- image format - supported images are JPEG, PNG, GIF, and BMP
- file size - 4MB or smaller
- face size range - from 36 x 36 up to 4096 x 4096.   Smaller or larger faces will not be detected
- other issues - face detection can be impaired by extreme face angles, occlusion (objects blocking the face such as sunglasses or a hand).  Best results are obtained when the faces are full-frontal or as near as possible to full-frontal

### Video Considerations

Improving detection when using video feeds can accomplished by considering the following aspects:

- smoothing - if your video camera applies this effect, turn it off.  The potential blur between frames has s tendency to reduce clarity of the image
- shutter speed - faster shutter speeds improves clarity of the images in each frame because the motion is reduced
- shutter angle - if your camera supports shutter angle, use a lower shutter angle to produce clearer frames, resulting in better clarity for recognition
