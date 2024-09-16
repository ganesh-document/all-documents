## <span style="color:red">**Keras**</span>
![aiml](img/keras.png)

- Keras is an open-source high-level Neural Network library, which is written in Python is capable enough to run on Theano, TensorFlow, or CNTK.
- It was developed by one of the Google engineers, Francois Chollet.
- It is made user-friendly, extensible, and modular for facilitating faster experimentation with deep neural networks.
- It not only supports Convolutional Networks and Recurrent Networks individually but also their combination.
- It cannot handle low-level computations, so it makes use of the Backend library to resolve it. The backend library act as a high-level API wrapper for the low-level API, which lets it run on TensorFlow, CNTK, or Theano.

## <span style="color:red">**What makes Keras special?**</span>

- Focus on user experience has always been a major part of Keras.

- Large adoption in the industry.

- It is a multi backend and supports multi-platform, which helps all the encoders come together for coding.

- Research community present for Keras works amazingly with the production community.

- Easy to grasp all concepts.

- It supports fast prototyping.

- It seamlessly runs on CPU as well as GPU.

- It provides the freedom to design any architecture, which then later is utilized as an API for the project.

- It is really very simple to get started with.

- Easy production of models actually makes Keras special.


## **How Keras support the claim of being multi-backend and multi-platform?**

Keras can be developed in R as well as Python, such that the code can be run with TensorFlow, Theano, CNTK, or MXNet as per the requirement. Keras can be run on CPU, NVIDIA GPU, AMD GPU, TPU, etc. It ensures that producing models with Keras is really simple as it totally supports to run with TensorFlow serving, GPU acceleration (WebKeras, Keras.js), Android (TF, TF Lite), iOS (Native CoreML) and Raspberry Pi.

## **Keras Backend**

Keras being a model-level library helps in developing deep learning models by offering high-level building blocks. All the low-level computations such as products of Tensor, convolutions, etc. are not handled by Keras itself, rather they depend on a specialized tensor manipulation library that is well optimized to serve as a backend engine. Keras has managed it so perfectly that instead of incorporating one single library of tensor and performing operations related to that particular library, it offers plugging of different backend engines into Keras.

Keras consist of three backend engines, which are as follows:

- **TensorFlow**
TensorFlow is a Google product, which is one of the most famous deep learning tools widely used in the research area of machine learning and deep neural network. It came into the market on 9th November 2015 under the Apache License 2.0. It is built in such a way that it can easily run on multiple CPUs and GPUs as well as on mobile operating systems. It consists of various wrappers in distinct languages such as Java, C++, or Python.

![aiml](img/keras-backend1.png)


- **Theano**
Theano was developed at the University of Montreal, Quebec, Canada, by the MILA group. It is an open-source python library that is widely used for performing mathematical operations on multi-dimensional arrays by incorporating scipy and numpy. It utilizes GPUs for faster computation and efficiently computes the gradients by building symbolic graphs automatically. It has come out to be very suitable for unstable expressions, as it first observes them numerically and then computes them with more stable algorithms.

![aiml](img/keras-backend2.png)

- **CNTK**
Microsoft Cognitive Toolkit is deep learning's open-source framework. It consists of all the basic building blocks, which are required to form a neural network. The models are trained using C++ or Python, but it incorporates C# or Java to load the model for making predictions.

![aiml](img/keras-backend3.png)

## **Advantages of Keras**

Keras encompasses the following advantages, which are as follows:

- It is very easy to understand and incorporate the faster deployment of network models.
- It has huge community support in the market as most of the AI companies are keen on using it.
- It supports multi backend, which means you can use any one of them among TensorFlow, CNTK, and Theano with Keras as a backend according to your requirement.
- Since it has an easy deployment, it also holds support for cross-platform. Following are the devices on which Keras can be deployed:
    1. iOS with CoreML
    2. Android with TensorFlow Android
    3. Web browser with .js support
    4. Cloud engine
    5. Raspberry pi
- It supports Data parallelism, which means Keras can be trained on multiple GPU's at an instance for speeding up the training time and processing a huge amount of data.

## **Disadvantages of Keras**

- The only disadvantage is that Keras has its own pre-configured layers, and if you want to create an abstract layer, it won't let you because it cannot handle low-level APIs. It only supports high-level API running on the top of the backend engine (TensorFlow, Theano, and CNTK).

```
#Based on the extracted code from the notebook, I'll transform the script to use Keras for defining and training a neural network that learns the AND and OR logic gates. I'll ensure that the neural network is correctly set up and that the previous errors and syntax issues are fixed.

#Here is the modified script using Keras:

import numpy as np
import pandas as pd
from tensorflow.keras.models import Sequential
from tensorflow.keras.layers import Dense

# Define the AND dataset
AND = pd.DataFrame({'x1': [0, 0, 1, 1], 'x2': [0, 1, 0, 1], 'y': [0, 0, 0, 1]})
inputs_and = AND[['x1', 'x2']]
targets_and = AND['y']

# Define the OR dataset
OR = pd.DataFrame({'x1': [0, 0, 1, 1], 'x2': [0, 1, 0, 1], 'y': [0, 1, 1, 1]})
inputs_or = OR[['x1', 'x2']]
targets_or = OR['y']

# Build the model
def build_model():
    model = Sequential()
    model.add(Dense(2, input_dim=2, activation='relu'))  # 2 neurons for input layer
    model.add(Dense(1, activation='sigmoid'))  # 1 neuron for output layer
    model.compile(loss='binary_crossentropy', optimizer='adam', metrics=['accuracy'])
    return model

# Train and evaluate the model for AND logic gate
model_and = build_model()
model_and.fit(inputs_and, targets_and, epochs=100, verbose=0)
loss_and, accuracy_and = model_and.evaluate(inputs_and, targets_and)
print(f'AND Gate - Loss: {loss_and}, Accuracy: {accuracy_and}')

# Train and evaluate the model for OR logic gate
model_or = build_model()
model_or.fit(inputs_or, targets_or, epochs=100, verbose=0)
loss_or, accuracy_or = model_or.evaluate(inputs_or, targets_or)
print(f'OR Gate - Loss: {loss_or}, Accuracy: {accuracy_or}')

# Predict using the trained models
predictions_and = model_and.predict(inputs_and)
predictions_or = model_or.predict(inputs_or)

print("AND Gate Predictions:")
print(np.round(predictions_and))

print("OR Gate Predictions:")
print(np.round(predictions_or))


### Explanation:
#- **Data Preparation**: The AND and OR datasets are defined as pandas DataFrames.
#- **Model Building**: A function `build_model` is created to define the neural network with Keras. The network consists of an input layer with 2 neurons (corresponding to the 2 input features) and an output layer with 1 neuron for binary classification.
#- **Training and Evaluation**: The model is trained separately for the AND and OR datasets. The training process is silent (verbose=0), and after training, the model's loss and accuracy are printed.
#- **Predictions**: The trained models are used to predict the outputs for the AND and OR datasets, and the predictions are printed.

#This script ensures proper use of Keras for defining, training, and evaluating neural networks for the given logic gate tasks.
```

## **Example-2**

```
import numpy as np

# Sample data for linear regression
X = np.array([[1], [2], [3], [4], [5]])
y = np.array([1, 3, 3, 2, 5])

# Linear regression with numpy
A = np.vstack([X.T, np.ones(len(X))]).T
m, c = np.linalg.lstsq(A, y, rcond=None)[0]

print(f"Slope: {m}, Intercept: {c}")
```

```
import numpy as np
import tensorflow as tf
from tensorflow.keras.models import Sequential
from tensorflow.keras.layers import Dense

# Sample data for linear regression
X = np.array([[1], [2], [3], [4], [5]])
y = np.array([1, 3, 3, 2, 5])

# Define the model
model = Sequential()
model.add(Dense(1, input_dim=1, kernel_initializer='normal', activation='linear'))

# Compile the model
model.compile(optimizer='adam', loss='mean_squared_error')

# Train the model
model.fit(X, y, epochs=100, verbose=0)

# Get the model parameters (weights and biases)
weights = model.layers[0].get_weights()
slope = weights[0][0][0]
intercept = weights[1][0]

print(f"Slope: {slope}, Intercept: {intercept}")
```

## **Example-3**

```
import matplotlib.pyplot as plt
import numpy as np
import sklearn.datasets
import tensorflow as tf
from tensorflow.keras.models import Sequential
from tensorflow.keras.layers import Dense
from tensorflow.keras.optimizers import Adam
from sklearn.model_selection import train_test_split

# Generate a dataset and plot it
np.random.seed(0)
X, y = sklearn.datasets.make_moons(200, noise=0.20)

# Split the data into training and test sets
X_train, X_test, y_train, y_test = train_test_split(X, y, test_size=0.2, random_state=0)

# Build and compile a Keras model
def build_keras_model(hidden_dim):
    model = Sequential()
    model.add(Dense(hidden_dim, input_dim=2, activation='tanh', kernel_regularizer=tf.keras.regularizers.l2(0.01)))
    model.add(Dense(2, activation='softmax'))
    model.compile(optimizer=Adam(learning_rate=0.01), loss='sparse_categorical_crossentropy', metrics=['accuracy'])
    return model

# Train the model
def train_keras_model(hidden_dim):
    model = build_keras_model(hidden_dim)
    model.fit(X_train, y_train, epochs=2000, batch_size=32, verbose=0)
    return model

# Plot decision boundary
def plot_decision_boundary(model, X, y):
    x_min, x_max = X[:, 0].min() - .5, X[:, 0].max() + .5
    y_min, y_max = X[:, 1].min() - .5, X[:, 1].max() + .5
    h = 0.01
    xx, yy = np.meshgrid(np.arange(x_min, x_max, h), np.arange(y_min, y_max, h))
    Z = model.predict(np.c_[xx.ravel(), yy.ravel()])
    Z = np.argmax(Z, axis=1)
    Z = Z.reshape(xx.shape)
    plt.contourf(xx, yy, Z, cmap=plt.cm.coolwarm)
    plt.scatter(X[:, 0], X[:, 1], c=y, cmap=plt.cm.seismic)
    plt.show()

# Build a model with a 3-dimensional hidden layer and plot the decision boundary
model = train_keras_model(3)
plot_decision_boundary(model, X, y)

# Visualize models with different hidden layer sizes
plt.figure(figsize=(16, 32))
hidden_layer_dimensions = [1, 2, 3, 4, 5, 20, 50]
for i, nn_hdim in enumerate(hidden_layer_dimensions):
    plt.subplot(5, 2, i+1)
    plt.title(f'Hidden Layer size {nn_hdim}')
    model = train_keras_model(nn_hdim)
    plot_decision_boundary(model, X, y)
plt.show()
```

## **Keras version**
```
import numpy as np
import matplotlib.pyplot as plt
from sklearn.model_selection import train_test_split
from sklearn.preprocessing import StandardScaler
from sklearn.datasets import make_regression
from tensorflow.keras.models import Sequential
from tensorflow.keras.layers import Dense
from tensorflow.keras.optimizers import SGD
from tensorflow.keras.losses import MeanSquaredError
```

```
# Generate synthetic data
X, y = make_regression(n_samples=1000, n_features=10, noise=0.1)
y = y.reshape(-1, 1)  # Reshape to match output dimensions

# Split data into training and test sets
X_train, X_test, y_train, y_test = train_test_split(X, y, test_size=0.2, random_state=42)

# Standardize the data
scaler_X = StandardScaler()
scaler_y = StandardScaler()

X_train = scaler_X.fit_transform(X_train)
X_test = scaler_X.transform(X_test)
y_train = scaler_y.fit_transform(y_train)
y_test = scaler_y.transform(y_test)
```

```
# Define the model
model = Sequential()
model.add(Dense(units=1, input_dim=X_train.shape[1], activation='linear'))

# Compile the model
model.compile(optimizer=SGD(learning_rate=0.01), loss=MeanSquaredError())
```

```
# Train the model
history = model.fit(X_train, y_train, epochs=1000, batch_size=32, verbose=1)
```

```
# Evaluate the model
y_pred = model.predict(X_test)
y_pred = scaler_y.inverse_transform(y_pred)
y_test_inverse = scaler_y.inverse_transform(y_test)

# Plot predictions vs actual
plt.scatter(y_test_inverse, y_pred, color='blue')
plt.plot([y_test_inverse.min(), y_test_inverse.max()], [y_test_inverse.min(), y_test_inverse.max()], 'k--', lw=2)
plt.xlabel('Actual')
plt.ylabel('Predicted')
plt.title('Predicted vs Actual')
plt.show()
```

## **#Keras version**

```
import tensorflow as tf
from tensorflow.keras.models import Sequential
from tensorflow.keras.layers import Dense
from tensorflow.keras.optimizers import SGD
from tensorflow.keras.losses import MeanSquaredError
```

```
# Split data into training and test sets
X_train, X_test, y_train, y_test = train_test_split(X, y, test_size=0.2, random_state=42)

# Standardize the data
scaler_X = StandardScaler()
scaler_y = StandardScaler()

X_train = scaler_X.fit_transform(X_train)
X_test = scaler_X.transform(X_test)
y_train = scaler_y.fit_transform(y_train)
y_test = scaler_y.transform(y_test)
```

```
from tensorflow.keras.layers import Dense, Dropout
```

```
# Define the model
model = Sequential()
model.add(Dense(units=128, input_dim=X_train.shape[1], activation='sigmoid'))  # First hidden layer H1
model.add(Dropout(0.2))  # Dropout layer with 20% rate
model.add(Dense(units=64, activation='relu'))  # Second hidden layer H2
model.add(Dropout(0.2))  # Dropout layer with 20% rate
model.add(Dense(units=32, activation='sigmoid'))  # Third hidden layer H3
#model.add(Dropout(0.2))  # Dropout layer with 20% rate
model.add(Dense(units=16, activation='relu'))  # First hidden layer H4
#model.add(Dropout(0.2))  # Dropout layer with 20% rate
model.add(Dense(units=8, activation='sigmoid'))  # Second hidden layer H5
#model.add(Dropout(0.2))  # Dropout layer with 20% rate
model.add(Dense(units=5, activation='relu'))  # Third hidden layer H6
#model.add(Dropout(0.2))  # Dropout layer with 20% rate

model.add(Dense(units=1, activation='linear'))  # Output layer
# Compile the model
model.compile(optimizer=SGD(learning_rate=0.05), loss=MeanSquaredError())
```

```
model.summary()
```

```
# Train the model
history = model.fit(X_train, y_train, epochs=1000, batch_size=32, verbose=1)
```

```
# Evaluate the model on test set
y_pred = model.predict(X_test)
y_pred = scaler_y.inverse_transform(y_pred)
y_test_inverse = scaler_y.inverse_transform(y_test)

# Call the function
mse, r2 = calculate_accuracy(y_test_inverse, y_pred)
```

```
# Evaluate the model on train set
y_pred_train = model.predict(X_train)
y_pred_train = scaler_y.inverse_transform(y_pred_train)
y_train_inverse = scaler_y.inverse_transform(y_train)

# Call the function
mse, r2 = calculate_accuracy(y_train_inverse, y_pred_train)
```

```
from tensorflow.keras.callbacks import EarlyStopping, ModelCheckpoint
from tensorflow.keras.wrappers.scikit_learn import KerasRegressor

from sklearn.model_selection import GridSearchCV
from tensorflow.keras.wrappers.scikit_learn import KerasRegressor
from tensorflow.keras.models import Sequential
from tensorflow.keras.layers import Dense, Dropout
from tensorflow.keras.optimizers import SGD


# Define the model creation function
def create_model(learning_rate=0.01, dropout_rate=0.0):
    model = Sequential()
    model.add(Dense(units=128, input_dim=X_train.shape[1], activation='sigmoid'))  # First hidden layer H1
    model.add(Dropout(0.2))  # Dropout layer with 20% rate
    model.add(Dense(units=64, activation='relu'))  # Second hidden layer H2
    model.add(Dropout(0.2))  # Dropout layer with 20% rate
    model.add(Dense(units=32, activation='sigmoid'))  # Third hidden layer H3
    #model.add(Dropout(0.2))  # Dropout layer with 20% rate
    model.add(Dense(units=16, activation='relu'))  # First hidden layer H4
    #model.add(Dropout(0.2))  # Dropout layer with 20% rate
    model.add(Dense(units=8, activation='sigmoid'))  # Second hidden layer H5
    #model.add(Dropout(0.2))  # Dropout layer with 20% rate
    model.add(Dense(units=5, activation='relu'))  # Third hidden layer H6
    #model.add(Dropout(0.2))  # Dropout layer with 20% rate

    optimizer = SGD(learning_rate=learning_rate)
    model.compile(optimizer=optimizer, loss='mean_squared_error')
    return model

# Create the model using KerasRegressor
model = KerasRegressor(build_fn=create_model, verbose=0)

# Define the hyperparameters to tune
param_grid = {
    'learning_rate': [0.01, 0.05, 0.1],
    'dropout_rate': [0.2, 0.5],
    'batch_size': [16, 32],
    'epochs': [100]
}

# Add early stopping and model checkpoint callbacks
early_stopping = EarlyStopping(monitor='val_loss', patience=10, verbose=1, restore_best_weights=True)
model_checkpoint = ModelCheckpoint('best_model.h5', monitor='val_loss', save_best_only=True, verbose=1)

# Use grid search with callbacks
grid = GridSearchCV(estimator=model, param_grid=param_grid, cv=3)
grid_result = grid.fit(X_train, y_train, validation_data=(X_test, y_test),
                       callbacks=[early_stopping, model_checkpoint])

# Summarize the results
print(f"Best: {grid_result.best_score_} using {grid_result.best_params_}")
```

```
# Summarize the results
print(f"Best: {grid_result.best_score_} using {grid_result.best_params_}")
```

```
import os
os.getcwd()
```

```
from tensorflow.keras.models import load_model
checkpoint_filepath = '/Users/pradmishra/Documents/Deep Learning Contents/DL5/best_model.h5'
```

```
# Load the saved model checkpoint
best_model = load_model(checkpoint_filepath)

# Evaluate the loaded model on test data
loss = best_model.evaluate(X_test, y_test)
print(f'Loaded model loss on test data: {loss}')
```

```
# Evaluate the model
y_pred = model.predict(X_test)
y_pred = scaler_y.inverse_transform(y_pred)
y_test_inverse = scaler_y.inverse_transform(y_test)

# Plot predictions vs actual
plt.scatter(y_test_inverse, y_pred, color='blue')
plt.plot([y_test_inverse.min(), y_test_inverse.max()], [y_test_inverse.min(), y_test_inverse.max()], 'k--', lw=2)
plt.xlabel('Actual')
plt.ylabel('Predicted')
plt.title('Predicted vs Actual')
plt.show()
```

## **Using Keras**

```
# Split data into training and test sets
X_train, X_test, y_train, y_test = train_test_split(X, y, test_size=0.2, random_state=42)

# Standardize the data
scaler_X = StandardScaler()
scaler_y = StandardScaler()

X_train = scaler_X.fit_transform(X_train)
X_test = scaler_X.transform(X_test)
y_train = scaler_y.fit_transform(y_train)
y_test = scaler_y.transform(y_test)
```

```
model = Sequential([
    Dense(64, input_dim=X_train.shape[1], activation='relu'),
    Dense(32, activation='relu'),
    Dense(16, activation='relu'),
    Dense(1, activation='linear')
])
```
```
model.compile(optimizer='adam', loss=MeanSquaredError())
```

```
history = model.fit(X_train, y_train, epochs=100, batch_size=32, verbose=1)
```

```
y_pred = model.predict(X_test)
y_pred = scaler_y.inverse_transform(y_pred)
y_test_inverse = scaler_y.inverse_transform(y_test)

plt.scatter(y_test_inverse, y_pred, color='blue')
plt.plot([y_test_inverse.min(), y_test_inverse.max()], [y_test_inverse.min(), y_test_inverse.max()], 'k--', lw=2)
plt.xlabel('Actual')
plt.ylabel('Predicted')
plt.title('Predicted vs Actual')
plt.show()
```


