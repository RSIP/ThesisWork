# ThesisWork
# Unsupervised Global To Local Nonrigid Image Registration Network Bidirectionally Reinforced By Joint Saliceny Map

## Abstract
- Missing correspondence and local large deformation bring in great challenges for both traditional and deep-learning based deformable image registration. It breaks the premise of one-to-one correspondence relationship and those problems are not well managed in traditional and recent deep learning based methods. To address this problem, we propose a novel global-to-local convolution neural network(CNN) to realize robust, unsupervised and fast registration simultaneously in one unified framework. Our contributions are two fold. (1)Based on the coarse estimation from the global network, the local network incrementally learns an adaptive regression function that corrects wrongly predicted residuals in coarse prediction. (2)To robustly address missing correspondence, we first introduce image joint saliency to bidirectional reinforce network’s forward estimation and back-propagation with uncertainty modeling and context-aware intelligence. Experiment results show that our unsupervised registration network attains comparable results with regard to traditional registration and deep learning based approaches.

- KEY WORDS: Non-Rigid Image Registration, Joint Saliency Map, Deep Learning, Deep Neural Network, Bidirectional reinforcement, Convolutional Neural Network, Global to Local

## Proposed Model
![Proposed Model](https://github.com/fedral/ThesisWork/raw/master/model.jpg)

- the architecture of our model:
	- (1)Global Prediction Network
		- initially estimates a coarse motion vector filed using global information from input images to be matched. 
	- (2)Joint Image Saliency Extraction
		- image joint saliency evaluates the certainty of pixelwise motion vector.
	- (3)Local Refinement Network
		- local refinement network learns a nonlinear regression function that adaptively corrects erroneous displacement vectors and preserve trustworthy motion vectors with the help of pixelwise certainty information pointed out by image joint saliency. 
		
## Experiment Result
- Datase : Mnist/Cadiac moving dataset(LVQU) 
- Training: GTX1080Ti,I7; Lasagne 02.dev/Theano 0.90; Ubuntu 14.04; Cudnn 5.0 + Cuda 8.0; Opt：Adam;
- Testing : Lasagne 02.dev/Theano 0.90; Tensorflow 0.12/Keras; Caffe;
## Training plot: 
		- ![Demo of JSM](https://github.com/fedral/ThesisWork/raw/master/training.jpg)
		- Adam default setting; Batch Size:8; Epoch Number：300; Initial Learning Rate: 0.0001; Split-Validation Ratio: 0.1; 
		- the convergence of training error and validation error shows no model over-fitting or under-fitting.
## Demo of JSM: 
![Demo of JSM](https://github.com/fedral/ThesisWork/raw/master/jsm.jpg)
- In forward prediction, the image joint saliency not only serves as an intermediate certainty map for current coarse prediction by emphasizing pixels where commonly salient image edge structures can be correctly aligned and suppressing outliers of missing correspondence and large deformation, but also provides spatial contextual cues for accurate prediction at the second local network. In back-propagation, additional back-propagation gradients for wrongly-predicted residual pixels are generated by joint saliency layer. Those residual gradients reinforce the improvement of the first global network.


## Comparsion state-of-art Methods:
   - traditional methods
		- [1] Ou, Yangming, et al. "DRAMMS: Deformable registration via attribute matching and mutual-saliency weighting." Medical image analysis 15.4 (2011): 622-639.
		- [2] Avants, Brian B., et al. "Symmetric diffeomorphic image registration with cross-correlation: evaluating automated labeling of elderly and neurodegenerative brain." Medical image analysis 12.1 (2008): 26-41.
		- [3] Vercauteren, Tom, et al. "Diffeomorphic demons: Efficient non-parametric image registration." NeuroImage 45.1 (2009): S61-S72.
   - latest deep-learning based unsupervised methods
		- [4] de Vos, Bob D., et al. "End-to-end unsupervised deformable image registration with a convolutional neural network." Deep Learning in Medical Image Analysis and Multimodal Learning for Clinical Decision Support. Springer, Cham, 2017. 204-212.
		- [5] Balakrishnan, Guha, et al. "An Unsupervised Learning Model for Deformable Medical Image Registration." Proceedings of the IEEE Conference on Computer Vision and Pattern Recognition. 2018.
- Quantitive Metric: mean/std of TRE(Targe Registration Error) of selected landmark pairs; 

![Comparison Result with satus quo both traditional and deep learning based image registration algorithms](https://github.com/fedral/ThesisWork/raw/master/errorplot.jpg)

Our method most robust and accurate result with the presence of iamge outliers such as missing correspondence and large local deformaities. 
The authors would like to thank Xue Wufeng for providing Cadiac dataset and open source image registration testing code. 

## Reference
1. Jaderberg, Max, Karen Simonyan, and Andrew Zisserman. "Spatial transformer networks." Advances in Neural Information Processing Systems. 2015.
2. Long, Jonathan, Evan Shelhamer, and Trevor Darrell. "Fully convolutional networks for semantic segmentation." Proceedings of the IEEE Conference on Computer Vision and Pattern Recognition. 2015.
3. Dosovitskiy, Alexey, et al. "Flownet: Learning optical flow with convolutional networks." Proceedings of the IEEE International Conference on Computer Vision. 2015.
4. Ilg, Eddy, et al. "Flownet 2.0: Evolution of optical flow estimation with deep networks." arXiv preprint arXiv:1612.01925 (2016).
5. Qin, Binjie, Shen Z, Fu Z,et al. Joint-saliency structure adaptive kernel regression with adaptive-scale kernels for deformable registration of challenging images[J]. IEEE Acce. 2018, 6: 330-343.
6. Xue, Wufeng, et al. "Full left ventricle quantification via deep multitask relationships learning." Medical image analysis 43 (2018): 54-65.

