1. Structural Re-parameterization
   ![[attchments/Pasted image 20230704114613.png|500]]
   (RepVGG)将卷积和BN层融合，构造3\*3卷积，再将3\*3卷积融合成一个，同时将参数也融合。
   训练时并行，推理时融合。
   在RepLKNet中，使用31的大核和5的小核(+BN)融合。
   
2. ResNeXt
   ![[Pasted image 20230704215152.png|]]
   使用Group Convolution ，把输入特征图按通道分成*g*个组，在每个组内分别应用卷积核卷积，卷积核通道数=每组含的通道数，每组卷积核个数=输出通道数/g，最后在通道维度拼接。
   
3. ConvNeXt
   ![[Pasted image 20230704204612.png|600]]
   ![[Pasted image 20230704210800.png|600]]
> Our starting point is a ResNet-50 model. We first train it with similar training techniques used to train vision Transformers.

- Marco design
	- Changing stage compute ratio;
	- Changing stem to "Patchify".
- ResNeXt-fy
	使用group卷积，但使group数和输入通道数相同，成为depth-wise卷积
>We note that depthwise convolution is similar to the weighted sum operation in self-attention.
- Inverted Bottleneck
	两头维度大，中间维度小
	即 dim -> 4\*dim -> dim
- Large Kernel Sizes
	- Moving up depthwise conv layer;
		由于Transformer中MSA在MLP之前
	- Increasing the kernel size.
		3\*3 -> 7\*7
- Micro design
	- Replacing ReLU with GELU;
	- Fewer activation functions;
	- Fewer normalization layers;
	- Substituting BN with LN;
	- Separate downsampling layers.
		ResNet的下采样是在Stage内的主分支和捷径分支上做的
  
4. RepLKNet
 
5. SLaK
   

   
