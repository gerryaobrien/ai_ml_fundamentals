# Identify Features of Image Classification Solutions

Classification is a technique that we can use to predict which class, or category, something belongs to. The simplest variant of this is binary classification where we predict whether an entity belongs to one of two classes. It's often used to determine if something is true or false about the entity.

To help you better understand this concept, consider this example. Suppose we take a number of patients in a health clinic, and we gather some personal details, run some tests, and then identify which patients are diabetic and which are not diabetic. We can apply these learnings to create a function, that can be applied to these patient features, and give a result of 1 for patients that are diabetic, and 0 for patients that are not.

If we apply a similar logic to the classification of images, we might, for example, take a number of images that contain bicycles.  In our diabetic scenario above, we collected details about the person, that helped determine what resulted in a diabetic diagnosis.  In our image sample, we can use details about bicycles such as:

- pedals
- two wheels (wheels will likely be thin and contain spokes, although not always)
- narrow or small seat
- handlebars
- thin, tubular, frame

Take a look at some bicycles to get an idea of the characteristics that make it a bicycle.  Think about how you can instinctively know that it is classified as a bicycle.  What makes it different from a tricycle, a motorcycle, a uni-cycle, or even other objects like a car or bus.

So, how does our bicycle image example, translate to an image classification solution? We first need to understand that computers deal with images as pixels.  What the human eye sees as a coherent image containing a plethora of features such as shapes, colors, and ultimately, objects that we recognize, the computer sees as a matrix of dots that represent the image.  A single dot or pixel, has no relevance or significance unless it is evaluated in the context of the surrounding pixels, and the image overall.  Even in the picture of a bicycle, we might find other objects such as a wall, a road, some grass, etc. In order to distinguish a bicycle from the other objects, we need to train the computer to recognize the pixels that are representative of a bicycle.

Consider the task of teaching a toddler what a bicycle is.  You can show the toddler an example of a bicycle and tell them what it is.  However, they might see a motorcycle and call it a bicycle.  An even more remote option is that they might simply call anything with wheels, a bicycle.   They don't yet know what the distinguishing characteristics are.   However, the more bicycles you show them and reinforce the bicycle concept, along with the opposite side, such as telling them when other specific objects are *NOT* a bicycle, they begin to see the defining characteristics are common *ONLY* to bicycles.

To help the computer understand the same thing, we must identify key data about the bicycle objects and then assign that data to the class, or category, of bicycle.  In order to train the computer, you provide positive images of bicycles and images that are not bicycles so that you can develop patterns of recognition that the computer can follow.

## Image Classification with Azure Custom Vision Service

You can perform image classification using the Custom Vision Service, available as part of the Microsoft Cognitive Services offerings.  You will need to have a Cognitive Services account in our Microsoft Azure subscription to do so.  Using the [Custom Vision portal](https://www.customvision.ai/), you can perform three simple tasks to begin your classification project:

1. Upload labeled images.  You can also edit and add labels or tags in this portal for the images
1. Use those images to teach (train) Custom Vision about the key aspects of the images (what you want identified)
1. Evaluate the results and begin utilizing the REST APi calls with the new model

You can also create a new Custom Vision resource in the Microsoft Azure portal.  The lab will cover the key aspects of creating this resource in the Custom Vision portal, and then begin to use it to train and classify images.

One of the key considerations when using images for classification, is to ensure that you have sufficient images of the objects in question and those images should be of the object(s) from many different angles.  Think back to our example of a bicycle classification.  If we only use images of a bicycle from the side, the model will fail to correctly identify bicycles when the image is strictly from the front or back.  There will be insufficient data to evaluate for the classification.
