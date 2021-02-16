## Directory
I have already segregated all the images based on their dance form as per the train.csv file in different folders.So, it will be easy to classify them.
Also created a new folder 'valid' to validate the model,just used around 15 images from each dance form .
`````
dance_pred: /train:
		  /bharatanatyam
    		  /kathak
   		  /kathakali
   		  /kuchipudi
  		  /manipuri
  		  /mohiniyattam
   		  /odissi
    		  /sattriya
       /valid:
		  /bharatanatyam
    		  /kathak
   		  /kathakali
   		  /kuchipudi
  		  /manipuri
  		  /mohiniyattam
   		  /odissi
    		  /sattriya

	/test..
	/dance_v2.h5
	/submission.csv
	/training.ipynb
	/predictions.ipynb
`````
## Approach:
1: Used the ImageDataGenerator function to create new augmentated images.and then applied that function to all the images present in train and valid folder

2: Created a Sequential model with different layers and summary of the model is below:
````
_________________________________________________________________
Layer (type)                 Output Shape              Param #   
=================================================================
conv2d_1 (Conv2D)            (None, 254, 254, 32)      896       
_________________________________________________________________
max_pooling2d_1 (MaxPooling2 (None, 127, 127, 32)      0         
_________________________________________________________________
conv2d_2 (Conv2D)            (None, 125, 125, 64)      18496     
_________________________________________________________________
max_pooling2d_2 (MaxPooling2 (None, 62, 62, 64)        0         
_________________________________________________________________
conv2d_3 (Conv2D)            (None, 60, 60, 64)        36928     
_________________________________________________________________
max_pooling2d_3 (MaxPooling2 (None, 30, 30, 64)        0         
_________________________________________________________________
conv2d_4 (Conv2D)            (None, 28, 28, 64)        36928     
_________________________________________________________________
max_pooling2d_4 (MaxPooling2 (None, 14, 14, 64)        0         
_________________________________________________________________
flatten_1 (Flatten)          (None, 12544)             0         
_________________________________________________________________
dense_1 (Dense)              (None, 128)               1605760   
_________________________________________________________________
activation_1 (Activation)    (None, 128)               0         
_________________________________________________________________
dropout_1 (Dropout)          (None, 128)               0         
_________________________________________________________________
dense_2 (Dense)              (None, 64)                8256      
_________________________________________________________________
activation_2 (Activation)    (None, 64)                0         
_________________________________________________________________
dropout_2 (Dropout)          (None, 64)                0         
_________________________________________________________________
dense_3 (Dense)              (None, 64)                4160      
_________________________________________________________________
activation_3 (Activation)    (None, 64)                0         
_________________________________________________________________
dropout_3 (Dropout)          (None, 64)                0         
_________________________________________________________________
dense_4 (Dense)              (None, 8)                 520       
_________________________________________________________________
activation_4 (Activation)    (None, 8)                 0         
=================================================================
Total params: 1,711,944
Trainable params: 1,711,944
Non-trainable params: 0
````
Although, didnt know much about how to boost the performace with different paramaters, so used the same model created in my OpenCV python course.

3: Then fit the model with around 150 epochs, and other different parameter and validate the model.
   It did take around 2hours to run and then saved the model with "dance_v2.h5'

4: Then in predictions.ipynb notebook, Loaded the model and test.csv file.

5: Created the empty array to save the names of dance form predicted and convert it into the dataframe

6: Get the index value of max value present in a particular prediction obtained
 
7: Then using dictionary created based on the index values and dance form, get the final dance form append that to temp array and write that accross that particular image read from test.csv file
 dict={0:'bharatanatyam',
 1:'kathak',
 2:'kathakali',
 3:'kuchipudi',
 4:'manipuri',
 5:'mohiniyattam',
 6:'odissi',
 7:'sattriya'}


 (eg. prediction for a particular image :[0.0, 2.9802322e-08, 0.0, 0.0, 0.0, 0.0, 0.0, 0.9999881], 
  index value of max value present in list is 7 and 7 is mapped to dance form 'sattriya' and append that name to temp array

8: convert that temp into the dataframe and concat it with test dataframe 
