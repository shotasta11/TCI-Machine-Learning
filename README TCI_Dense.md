# TCI Forecasting For Tourism Recommendation with Dense Layer
## TCI
TCI is very helpful in identifying the comfort level of tourist destinations based on climate conditions. The results of the analysis based on the TCI method can be useful as one of the information on the schedule of visits for tourists

## Library 
import required libraries :
* import tensorflow
* import numpy
* import pandas

## Split Data 
Split the data by your choice, in this case we use 90:10 
> split_time = 50

> Day_train = Day[:split_time]

> TCI_train = TCI[:split_time]

> Day_valid = Day[split_time:]

> TCI_valid = TCI[split_time:]

## Creating The Model
Layers are reusable functions with trainable variables that have a specified mathematical structure. To find the best prediction, Adding a layers.Dense between the input and output gives the linear model more power, but is still only based on a single input timestep.

set the layer : 
> model = tf.keras.models.Sequential()

> model.add(tf.keras.layers.Dense(256, activation='relu', input_shape=[1]))

> model.add(tf.keras.layers.Dense(256, activation='relu'))

> model.add(tf.keras.layers.Dense(64, activation='relu'))

> model.add(tf.keras.layers.Dense(1))

and then we compile : 

> model.compile(optimizer='Adam', loss='mean_squared_error')

next, we fit the model with 500 epochs : 

> model.fit(Day_train,TCI_train, epochs=500)

**This model is far from optimized, so feel free to try another model* 

## Convert To tflite
with code :
> TCI_tflite_model = converter.convert()

## Testing Data 
we test with validation  data. In this case we input data at Days 50 : 

> input_data = np.array(Day_valid[0:1], dtype=np.float32)

> input_data = np.expand_dims(input_data, axis=0)

> interpreter.set_tensor(input_details[0]['index'], input_data)

> interpreter.invoke()
print(input_data)

___
[[50.]]
___

and the output :
> output_data = interpreter.get_tensor(output_details[0]['index'])

>print(output_data)

___
TCI
[[136.3944]]
___
