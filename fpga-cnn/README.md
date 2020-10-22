# FPGA-based Convolutional Neural Network acceleration

## Introduction

We leave in the century of fast changes when the flow of information is much bigger than we can process and analyze. That is the reason why real-time systems become more and more popular. Moor's law [[Ref](https://en.wikipedia.org/wiki/Moore%27s_law)] is not working anymore from 2019: it is physically impossible to make smaller transistors because of physics, on such small sizes the Relative Theory stops working, that is time for Quantum theory and another kind of computers. <br>
That is the reason why concurrent approaches become so popular - it is easy to make it horizontal-scalable. Multicore Processors, GPU's are very popular now, but they are not suitable for some approaches. That is why we are working with FPGA's. Maybe it can be a better platform for CNN?

### What is FPGA?
**FPGA** - Field Programmable Gate Array, one more integral circuit, projected to be reconfigured after manufacturing. Always is used for ASIC's (Application Specific Integrated Circuit) prototyping, but also it is a powerful platform for making own circuits [[Ref](https://numato.com/blog/differences-between-fpga-and-asics/#what-is-asic)]. The main pros of FPGA's are creating parallel processing in terms of DSP, own pipelines and reconfigurable logic.

### What is CNN?
**CNN** - Convolutional Neural Network, also known as ConvNet. It is a class of Deep Neural Networks, where primary (the most expensive) operation is Convolution. It is trendy in Image and Video processing for recognition classification and analysis problems. Also can be successfully used for time series analysis/predictions and natural language processing.  **Convolution** is an operation on functions, that express, how one modifies the shape of another one [[Ref](https://en.wikipedia.org/wiki/Convolution)].
<img src="images/conv.jpg">

## Solutions
So let us make a fast overview of the most popular approaches to run and accelerate CNN's on FPGA's

#### OpenVINO
Terasic boards are the most popular FPGA's in the world, so if somebody has ever worked with FPGA, most likely he deals with Intel Terasic's chips, such as Cyclone or Stratix. <br>
**OpenVINO** - where VINO stands for Open Visual Inference and Neural network Optimization - a toolkit from Intel to "extend computer vision and non-vision workloads across Intel® hardware, maximizing performance" [[Ref](https://docs.openvinotoolkit.org/latest/index.html)]. It is developed for usage on heterogeneous systems, but only made by Intel®, so when it bought Terasic Inc, OpenVINO extends to supporting FPGA's as well. Personally I have no expertise with this instrument, so more details are in other our article [here](/movidius) and [here](/movidius-2)

#### Mipsology
<img src="images/mipsology200x200.png" />
Mipsology product called ***Zebra***- a deep learning compute engine for neural network interface [[Ref](https://mipsology.com/)]. They promise that if the network was trained in any method, it could be run on CPU, GPU and FPGA with zero efforts without any changes inside the neural network and training process, what is more, it will be faster then before [[Ref](https://www.xilinx.com/video/events/mipsology-demonstrates-zebra.html)]

#### Vitis AI
Vitis - SDK from Xilinx. More info [here](https://www.xilinx.com/products/design-tools/vitis.html). <br>
<img src="images/vitis.jpg" />
**Vitis AI** is a development platform for AI inference on Xilinx hardware platforms (FPGA, Cloud) [[Ref](https://www.xilinx.com/products/design-tools/vitis/vitis-ai.html)]. It supports models designed and trained on Caffee, TensorFlow, and PyTorch. The workflow is: <br>
Develop a model using any framework (but using only supporting layers and versions, that are described in the official documentation)
Train the model
Optimize, Compile and Quantize the model using Vitis AI tools
Run the model on the DPU (Deep learning Processing Unit) - a particular IP block for Xilinx boards with UltraScale+ chip on it. It is a part of Vitis AI.
That is it! The development process is simple and is designed for AI programmers as much as for Embedded programmers.
Performance (from official sites):
Optimizer: reduce the model complexity from 5 to 50 times. Loss: up to 1% of accuracy.
Quantizer: Float32 -> Int8 quantization to make the model faster and lighter. Loss: up to 1% of accuracy.
Performance (from experience): <br>
As far as it is impossible to deploy unsupported layers, by replacing Instance norm with the Batch norm, it managed to reduce the time in average from 32ms to 9ms, but the MAPE (mean absolute percentage error) is up to 10%. We think it is because of replacing such a vital layer but cannot check this assumption.

