# DL_File
import libraries
import tensorflow as tf
from tensorflow import keras
import pandas as pd
import numpy as np
import matplotlib.pyplot as plt
import random
%matplotlib inline

import datasets
mnist = tf.keras.datasets.mnist

split dataset into train and test data
(x_train,y_train), (x_test,y_test) = mnist.load_data()

to see length of training and testing dataset
len(x_train)
len(x_test)

shape of training dataset
x_train.shape
x_train[0]

to see how first image looks
plt.matshow(x_train[0])

normalize the image by scaling pixel intensities to the range 0,1
x_train=x_train/255
x_test=x_test/255

x_train[11]

define the network architecture using keras(using ReLU and softmax)
model = keras.Sequential([
keras.layers.Flatten(input_shape=(28,28)),
keras.layers.Dense(128, activation='relu'),
keras.layers.Dense(10, activation='softmax')
])

model.summary()

compile the model
model.compile(optimizer='sgd', loss='sparse_categorical_crossentropy',
metrics=['accuracy'])

train the model
history=model.fit(x_train,y_train,validation_data=(x_test,y_test),epochs=10)

evaluate the model
test_loss,test_acc=model.evaluate(x_test,y_test)
print("loss=%.3f" %test_loss)
print("accuracy=%.3f" %test_acc)

making prediction on new data
n=random.randint(0,9999)
plt.imshow(x_test[n])
plt.show()

use predict() on new data
predicted_value=model.predict(x_test)
print("num in img is=%d" %np.argmax(predicted_value[n])) \

plot graph for accuracy
history.history??

history.history.keys()

dict_keys(['loss','accuracy','val_loss','val_accuracy'])

plt.plot(history.history['accuracy'])
plt.plot(history.history['val_accuracy'])
plt.title('model accuracy')
plt.ylabel('accuracy')
plt.xlabel('epoch')
plt.legend(['Train','Validation'],loc='upper left')
plt.show()

plot graph for loss
plt.plot(history.history['loss'])
plt.plot(history.history['val_loss'])
plt.title('model loss')
plt.ylabel('loss')
plt.xlabel('epoch')
plt.legend(['Train','Validation'],loc='upper left')
plt.show()

plt.plot(history.history['accuracy'])
plt.plot(history.history['val_accuracy'])
plt.plot(history.history['loss'])
plt.plot(history.history['val_loss'])
plt.title('Training loss and accuracy')
plt.ylabel('accuracy/loss')
plt.xlabel('epoch')
plt.legend(['accuracy','val_accuracy','loss','val loss'])
plt.show()

save the model
keras_model_path="C:\Users\Lenovo\Downloads\Telegram Desktop\projects\VOIS" \

model.save(keras_model_path)

use the save model
restored_keras_model = tf.keras.models.load_model(keras_model_path)

Conclusion: With above code We can see, that throughout the epochs, our model accuracy increases and our model loss decreases,that is good since our model gains confidence with its predictions.
1. The two losses (loss and val_loss) are decreasing and the accuracy
(accuracy and val_accuracy)are increasing.
So this indicates the model is trained in a good way.
2. The val_accuracy is the measure of how good the predictions of your model are.
So In this case, it looks like the model is well trained after 10 epochs
