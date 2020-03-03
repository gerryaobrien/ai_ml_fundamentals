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

## Classification Types, Project Types, and Domains

In the Custom Vision projects that you create, you will be asked to determine the project type, classification type, and domain. The service offers two project types, Classification and Object Detection.  Classification is the area we are concerned about in this topic.  There are two options available for classification, Multilabel and Multiclass. Multilabel refers to an image having multiple tags while the Multiclass only has a single tag per image.

The service also provides some prebuilt domains for classification.  They are as follows:

- General - Optimized for a broad range of image classification tasks. If none of the other domains are appropriate, or you're unsure of which domain to choose, select the Generic domain.
- Food - Optimized for photographs of dishes as you would see them on a restaurant menu. If you want to classify photographs of individual fruits or vegetables, use the Food domain.
- Landmarks - Optimized for recognizable landmarks, both natural and artificial. This domain works best when the landmark is clearly visible in the photograph. This domain works even if the landmark is slightly obstructed by people in front of it.
- Retail - 	Optimized for images that are found in a shopping catalog or shopping website. If you want high precision classifying between dresses, pants, and shirts, use this domain.
- Adult - Optimized for adult oriented content
- General (compact) - Optimized for the constraints of real-time classification on mobile devices. The models generated by compact domains can be exported to run locally.
- Landmarks (compact) - Optimized for the constraints of real-time classification on mobile devices. The models generated by compact domains can be exported to run locally.
- Retail (compact) - Optimized for the constraints of real-time classification on mobile devices. The models generated by compact domains can be exported to run locally.

Once you have built your classifier, added images, trained and published it, you should consider how to improve the classification.  The following are recommendations from Microsoft on improving your classifier:

- Data Quantity Considerations - This is more important for your starting point.  The recommendation is to use at least 50 images.  The rationale behind this thought is that fewer images may result in a condition known as overfitting. If you are creating a classifier for apples vs. citrus, and you've used images of apples in hands and of citrus on white plates, the classifier may give undue importance to hands vs. plates, rather than apples vs. citrus.
- Data Balance - Using 500 images for one label and 50 images for another label makes for an imbalanced training dataset. This will cause the model to be more accurate in predicting one label than another. You're likely to see better results if you maintain at least a 1:2 ratio between the label with the fewest images and the label with the most images. For example, if the label with the most images has 500 images, the label with the least images should have at least 250 images for training.
- Variety - This concept focuses on variety in the images such as different backgrounds, different lighting, object size, camera angle, and style of photo.

Once you have addressed the above considerations, train the model again, then use new images to test the prediction results.   This can be a continuous cycle until you get the prediction accuracy you are looking for.
