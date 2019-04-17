# Coral Evaluation

## Experiment objectives
Google announced Beta version of their Coral AI device a month ago and we had a possibility to evaluate it and compare with Intel's Movidius and Movidius 2 devices. Main idea of evaluation is to compare the performance of all sticks when same neural network is executed.
## Obtaining internal neural network representation
The main problem to be solved is that Movidius and Coral use different internal representations of the networks. From the other point of view, Coral is in beta and supports only several NN architectures. Fortunately, the last version of OpenVINO (2019 R1) has the support of [Frozen Quantized Topologies](https://docs.openvinotoolkit.org/latest/_docs_MO_DG_prepare_model_convert_model_Convert_Model_From_TensorFlow.html) that Coral uses as well. Moreover, documentation contains recommendations for conversion of such networks in inference engine implementation used by Movidius hardware :

> "It is necessary to specify the following command line parameters for the Model Optimizer to convert some of the models from the list above: --input input --input_shape [1,HEIGHT,WIDTH,3]. Where HEIGHT and WIDTH are the input images height and width for which the model was trained."
>

Information about networks selected for comparison are summarized in Table 1.
*Table 1. Networks, selected for experiments.*

<table>
<tr>
    <th>Network</th>
    <th>URL</th>
    <th>Conversion parameters</th>
    <th>Result</th>
</tr>
<tr>
    <td>Inception V1</td>
    <td>
    	<a href="http://download.tensorflow.org/models/inception_v1_224_quant_20181026.tgz">
    	inception_v1_224_quant_20181026.tgz	
    	</a>
    </td>
    <td><p>--input_model inception_v1_224_quant_frozen.pb 
		<p>--input input
		<p>--input_shape [1,224,224,3]
		<p>--data_type FP16 
	</td>
	<td>
	Converted
	</td>
</tr>
<tr>
	<td>Inception V2</td>
	<td><a href="http://download.tensorflow.org/models/inception_v2_224_quant_20181026.tgz">inception_v2_224_quant_20181026.tgz</a></td>
	<td><p>--input_model inception_v2_224_quant_frozen.pb
			<p>--input input
            <p>--input_shape [1,224,224,3]
            <p>--data_type FP16
    </td>
	<td>Converted</td>
</tr>
<tr>
	<td>Inception V3</td>
	<td><a href="http://download.tensorflow.org/models/tflite_11_05_08/inception_v3_quant.tgz">inception_v3_quant.tgz</a></td>
	<td><p>--input_model inception_v3_quant_frozen.pb
			<p>--input input
            <p>--input_shape [1,299,299,3]
            <p>--data_type FP16
    </td>
	<td>Converted</td>
</tr>
<tr>
	<td>Inception V4</td>
	<td><a href="http://download.tensorflow.org/models/inception_v4_299_quant_20181026.tgz">inception_v4_299_quant_20181026.tgz</a></td>
	<td><p>--input_model inception_v4_299_quant_frozen.pb
			<p>--input input
            <p>--input_shape [1,299,299,3]
            <p>--data_type FP16
    </td>
	<td>Converted</td>
</tr>
<tr>
	<td>Mobilenet V1 0.25 128</td>
	<td><a href="http://download.tensorflow.org/models/mobilenet_v1_2018_08_02/mobilenet_v1_0.25_128_quant.tgz">mobilenet_v1_0.25_128_quant.tgz</a></td>
	<td><p>--input_model mobilenet_v1_0.25_128_quant_frozen.pb
			<p>--input input
            <p>--input_shape [1,128,128,3]
            <p>--data_type FP16
     </td>
	<td>Converted</td>
</tr>
<tr>
	<td>Mobilenet V1 1.0 224</td>
	<td><a href="http://download.tensorflow.org/models/mobilenet_v1_2018_08_02/mobilenet_v1_1.0_224_quant.tgz">mobilenet_v1_1.0_224_quant.tgz</a></td>
	<td><p>--input_model mobilenet_v1_1.0_224_quant_frozen.pb
			<p>--input input
            <p>--input_shape [1,224,224,3]
            <p>--data_type FP16
    </td>
	<tdConverted></td>
</tr>
<tr>
	<td>Mobilenet V2 1.0 224</td>
	<td><a href="http://download.tensorflow.org/models/tflite_11_05_08/mobilenet_v2_1.0_224_quant.tgz">mobilenet_v1_1.0_224_quant.tgz</a></td>
	<td><p>--input_model mobilenet_v2_1.0_224_quant_frozen.pb
			<p>--input input
            <p>--input_shape [1,224,224,3]
            <p>--data_type FP16
    </td>
	<td>Converted</td>
</tr>
<tr>
	<td>MobileNet SSD v1 (COCO)</td>
	<td><a href="http://download.tensorflow.org/models/object_detection/ssd_mobilenet_v1_quantized_300x300_coco14_sync_2018_07_18.tar.gz">ssd_mobilenet_v1_quantized_300x300_coco14_sync_2018_07_18.tar.gz</a></td>
	<td><p>--input_model tflite_graph.pb
			<p>--tensorflow_use_custom_operations_config c:\IntelSWTools\openvino\deployment_tools\model_optimizer\extensions\front\tf\ssd_support.json
            <p>--tensorflow_object_detection_api_pipeline_config pipeline.config
            <p>--input_shape [1,300,300,3]
            <p>--data_type FP16
    </td>
	<td>Conversion errors
Model Optimizer version: 2019.1.0-341-gc9b66a2
[ ERROR ] Cannot infer shapes or values for node "TFLite_Detection_PostProcess".
[ ERROR ] Op type not registered 'TFLite_Detection_PostProcess' in binary running on DESKTOP-816AP20. Make sure the Op and Kernel are registered in the binary running in this process. Note that if you are loading a saved graph which used ops from tf.contrib, accessing (e.g.) `tf.contrib.resampler` should be done before importing the graph, as contrib ops are lazily registered when the module is first accessed.
[ ERROR ]
[ ERROR ] It can happen due to bug in custom shape infer function <function tf_native_tf_node_infer at 0x000002D007A9B598>.
[ ERROR ] Or because the node inputs have incorrect values/shapes.
[ ERROR ] Or because input shapes are incorrect (embedded to the model or passed via --input_shape).
[ ERROR ] Run Model Optimizer with --log_level=DEBUG for more information.
[ ERROR ] Exception occurred during running replacer "REPLACEMENT_ID" (<class 'extensions.middle.PartialInfer.PartialInfer'>): Stopped shape/value propagation at "TFLite_Detection_PostProcess" node.
	</td>
</tr>
<tr>
	<td>MobileNet SSD v2 (COCO)</td>
	<td><a href="http://download.tensorflow.org/models/object_detection/ssd_mobilenet_v2_quantized_300x300_coco_2019_01_03.tar.gz">ssd_mobilenet_v2_quantized_300x300_coco_2019_01_03.tar.gz</a></td>
	<td><p>--input_model tflite_graph.pb
			<p>--tensorflow_use_custom_operations_config c:\IntelSWTools\openvino\deployment_tools\model_optimizer\extensions\front\tf\ssd_v2_support.jso
            <p>--tensorflow_object_detection_api_pipeline_config pipeline.config
            <p>--input_shape [1,300,300,3]
            <p>--data_type FP16
            <p>--reverse_input_channels
    </td>
	<td><p>Conversion errors
<p>Model Optimizer version: 2019.1.0-341-gc9b66a2
<p>[ ERROR ] Cannot infer shapes or values for node "TFLite_Detection_PostProcess".
<p>[ ERROR ] Op type not registered 'TFLite_Detection_PostProcess' in binary running on DESKTOP-816AP20. 
Make sure the Op and Kernel are registered in the binary running in this process. Note that if you are loading a saved graph which used ops from tf.contrib, accessing (e.g.) `tf.contrib.resampler` should be done before importing the graph, as contrib ops are lazily registered when the module is first accessed.
<p>[ ERROR ]
<p>[ ERROR ] It can happen due to bug in custom shape infer function <function tf_native_tf_node_infer at 0x000002084589E620>.
<p>[ ERROR ] Or because the node inputs have incorrect values/shapes.
<p>[ ERROR ] Or because input shapes are incorrect (embedded to the model or passed via --input_shape).
<p>[ ERROR ] Run Model Optimizer with --log_level=DEBUG for more information.
<p>[ ERROR ] Exception occurred during running replacer "REPLACEMENT_ID" (<class 'extensions.middle.PartialInfer.PartialInfer'>): Stopped shape/value propagation at "TFLite_Detection_PostProcess" node.
	</td>
</tr>
<tr>
	<td>MobileNet SSD v2 (Faces)</td>
	<td><a href="http://download.tensorflow.org/models/object_detection/facessd_mobilenet_v2_quantized_320x320_open_image_v4.tar.gz">facessd_mobilenet_v2_quantized_320x320_open_image_v4.tar.gz</a></td>
	<td><p>--input_model tflite_graph.pb
			<p>--tensorflow_use_custom_operations_config c:\IntelSWTools\openvino\deployment_tools\model_optimizer\extensions\front\tf\ssd_v2_support.json
            <p>--tensorflow_object_detection_api_pipeline_config pipeline.config
            <p>--input_shape [1,320,320,3]
            <p>--data_type FP16
    </td>
	<td><p>Conversion errors
<p>Model Optimizer version: 2019.1.0-341-gc9b66a2
<p>[ ERROR ] Cannot infer shapes or values for node "TFLite_Detection_PostProcess".
<p>[ ERROR ] Op type not registered 'TFLite_Detection_PostProcess' in binary running on DESKTOP-816AP20. Make sure the Op and Kernel are registered in the binary running in this process. Note that if you are loading a saved graph which used ops from tf.contrib, accessing (e.g.) `tf.contrib.resampler` should be done before importing the graph, as contrib ops are lazily registered when the module is first accessed.
<p>[ ERROR ]
<p>[ ERROR ] It can happen due to bug in custom shape infer function <function tf_native_tf_node_infer at 0x000001A1C01BC598>.
<p>[ ERROR ] Or because the node inputs have incorrect values/shapes.
<p>[ ERROR ] Or because input shapes are incorrect (embedded to the model or passed via --input_shape).
<p>[ ERROR ] Run Model Optimizer with --log_level=DEBUG for more information.
<p>[ ERROR ] Exception occurred during running replacer "REPLACEMENT_ID" (<class 'extensions.middle.PartialInfer.PartialInfer'>): Stopped shape/value propagation at "TFLite_Detection_PostProcess" node.
	</td>
</tr>
</table>

Raspberry Pi 3+ was selected as platform for Coral and Movidius evaluation. Taking into account that OpenVINO installation for Raspbian doesn't contain model optimizer, conversion was made on Win 10 notebook with the installed openVINO 2019 R1. Note that out of 10 neural networks selected for the comparison, only 7 were converted without errors. Information about errors was posted to Intel's forum and we are waiting for answer.


## Performance measuring

For chip performance measurement, we used the above mentioned  TensorFlow and TensorFlowLite implementations of Inception V1, Inception V2, Inception V3, Inception V4, Mobilenet V1 0.25 128, Mobilenet V1 1.0 224, Mobilenet V2 1.0 224 networks. Test images were loaded to the stick for classification and measuring of image processing speed. 20 test images were used for experiment with 50 cycles run for data collection. Results are provided in Table 2.

Note that attempts to use Inception V3, Inception V4 and Mobilenet V2 1.0 224 on Movidius 1 resulted in unexpected errors, nevertheless that models were converted without any problems. Situation with Movidius 2 was more strange - none network was even possible to load into the chip, some assertion was involved during the loading process. Information about such Movidius 2 behavior was posted to [Intel's forum](https://software.intel.com/en-us/forums/computer-vision/topic/807826) and we are waiting for answer.

We also made the second experiment for EdgeTPU on Dev board to avoid USB2 bias on the device speed (Raspberry Pi 3 B+ has only USB2, when Coral was designed for USB3). Performance increased, but only in 1.4 - 2 times. Details are also shown in table 2 below, corresponding visualization in Figure 1 and 2. 

*Table 2. Results of performance measuring.*

<table>
	<tr>
		<td rowspan="3">Network</td>
		<td colspan="9">Image processing time, sec</td>
	</tr>
	<tr>		
        <td colspan="3">TPU on Dev board</td>
		<td colspan="3">Coral</td>
		<td colspan="3">Movidius 1</td>
	</tr>
	<tr>		
        <td>mean</td>
		<td>std</td>
		<td>median</td>
		<td>mean</td>
		<td>std</td>
		<td>median</td>
		<td>mean</td>
		<td>std</td>
		<td>median</td>
	</tr>
	<tr>
        <td>Inception V1</td>
		<td>0.410</td>
        <td>12.76 e-4</td>
        <td>0.410</td>
        <td>0.612</td>
        <td>282.16 e-4</td>
        <td>0.625</td>
        <td>0.113</td>
        <td>4.57 e-4</td>
        <td>0.113</td>
	</tr>
	<tr>
		<td>Inception V2</td>
		<td>0.646</td>
        <td>16.09 e-4</td>
        <td>0.646</td>
        <td>0.918</td>
        <td>4.00 e-4</td>
        <td>0.918</td>
        <td>0.149</td>
        <td>3.66 e-4</td>
        <td>0.149</td>
	</tr>
	<tr>
		<td>Inception V3</td>
		<td>1.553</td>
        <td>42.22 e-4</td>
        <td>1.553</td>
        <td>2.288</td>
        <td>26.87 e-4</td>
        <td>2.287</td>
        <td></td>
        <td></td>
        <td></td>
	</tr>
	<tr>
		<td>Inception V4</td>
		<td>3.291</td>
        <td>50.05 e-4</td>
        <td>3.291</td>
        <td>4.835</td>
        <td>16.21 e-4</td>
        <td>4.835</td>
        <td></td>
        <td></td>
        <td></td>
	</tr>
	<tr>
		<td>Mobilenet V1 0.25 128</td>
		<td>0.009</td>
        <td>0.67 e-4</td>
        <td>0.009</td>
        <td>0.018</td>
        <td>1.38 e-4</td>
        <td>0.018</td>
        <td>0.018</td>
        <td>6.87 e-4</td>
        <td>0.018</td>
	</tr>
	<tr>
		<td>Mobilenet V1 1.0 224</td>
		<td>0.182</td>
        <td>5.42 e-4</td>
        <td>0.182</td>
        <td>0.305</td>
        <td>2.45 e-4</td>
        <td>0.304</td>
        <td>0.069</td>
        <td>3.98 e-4</td>
        <td>0.069</td>
	</tr>
	<tr>
		<td>Mobilenet V2 1.0 224</td>
		<td>0.143</td>
        <td>3.21 e-4</td>
        <td>0.143</td>
        <td>0.269</td>
        <td>2.76 e-4</td>
        <td>0.269</td>
        <td></td>
        <td></td>
        <td></td>
	</tr>
</table>



![](img/image-processing-time-coral-edge-tpu-1.png) ![](img/image-processing-time-coral-edge-tpu-2.png)

*Figure 1. Image processing time comparison for Edge TPU on Dev board and Coral.*

![](img/image-processing-time-coral-edge-tpu-movidius-1.png) ![](img/image-processing-time-coral-edge-tpu-movidius-1.png)

*Figure 2.  Image processing time comparison for EdgeTPU, Corel and Movidius 1.*

## Power consumption
We used XTARs USB Detector to measure power consumption during the computations. Measurements were made for Coral and Movidius1 only, becauseit was impossible to measure EdgeTPU consumption  current on Dev board without changes in board design. Results are shown in Table3. We also made computations of energy consumption in terms of Images per Joule (see Figure 3).

*Table 3. Power consumption of Coral and Movidius 1.*

| Device     |  U,B |  I,A |
| :--------- | ---: | ---: |
| Coral      | 5.26 | 0.05 |
| Movidius 1 | 5.22 | 0.30 |

![](img/energy-consumption-images-per-joule-coral-movidius-1.png) ![](img/energy-consumption-images-per-joule-coral-movidius-2.png)

*Figure 3.   Energy consumption in Images per Joule for Coral and Movidius 1.*

## Conclusions
According to the measurements results Movidius 1 is 4-6 times faster than Coral on tasks of single image classification.

But energy consumption in terms of images per Joule is very close for both Coral and Movidius 1.

Exceptions was Mobilenet V1 0.25 128 model - Coral allows to process about 200 images per Joule on this network, when Movidius 1 only 35.

Edge TPU on dev board is 1.4 - 2 times quicker than Coral connected to USB2.

Still there are problems with the neural network conversions between TF and Movidius format, but nevertheless, new implementation of OpenVINO (2019 R1) has better networks support. 

