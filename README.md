# IMU_MLDL

## 1. Noise Filter Module

As you have suggested, we have re-trainined the autoencoder models so that each model filters 1 axis data instead of filtering them simultaneously.

We have also created a simple custom padding layer so that the model deals better with initial and final values, which were our concerns beforehand.

### How to use model to filter data

The how_to_use.ipynb file is an example of how to use the model.
The following is a written description of how to use the model.

1. load the model
2. load data
3. normalize data
    - accelerometer: [-16, 16] -> [-1, 1]
    - gyroscope: [-2000, 2000] -> [-1, 1]
4. reshape data to fit the model: (1, 1000, 1)
5. convert to tensor
6. input data into model to filter
7. check result
8. multiply 16 for accelerometer and 2000 for gyroscope again, if needed

### Accelerometer

For filtering accelerometer data, we have suggested you with 2 autoencoder models for each axis. This is because accelerometer data are very noisy, and we weren't sure if filtering these data are actually helpful (since some data points that seem "noisy" might actually not be noise, but instead are important data points for calculation)

One model is a simple configuration of Conv2D layers, and the other is a more complex model with more layers.

The simpler model doesn't filter noise very much, but is a more consistent one.

The more complex model filters more noise, but it sometimes shows low accuracy in special cases.

### Gyroscope

To filter gyroscope data, we have used the same layer configuration as the simpler model used to filter the accelerometer data, and it shows impressive performance.

### The Model Configuration

We have also attached the sample ipynb files of the models that we've built so that you can check.

### Sample Output

The sample_output.csv file is a sample csv file with the output data from the models.
The columns are as follows:
    - frame: = index
    - {accel/gyro}_x_input: the input data
    - {accel/gyro}_x_given: the given model answer data in the .csv files we are provided with
    - accel_x_output: the output data points from the complex model
    - accel_x_simple_output: the output data points from the simple model
    - gyro_x_output: the output data points from the model
