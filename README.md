# ThesisWork
# Unsupervised Global To Local Nonrigid Image Registration Network Bidirectionally Reinforced By Joint Saliceny Map

## Abstract
### After decades of scientific development, non-rigid image registration is becoming an indispensible image processing tool for many research areas such as life science, medical imaging, motion analysis and pattern recognition. On the one hand, with rapid development of imaging technologies and upgrading devices, the surging of large scale, high-dimensional images with rich structural and functional information has to cope with the large computational cost of image registration. On the other hand, due to common reasons like biological tissue motion, tumor development and outside physical factors, the images to be registered often contain outliers such as missing correspondences and large local deformations, which greatly challenge deformable image registration in making the balance between accuracy and robustness. 

### To address the missing correspondences and large local deformations in an accurate, robust and fast manner, we propose an unsupervised deformable image registration deep neural network that firstly predict a global deformation field and then elevate the accuracy of global prediction with local regression. Registration deep network aims to learn the pixelwise mapping between moving image and target image while this mapping function is too complicated by the outliers to be learned in the deep neural network. In our work, we take a "divide and conquer" tactics that decompose the original complex mapping into two solvable sub-mappings: a first global prediction network learns the mapping form input images to coarse motion field, and a subsequent local regression network is to accurately recover true motion field from coarse deformation prediction.

### To curb the vicious deformations at the outlier regions, we further introduce a joint saliency map based bidirectional reinforcement mechanism into the registration network. Taking full advantage of consistency relationship between images’ structural context and deformation fields indicated by joint saliency map, the proposed network focuses more on correctly-aligned joint salient pixels and suppresses the vicious impact from erroneously registered pixels and outlier pixels with missing correspondences. Differentiable joint saliency map not only bidirectionally reinforces the whole network’s cooperative training by providing image contextual guidance for forward prediction of local regression network and generating backward feedback gradients basing on image alignment residual error to improve the global prediction network’s learning, but also prompt fast convergence to accurate and robust deformable registration results at both global and local estimation. 

### Experiment results demonstrate that the proposed unsupervised global to local deformable registration network bidirectionally reinforced by joint saliency map is able to tackle with difficult deformable registration problem with missing correspondences and large local deformations in an accurate, robust and fast manner. Compared with several state-of-art traditional and deep learning based registration methods, our method achieved best in both visual evaluation and landmark-based quantitative evaluation and the running time is reduced to 0.01~0.2 second in 2D image registration.    

- KEY WORDS: Non-Rigid Image Registration, Joint Saliency Map, Deep Learning, Deep Neural Network, Bidirectional reinforcement, Convolutional Neural Network, Global to Local

## Proposed Model
![Proposed Model](https://github.com/fedral/ThesisWork/raw/master/model.jpg)

the architecture of our model:
	(1) [x] Global Prediction Network
		- initially estimates a coarse motion vector filed using global information from input images to be matched. 
	(2) [x]Joint Image Saliency Extraction}
		- Closely working with our global to local network, joint saliency bidirectionally reinforces the whole network performance during forward estimation and back-propagation. In forward prediction, the image joint saliency not only serves as an intermediate certainty map for current coarse prediction by emphasizing pixels where commonly salient image edge structures can be correctly aligned and suppressing outliers of missing correspondence and large deformation, but also provides spatial contextual cues for accurate prediction at the second local network. In back-propagation, additional back-propagation gradients for wrongly-predicted residual pixels are generated by joint saliency layer. Those residual gradients reinforce the improvement of the first global network.
		- Given a coarse motion field from global network, image joint saliency evaluates the certainty of pixelwise motion vector. Joint saliency value is defined by pixel’s local edge structures similarity between target image and deformed moving image. Correctly aligned pixels with commonly salient edge structures are given higher weights, while erroneously registered pixels and inconsistent outliers are suppressed to small value. Joint saliency explicitly tells good predictions apart from pixels with difficult registration like local large deformation and vicious outliers like missing correspondence. As a image context information for intermediate coarse motion prediction, joint saliency is also inputted to the following local refinement network shown in Figure $1$. Since image joint saliency extraction is a differentiable algebra operation, we implemented joint saliency extraction[36-38] as a layer based on Lasagne[28] to render end-to-end unsupervised training of whole network.
	(3) [x] Local Refinement Network
		- To elevate prediction accuracy upon the coarse prediction from global network, the local refinement network learns a nonlinear regression function that adaptively corrects erroneous displacement vectors and preserve trustworthy motion vectors with the help of pixelwise certainty information pointed out by image joint saliency. The coarse motion field is concatenated axially with its image joint saliency before inputting local refinement CNN. 
		- The local refinement network composed by four convolution layers shows two novel features. On one hand, by properly setting four convolution layers’ kernel size, the local network provides a large receptive field for local adaptive regression over input coarse motion field. On the other hand, kernel shape and scale in traditional regression are delicately crafted, while our learning based local network is able to learn flexible kernels with arbitrary shapes and scales.  

## Tesing Result
- Training: GTX1080Ti,I7; Lasagne 02.dev/Theano 0.90; Ubuntu 14.04; Cudnn 5.0 + Cuda 8.0
- Testing : Lasagne 02.dev/Theano 0.90; Tensorflow 0.12/Keras; Caffe;
- Comparsion state-of-art Methods:
   (a) traditional methods
		- [1] Ou, Yangming, et al. "DRAMMS: Deformable registration via attribute matching and mutual-saliency weighting." Medical image analysis 15.4 (2011): 622-639.
		- [2] Avants, Brian B., et al. "Symmetric diffeomorphic image registration with cross-correlation: evaluating automated labeling of elderly and neurodegenerative brain." Medical image analysis 12.1 (2008): 26-41.
		- [3] Vercauteren, Tom, et al. "Diffeomorphic demons: Efficient non-parametric image registration." NeuroImage 45.1 (2009): S61-S72.
   (b) latest deep-learning based unsupervised methods
		- [4] de Vos, Bob D., et al. "End-to-end unsupervised deformable image registration with a convolutional neural network." Deep Learning in Medical Image Analysis and Multimodal Learning for Clinical Decision Support. Springer, Cham, 2017. 204-212.
		- [5] Balakrishnan, Guha, et al. "An Unsupervised Learning Model for Deformable Medical Image Registration." Proceedings of the IEEE Conference on Computer Vision and Pattern Recognition. 2018.
- Quantitive Metric: mean/std of TRE(Targe Registration Error) of selected landmark pairs; 

![Comparison Result with satus quo both traditional and deep learning based image registration algorithms](https://github.com/fedral/ThesisWork/raw/master/errorplot.jpg)

Our method most robust and accurate result with the presence of iamge outliers such as missing correspondence and large local deformaities. 

## Reference
1. Jaderberg, Max, Karen Simonyan, and Andrew Zisserman. "Spatial transformer networks." Advances in Neural Information Processing Systems. 2015.
2. Long, Jonathan, Evan Shelhamer, and Trevor Darrell. "Fully convolutional networks for semantic segmentation." Proceedings of the IEEE Conference on Computer Vision and Pattern Recognition. 2015.
3. Dosovitskiy, Alexey, et al. "Flownet: Learning optical flow with convolutional networks." Proceedings of the IEEE International Conference on Computer Vision. 2015.
4. Ilg, Eddy, et al. "Flownet 2.0: Evolution of optical flow estimation with deep networks." arXiv preprint arXiv:1612.01925 (2016).
5. Qin, Binjie, Shen Z, Fu Z,et al. Joint-saliency structure adaptive kernel regression with adaptive-scale kernels for deformable registration of challenging images[J]. IEEE Acce. 2018, 6: 330-343.

