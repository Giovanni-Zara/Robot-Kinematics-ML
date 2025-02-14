# Robot Kinematics - Machine Learning Project

## Overview

This project is centered around solving forward kinematics problems for three distinct robot models using machine learning techniques. The robots vary in degrees of freedom (DOF): a 2-DOF planar robot (R2), a 3-DOF planar robot (R3), and a 5-DOF spatial robot (R5). The primary objective is to develop and evaluate machine learning models capable of accurately predicting the position and orientation of a robot's end-effector based on joint angles. The project involves exploratory data analysis (EDA), model development, hyperparameter tuning, and performance evaluation, including the computation and comparison of Jacobian matrices.

## Dataset

The dataset used in this project was generated using the Mujoco physics engine, which provides highly realistic simulations suitable for robotics applications. Each dataset includes the following features:

- **Joint Angles**: The angles of the robot's joints.
- **Directional Sine and Cosine Values**: These values help in understanding the orientation.
- **End-Effector Positions and Orientations**: The target variables to be predicted.

To ensure robust model generalization, different random seeds were used to partition the data into training and testing sets. This approach helps in avoiding overfitting and ensures that the model performs well on unseen data.

## Models

### R2 Robot (2-DOF Planar Robot)

- **Model**: Feedforward Neural Network (NN) with ReLU activation.
- **Approach**:
  - **Initial Model**: A simple linear model was implemented first, which performed poorly due to its inability to capture the non-linear relationships in the data.
  - **Enhanced Model**: A more complex model with a hidden layer and ReLU activation was then implemented, significantly improving performance.
- **Results**:
  - **Training MSE**: 0.1
  - **Test MSE**: 0.2
  - **Jacobian Comparison**: The mean difference between the learned and analytical Jacobians was 0.078, indicating good predictive capabilities.

### R3 Robot (3-DOF Planar Robot)

- **Model**: Support Vector Regressor (SVR) with AdaBoost.
- **Approach**:
  - **Initial Model**: Given the limitations of linear regression observed in the R2 model, an ensemble approach with SVR was adopted.
  - **Dataset**: The model was trained on both a small dataset (1k samples) and a larger dataset (10k samples) to evaluate the impact of data size on performance.
- **Results**:
  - **Training MSE**: \(3.15*10^{-5}\)
  - **Test MSE**: \(3.08*10^{-5}\)
  - **Jacobian Comparison**: The mean difference between the learned and analytical Jacobians was 0.020, indicating excellent predictive accuracy.

### R5 Robot (5-DOF Spatial Robot)

- **Model**: Deep Neural Network (DNN) with multiple hidden layers.
- **Approach**:
  - **Initial Model**: A DNN was implemented to handle the increased complexity of the 5-DOF robot. The model was initially trained on a small dataset (1k samples).
  - **Enhanced Model**: To improve performance, the model was retrained on a larger dataset (10k samples).
- **Results**:
  - **Training MSE**: 0.0059
  - **Test MSE**: 0.0054
  - **Jacobian Comparison**: The mean difference between the learned and analytical Jacobians was 0.49, indicating room for improvement, possibly due to non-constant link lengths.
