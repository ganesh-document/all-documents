## **Linear Regression DL using PT KS and TF**
```
import torch
import torch.nn as nn
import torch.optim as optim

import numpy as np
import matplotlib.pyplot as plt

from sklearn.model_selection import train_test_split
from sklearn.preprocessing import StandardScaler
from sklearn.datasets import make_regression
```

```
# Generate synthetic data
X, y = make_regression(n_samples=10000, n_features=10, noise=0.1)
y = y.reshape(-1, 1)  # Reshape to match output dimensions

# Split data into training and test sets
X_train, X_test, y_train, y_test = train_test_split(X, y, test_size=0.2, random_state=42)
X_train.shape, X_test.shape, y_train.shape, y_test.shape
```

```
X_train[0:5]
```

```
# Standardize the data
scaler_X = StandardScaler()
scaler_y = StandardScaler()

X_train = scaler_X.fit_transform(X_train)
X_test = scaler_X.transform(X_test)
y_train = scaler_y.fit_transform(y_train)
y_test = scaler_y.transform(y_test)
```

```
# Convert to PyTorch tensors
X_train = torch.tensor(X_train, dtype=torch.float32)
X_test = torch.tensor(X_test, dtype=torch.float32)
y_train = torch.tensor(y_train, dtype=torch.float32)
y_test = torch.tensor(y_test, dtype=torch.float32)
```

```
class LinearRegressionModel(nn.Module):
    def __init__(self, input_dim, output_dim):
        super(LinearRegressionModel, self).__init__()
        self.linear = nn.Linear(input_dim, output_dim)

    def forward(self, x):
        return self.linear(x)
```

```
# Instantiate the model
input_dim = X_train.shape[1]
output_dim = 1
model = LinearRegressionModel(input_dim, output_dim)
```

```
criterion = nn.MSELoss()
optimizer = optim.SGD(model.parameters(), lr=0.05)
```

```
num_epochs = 1000
for epoch in range(num_epochs):
    model.train()

    # Forward pass
    outputs = model(X_train)
    loss = criterion(outputs, y_train)

    # Backward pass and optimization
    optimizer.zero_grad()
    loss.backward()
    optimizer.step()

    if (epoch+1) % 100 == 0:
        print(f'Epoch [{epoch+1}/{num_epochs}], Loss: {loss.item():.4f}')
```

```
model.eval()
```

```
model.eval()
with torch.no_grad():
    predicted = model(X_test)
    predicted = scaler_y.inverse_transform(predicted.numpy())
    actual = scaler_y.inverse_transform(y_test.numpy())

# Plot predictions vs actual
plt.scatter(actual, predicted, color='blue')
plt.plot([actual.min(), actual.max()], [actual.min(), actual.max()], 'k--', lw=2)
plt.xlabel('Actual')
plt.ylabel('Predicted')
plt.title('Predicted vs Actual')
plt.show()
```

## **Boston Housing Price Prediction**

```
import torch
import torch.nn as nn
import torch.optim as optim
import numpy as np
import matplotlib.pyplot as plt
from sklearn.model_selection import train_test_split
from sklearn.preprocessing import StandardScaler
```

```
import pandas as pd
boston = pd.read_csv("https://raw.githubusercontent.com/selva86/datasets/master/BostonHousing.csv")
boston.info()
```

```
boston.head()
```

```
y = boston.pop("medv")
X = boston
```

```
y = np.array(y)
y
```

```
y.reshape(-1, 1)
```
# Load the dataset
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

# Convert to PyTorch tensors
X_train = torch.tensor(X_train, dtype=torch.float32)
X_test = torch.tensor(X_test, dtype=torch.float32)
y_train = torch.tensor(y_train, dtype=torch.float32)
y_test = torch.tensor(y_test, dtype=torch.float32)
```

```
X_train.shape, X_test.shape, y_train.shape, y_test.shape
```

```
class LinearRegressionModel(nn.Module):
    def __init__(self, input_dim, output_dim):
        super(LinearRegressionModel, self).__init__()
        self.linear = nn.Linear(input_dim, output_dim)

    def forward(self, x):
        return self.linear(x)

# Instantiate the model
input_dim = X_train.shape[1]
output_dim = 1
model = LinearRegressionModel(input_dim, output_dim)
```

```
criterion = nn.MSELoss()
optimizer = optim.SGD(model.parameters(), lr=0.05)
```

```
num_epochs = 5000
for epoch in range(num_epochs):
    model.train()

    # Forward pass
    outputs = model(X_train)
    loss = criterion(outputs, y_train)

    # Backward pass and optimization
    optimizer.zero_grad()
    loss.backward()
    optimizer.step()

    if (epoch+1) % 100 == 0:
        print(f'Epoch [{epoch+1}/{num_epochs}], Loss: {loss.item():.4f}')
```

```
model.eval()
with torch.no_grad():
    predicted = model(X_test)
    predicted = scaler_y.inverse_transform(predicted.numpy())
    actual = scaler_y.inverse_transform(y_test.numpy())

# Plot predictions vs actual
plt.scatter(actual, predicted, color='blue')
plt.plot([actual.min(), actual.max()], [actual.min(), actual.max()], 'k--', lw=2)
plt.xlabel('Actual')
plt.ylabel('Predicted')
plt.title('Predicted vs Actual')
plt.show()
```

```
from sklearn.metrics import mean_squared_error, r2_score

def calculate_accuracy(actual, predicted):
    # Calculate Mean Squared Error
    mse = mean_squared_error(actual, predicted)
    
    # Calculate R² score
    r2 = r2_score(actual, predicted)
    
    print(f'Mean Squared Error (MSE): {mse:.4f}')
    print(f'R² Score: {r2:.4f}')
    
    return mse, r2

# Call the function
mse, r2 = calculate_accuracy(actual, predicted)
```


