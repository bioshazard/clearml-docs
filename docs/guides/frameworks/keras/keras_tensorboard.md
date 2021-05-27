---
title: Keras with TensorBoard
---

The [keras_tensorboard.py](https://github.com/allegroai/clearml/blob/master/examples/frameworks/keras/keras_tensorboard.py)
example demonstrates the integration of **ClearML** into code which uses Keras and TensorBoard. 

The example does the following: 
1. Trains a simple deep neural network on the Keras built-in [MNIST](https://keras.io/api/datasets/mnist/#load_data-function) 
   dataset.
1. Builds a sequential model using a categorical crossentropy loss objective function. 
   
1. Specifies accuracy as the metric, and uses two callbacks: a TensorBoard callback and a model checkpoint callback. 
   
1. During script execution, it creates an experiment named `Keras with TensorBoard example` which is associated with the 
   `examples` project.

## Scalars

The loss and accuracy metric scalar plots appear in the **RESULTS** **>** **SCALARS**, along with the resource utilization 
plots, which are titled **:monitor: machine**.

![image](../../../img/examples_keras_01.png)

## Histograms

Histograms for layer density appear in **RESULTS** **>** **PLOTS**.

![image](../../../img/examples_keras_02.png)

## Hyperparameters

**ClearML** automatically logs command line options generated with `argparse`, and TensorFlow Definitions.

Command line options appear in **CONFIGURATIONS** **>** **HYPER PARAMETERS** **>** **Args**.

![image](../../../img/examples_keras_00.png)

TensorFlow Definitions appear in **TF_DEFINE**.

![image](../../../img/examples_keras_00a.png)

## Console

Text printed to the console for training progress, as well as all other console output, appear in **RESULTS** **>** **CONSOLE**.

![image](../../../img/examples_keras_03.png)

## Configuration objects

In the experiment code, a configuration dictionary is connected to the Task by calling the [Task.connect](../../../references/sdk/task.md#connect) 
method. 
```python
task.connect_configuration({'test': 1337, 'nested': {'key': 'value', 'number': 1}})
```

It appears in **CONFIGURATIONS** **>** **CONFIGURATION OBJECTS**. 

![image](../../../img/examples_keras_00b.png)