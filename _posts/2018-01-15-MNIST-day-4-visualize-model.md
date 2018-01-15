---
layout: post
title: "Visualization of the model, MNIST - Day 4."
description: "Visualize the model of previous MNIST work."
categories: [deep-learning]
tags: [mnist,keras,model,visualize,graphviz]
---

### The previous work

At the end of [day 3](/blog/2018/01/12/MNIST-day-3/), we successfully trained a model for the dataset MNIST which achieve the accuracy of 99% after 12 runs. Let's little by little explore what do they do, and dig a little bit deeper into CNN and Keras.

First I am very curious what does the model do, and their responsibility with Keras. A quick search leads me to document page of Keras and they are two types of models, a sequential one and one with functional API. Let's ignore the latter and focus on the one we had tested.

### Keras documents

Anybody want to read [the document](https://keras.io/getting-started/sequential-model-guide/) themselves, follow the link. Here are some quick notes on the sequential model:

- The Sequential model is a linear stack of layers.
- The model needs to know what input shape it should expect, and the first and only the first layer in a Sequential model needs to receive information about its input shape.
- You need to compile a model before training it

### Visualization efforts.

Keras has a document about [visualing a model](https://keras.io/visualization/). We are going to follow the step

Look like we can use `keras.utils.vis_utils` to visualize the model with

~~~ python
from keras.utils import plot_model
plot_model(model, to_file='model.png')
~~~

As the result, here is the code

~~~ python
import keras
from keras.utils import plot_model
from keras.models import Sequential
from keras.layers import Dense, Dropout, Flatten
from keras.layers import Conv2D, MaxPooling2D

num_classes = 10

model = Sequential()
model.add(Conv2D(32, kernel_size=(3, 3),
                 activation='relu',
                 input_shape=(28, 28, 1)))
model.add(Conv2D(64, (3, 3), activation='relu'))
model.add(MaxPooling2D(pool_size=(2, 2)))
model.add(Dropout(0.25))
model.add(Flatten())
model.add(Dense(128, activation='relu'))
model.add(Dropout(0.5))
model.add(Dense(num_classes, activation='softmax'))

model.compile(loss=keras.losses.categorical_crossentropy,
              optimizer=keras.optimizers.Adadelta(),
              metrics=['accuracy'])

plot_model(model, to_file="model.png")
~~~

Running the code yield error

~~~
ImportError('Failed to import pydot. You must install pydot'
ImportError: Failed to import pydot. You must install pydot and graphviz for `pydotprint` to work.
~~~

Install `pydot` and `graphviz` with

~~~ bash
$ pip install pydot
Collecting pydot
Collecting pyparsing>=2.1.4 (from pydot)
Building wheels for collected packages: pydot
Running setup.py bdist_wheel for pydot ... done
  Stored in directory: /home/Library/Caches/pip/wheels/62/48/83/42bc8712cb5f9bb93b8f3804e84b
31024046981097729ff44e
Successfully built pydot
Installing collected packages: pyparsing,pydot
Successfully installed pydot-1.2.4 pyparsing-2.2.0

$ pip install graphviz
Collecting graphviz
  Downloading graphviz-0.8.2-py2.py3-none-any.whl
Installing collected packages: graphviz
Successfully installed graphviz-0.8.2
~~~

Re-run the script with
~~~ bash
$ python visualize.py
~~~

Give the following images
![model.png](/assets/images/mnist/model.png)

### Next step

The next step I want to visualize how each layer affects the images, to grasp the essential part of this model.

