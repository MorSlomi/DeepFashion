# DeepFashion

The inspiration of starting this project came from the passion I have for Technolegy & Fashion.
The idea was to create an image classification with data that I have intrest in (my own clothes).
My goal of this project is to create an accurate image classifier using images of clothes from my own closet
in order to challenge myself and deal with real life data problems.

## Dataset 
As mentioned, the dataset consists of images of clothes from my own closet: 50 Tops, 50 Bottems, 26 shoes (in the near future I will add more images).
Here's an example of some images (after resizing the images 244 * 244) :

![DeepFashionVGG16_presenting_imgs](<Evaluation_Images/DeepFashionVGG16_presenting_imgs.jpg>)

All images were taken from a cell phone camera.

I moved the images to google drive in order to work with google colab (which enables to speed up the running time of the network with GPU).
Then separated the data into train (106 images) and validation (21 images) and kept it in the “train” and “validation” folders. 

As you can see, my dataset is small and there are not enough images in order to train a model from scratch, for this reason I decided to use a pre-trained model (VGG16) and fine-tune it with my data. To do so I loaded the pre-trained model without the top layer (which consists of fully connected layers). Then freeze the weights of all layers so that these layers will not be trained again.

## Building the model
I created a new model. The new model is based on the pre-trained model (VGG16 without the top layer). On top of it I added a fully connected layer, a batch normalization layer, a dropout layer and a softmax layer with three outputs (as the number of classes).

![summary_model](<Evaluation_Images/model_summary.jpg>)


In addition, I preformed data augmentation, which is a technique that can be used to artificially expand the size of a training dataset by creating modified versions of images in the dataset. Commom techniques of data augmentation include rotation, zooming, cropping, flipping, etc. The techniques I used are rescale, shifting the picture a few pixels, shearing, zooming and fliping.

## Training the model
Next, I trained the model with the following hyperparameters:
* Training batch size = 30
* Validation batch size = 21
* Epochs = 45
* 'Adam' optimizer with learning rate = 1e-5 and momentum = 0.99

## Evaluation 
In order to evatuate the model I created learning curves:

![Learning Curves - Accuracy](<Evaluation_Images/DeepFashionVGG16CurvesAcc.jpg>)
![Learning Curves - Accuracy](<Evaluation_Images/DeepFashionVGG16CurvesLoss.jpg>)



The validation accuracy is: 0.98

The validation loss is: 0.119


If we take a look at the confusion matrix, we will find out that the only error is between bottem and top:

![Confusion_matrix](<Evaluation_Images/DeepFashionVGG16_confusion_matrix.jpg>)


Here's an example of the predicted labels vs. the real labels for a few images:
![predicted_images](<Evaluation_Images/DeepFashionVGG16_predicted_imgs.jpg>)



## Future Work
In the near future, my intention is to add more images and insert them as testset.
In addition, I am thinking to add more images of different classes of clothes (as dresses, coats, jumpers, etc).
