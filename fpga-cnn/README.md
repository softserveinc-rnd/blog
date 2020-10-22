# FPGA-based Convolutional Neural Network acceleration

## Introduction

We leave in the century of fast changes when the flow of information is much bigger than we can process and analyze. That is the reason why real-time systems become more and more popular. Moor's law [[Ref](https://en.wikipedia.org/wiki/Moore%27s_law)] is not working anymore from 2019: it is physically impossible to make smaller transistors because of physics, on such small sizes the Relative Theory stops working, that is time for Quantum theory and another kind of computers. <br>
That is the reason why concurrent approaches become so popular - it is easy to make it horizontal-scalable. Multicore Processors, GPU's are very popular now, but they are not suitable for some approaches. That is why we are working with FPGA's. Maybe it can be a better platform for CNN?

### What is FPGA?
**FPGA** - Field Programmable Gate Array, one more integral circuit, projected to be reconfigured after manufacturing. Always is used for ASIC's (Application Specific Integrated Circuit) prototyping, but also it is a powerful platform for making own circuits [[Ref](https://numato.com/blog/differences-between-fpga-and-asics/#what-is-asic)]. The main pros of FPGA's are creating parallel processing in terms of DSP, own pipelines and reconfigurable logic.

### What is CNN?
**CNN** - Convolutional Neural Network, also known as ConvNet. It is a class of Deep Neural Networks, where primary (the most expensive) operation is Convolution. It is trendy in Image and Video processing for recognition classification and analysis problems. Also can be successfully used for time series analysis/predictions and natural language processing.  **Convolution** is an operation on functions, that express, how one modifies the shape of another one [[Ref](https://en.wikipedia.org/wiki/Convolution#:~:text=In%20mathematics%20(in%20particular%2C%20functional,the%20process%20of%20computing%20it.)].
<img src="images/conv.jpg">

## Solutions
So let us make a fast overview of the most popular approaches to run and accelerate CNN's on FPGA's

### OpenVINO
Terasic boards are the most popular FPGA's in the world, so if somebody has ever worked with FPGA, most likely he deals with Intel Terasic's chips, such as Cyclone or Stratix. <br>
**OpenVINO** - where VINO stands for Open Visual Inference and Neural network Optimization - a toolkit from Intel to "extend computer vision and non-vision workloads across Intel® hardware, maximizing performance" [[Ref](https://docs.openvinotoolkit.org/latest/index.html)]. It is developed for usage on heterogeneous systems, but only made by Intel®, so when it bought Terasic Inc, OpenVINO extends to supporting FPGA's as well. Personally I have no expertise with this instrument, so more details are in other our article [here](/movidius) and [here](/movidius-2)

### PYNQ

### Vitis AI

### Miposology

## Algorithms

#### quantisation
#### parallelism + caching

### Bare metal
#### GEMM

#### Vinogradov algorithm
##### pipeline

## Sources
MIT Technology Review, February 24, 2020: "We're not prepared for the end of Moore's Law" by Devid Rotman, [Ref](https://www.technologyreview.com/2020/02/24/905789/were-not-prepared-for-the-end-of-moores-law/)


