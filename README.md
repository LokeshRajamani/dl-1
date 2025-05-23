# Developing a Neural Network Regression Model

## AIM
To develop a neural network regression model for the given dataset.

## THEORY
Regression problems involve predicting a continuous output variable based on input features. Traditional linear regression models often struggle with complex patterns in data. Neural networks, specifically feedforward neural networks, can capture these complex relationships by using multiple layers of neurons and activation functions. In this experiment, a neural network model is introduced with a single linear layer that learns the parameters weight and bias using gradient descent.

## Neural Network Model
Include the neural network model diagram.

## DESIGN STEPS
### STEP 1: Generate Dataset

Create input values  from 1 to 50 and add random noise to introduce variations in output values .

### STEP 2: Initialize the Neural Network Model

Define a simple linear regression model using torch.nn.Linear() and initialize weights and bias values randomly.

### STEP 3: Define Loss Function and Optimizer

Use Mean Squared Error (MSE) as the loss function and optimize using Stochastic Gradient Descent (SGD) with a learning rate of 0.001.

### STEP 4: Train the Model

Run the training process for 100 epochs, compute loss, update weights and bias using backpropagation.

### STEP 5: Plot the Loss Curve

Track the loss function values across epochs to visualize convergence.

### STEP 6: Visualize the Best-Fit Line

Plot the original dataset along with the learned linear model.

### STEP 7: Make Predictions

Use the trained model to predict  for a new input value .

## PROGRAM

### Name: LOKESH R

### Register Number: 212222240055

```python
import torch
import torch.nn as nn
import torch.optim as optim
import numpy as np
import matplotlib.pyplot as plt
X=torch.linspace(1,70,70).reshape(-1,1)
torch.manual_seed(71)
e = torch.randint(-8, 9, (70, 1), dtype=torch.float)
y = 2 * X + 1 + e
print(y.shape)


plt.scatter(X.numpy(), y.numpy(), color='red')
plt.xlabel('x')
plt.ylabel('y')
plt.title('Generated Data for Linear Regression')
plt.show()
print("Name: LOKESH R")
print("Reg No: 212222240055")


torch.manual_seed(71)
class Model(nn.Module):
    def __init__(self, in_features, out_features):
        super().__init__()
        self.linear = nn.Linear(in_features, out_features)

    def forward(self, x):
        return self.linear(x)

model = Model(1, 1)


print(f'Initial Weight: {model.linear.weight.item():.8f}')
print(f'Initial Bias  : {model.linear.bias.item():.8f}')

loss_function = nn.MSELoss()
optimizer = torch.optim.SGD(model.parameters(), lr=0.0001)

epochs = 100
losses = []

for epoch in range(1, epochs + 1):
    optimizer.zero_grad()
    y_pred = model(X)
    loss = loss_function(y_pred, y)
    losses.append(loss.item())
    loss.backward()
    optimizer.step()
    print(f'Epoch: {epoch:3}  Loss: {loss.item():10.8f}  '
          f'Weight: {model.linear.weight.item():10.8f}  '
          f'Bias: {model.linear.bias.item():10.8f}')

plt.plot(range(epochs), losses)
plt.xlabel('Epoch')
plt.ylabel('Loss')
plt.title('Loss Curve')
plt.show()
print("Name: LOKESH R")
print("Reg No: 212222240055")

x1 = torch.tensor([X.min().item(), X.max().item()])
w1, b1 = model.linear.weight.item(), model.linear.bias.item()
y1 = x1 * w1 + b1

print(f'Final Weight: {w1:.8f}, Final Bias: {b1:.8f}')
print(f'X range: {x1.numpy()}')
print(f'Predicted Y values: {y1.numpy()}')

plt.scatter(X.numpy(), y.numpy(), label="Original Data")
plt.plot(x1.numpy(), y1.numpy(), 'r', label="Best-Fit Line")
plt.xlabel('x')
plt.ylabel('y')
plt.title('Trained Model: Best-Fit Line')
plt.legend()
plt.show()
print("Name: LOKESH R")
print("Reg No: 212222240055")

X_new = torch.tensor([[75.0]])
y_new = model(X_new)
print(f'Prediction for X=75: {y_new.item():.8f}')

torch.save(model.state_dict(),'LokeshDLex1.pt')
print("\nModel saved as 'linear_regression_model.pth'")

```

### OUTPUT:


![Screenshot 2025-03-27 101134](https://github.com/user-attachments/assets/401b343f-8529-403f-9104-fd62b22df8ad)


![Screenshot 2025-03-27 101141](https://github.com/user-attachments/assets/c6333f3d-0c66-4101-93aa-eaa5c64a3154)


![Screenshot 2025-03-27 101150](https://github.com/user-attachments/assets/bcf798e0-2570-4ab9-b512-1cad651fd74f)




![Screenshot 2025-03-27 101349](https://github.com/user-attachments/assets/fc77d5fc-5e47-4349-b052-9c8b2356a50c)



## RESULT
Thus, a neural network regression model was successfully developed and trained using PyTorch.
