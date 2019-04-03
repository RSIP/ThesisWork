# ThesisWork
# Unsupervised Global To Local Nonrigid Image Registration Network Bidirectionally Reinforced By Joint Saliceny Map

## Abstract
- Deformable image registration estimates one-to-one correspondence for each pixel to build a dense displacement vector field between target image and moving image. In medical imaging, common physical reasons such as tumor recurrence as well as resection cavities and large mass effects[1-2] not only breaks the image registration’s premise of one-to-one pixels’ mapping relationship but also brings about large local image deformities in nearby regions, which make image registration extremely difficult. In past decades, numerous conventional deformable image registration methods have emerged. At present, image registration problem with missing correspondence and large local distortion is still not well addressed by conventional registration approaches. Both feature-based and intensity-based methods still lack of robust performance and often arise spurious matching in those image outlier regions. In feature-based registration methods, to address the image outliers during pixel matching, Chui[3] proposes a fuzzy softassign strategy to regularize missing outliers and compensate one-to-one correspondence. CPD[4] constrains deformation field to be moving coherently and utilizes probabilistic Gaussian mixture model during feature matching. [5] introduces a graph structure during image registration and exploits topological information from neighbouring nodes to suppress negative influence of image outliers. Although those methods have robustly addressed missing correspondence issue, they still suffer from feature matching ambiguity caused by large local deformations. While in intensity-based methods, image registration is formed as energy function consisting a similarity term and an motion regularization term. [6] adopt an expectation and maximization algorithm to estimate correspondence field robustly based on partial pixels’ information. [7-8] designs an intensity-driven trading weight between image similarity and motion regularization. But over smooth and inaccurate pixels’ mappings are observed in nearby regions of missing correspondence and large image distortion. Other intensity-based methods turn to a joint segmentation and registration trick by using beforehand segmentation to curb the vicious influences from image regions with missing tissues and large distortion during registration. In CT-guided surgery, Nithiananthan et.al [9] used iterative segmentation step to identify and regularize tumor excised regions’ influence on following Demons based image registration. Nicha et.al[10] present a joint registration and segmentation framework to handle missing correspondence problem, in which segmentation is used to separating valid and missing correspondence during transformation estimation. Similarly, Berendsen et.al[11] purposedly designed a surface mesh penalty function based on pre-segmented image contour to accurate align cervical MR images for brachytherapy. Nevertheless, image segmentation in itself is an unaffordable workload that not only requires exhausting algorithm crafting but also puts additional computational burden on deformable registration algorithms which are already time-consuming in real practices.

- KEY WORDS: Non-Rigid Image Registration, Joint Saliency Map, Deep Learning, Deep Neural Network, Bidirectional reinforcement, Convolutional Neural Network, Global to Local

## Proposed Model
![Proposed Model](https://github.com/fedral/ThesisWork/raw/master/model.jpg)

- the architecture of our model:
	- (1)Global Prediction Network
		- initially estimates a coarse motion vector filed using global information from input images to be matched. 
	- (2)Joint Image Saliency Extraction}
		- image joint saliency evaluates the certainty of pixelwise motion vector.
	- (3)Local Refinement Network
		- local refinement network learns a nonlinear regression function that adaptively corrects erroneous displacement vectors and preserve trustworthy motion vectors with the help of pixelwise certainty information pointed out by image joint saliency. 
		
## Tesing Result
- Datase : Mnist/LVQU(heart moving frames) 
- Training: GTX1080Ti,I7; Lasagne 02.dev/Theano 0.90; Ubuntu 14.04; Cudnn 5.0 + Cuda 8.0
- Testing : Lasagne 02.dev/Theano 0.90; Tensorflow 0.12/Keras; Caffe;
- Comparsion state-of-art Methods:
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

## Reference
1. Jaderberg, Max, Karen Simonyan, and Andrew Zisserman. "Spatial transformer networks." Advances in Neural Information Processing Systems. 2015.
2. Long, Jonathan, Evan Shelhamer, and Trevor Darrell. "Fully convolutional networks for semantic segmentation." Proceedings of the IEEE Conference on Computer Vision and Pattern Recognition. 2015.
3. Dosovitskiy, Alexey, et al. "Flownet: Learning optical flow with convolutional networks." Proceedings of the IEEE International Conference on Computer Vision. 2015.
4. Ilg, Eddy, et al. "Flownet 2.0: Evolution of optical flow estimation with deep networks." arXiv preprint arXiv:1612.01925 (2016).
5. Qin, Binjie, Shen Z, Fu Z,et al. Joint-saliency structure adaptive kernel regression with adaptive-scale kernels for deformable registration of challenging images[J]. IEEE Acce. 2018, 6: 330-343.

