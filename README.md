# BrainTumorSegmentation-
WEB APP for Brain Tumor Segmentation into gliomas, pituitary, meningioma, and tumor free using CNN
1.Abstract
The diagnosis of brain tumors traditionally involves invasive procedures like biopsy, often performed during definitive brain surgery. Advances in technology and machine learning offer a non-invasive alternative to aid radiologists in tumor diagnostics. Among machine learning algorithms, Convolutional Neural Networks (CNNs) have demonstrated significant success in image segmentation and classification. In this study, we introduce a novel CNN architecture designed for the classification of three types of brain tumors using T1-weighted contrast-enhanced magnetic resonance images.
Distinguishing itself from existing pre-trained networks, our developed CNN architecture prioritizes simplicity while maintaining efficacy. The network's performance was systematically assessed through four approaches, involving combinations of two 10-fold cross-validation methods and two databases. To gauge the network's generalization capability, subject-wise cross-validation was employed, and augmentation of the image database was explored to test for improvements.
The most notable outcome was achieved with record-wise cross-validation for the augmented dataset using the 10-fold method, yielding an impressive accuracy of 96.7%. The developed CNN architecture showcased not only high accuracy but also exhibited good generalization capability. Furthermore, its efficient execution speed positions it as a potentially effective decision-support tool for radiologists in medical diagnostics.
This research highlights the promise of leveraging machine learning, particularly CNNs, in the non-invasive classification of brain tumors. The presented CNN architecture stands out for its simplicity, robust performance, and potential as a valuable tool in the medical diagnostic process.



2. Introduction
Cancer stands as the second leading cause of global mortality, emphasizing the critical need for early detection to prevent fatalities. Tumors, whether benign, pre-carcinoma, or malignant, necessitate distinct diagnostic approaches. Unlike malignant tumors, benign tumors are typically non-spreading and surgically removable. Within the realm of primary brain tumors, gliomas, meningiomas, and pituitary tumors hold significance. Gliomas originate from brain tissues other than nerve cells and blood vessels, while meningiomas arise from membranes covering the brain, and pituitary tumors manifest as lumps within the skull. Accurate differentiation among these tumor types is pivotal for effective clinical diagnostics.

Magnetic Resonance Imaging (MRI) serves as the primary method for tumor type differential diagnostics. However, its susceptibility to subjectivity and the challenge of processing vast datasets hinder human observation. Early brain tumor detection heavily relies on radiologist experience, and a comprehensive diagnosis often involves invasive procedures like biopsies performed during brain surgery. To address these challenges and enhance diagnostics, there is a crucial need for an effective tool utilizing artificial intelligence and machine learning for tumor segmentation and classification from MRI images.

The evolution of technology, particularly artificial intelligence and machine learning, has significantly impacted the medical field, providing valuable support for imaging in various medical branches. The Multimodal Brain Tumor Segmentation Challenge (BRATS) has been a notable platform for evaluating machine learning algorithms for brain tumor classification. However, existing databases are often limited in size, containing approximately 285 images on average, and may not encompass diverse tumor levels.

This study delves into a novel Convolutional Neural Network (CNN) architecture for classifying three brain tumor types—meningioma, glioma, and pituitary tumor—utilizing T1-weighted contrast-enhanced MRI images. Unlike more complex architectures, the developed CNN prioritizes simplicity without compromising efficacy. Evaluations were conducted using four approaches involving two 10-fold cross-validation methods and two databases—original and augmented. The study emphasizes the importance of a simpler network, requiring fewer resources for training and implementation, essential for clinical diagnostics and mobile platforms. The research underscores the CNN's generalization capability for clinical studies, employing a subject-wise cross-validation approach for realistic results.

This comprehensive investigation contributes a new CNN architecture for brain tumor classification, navigating the challenges posed by imbalanced databases and emphasizing resource-efficient solutions. The results, presented through confusion matrices and accuracy metrics, are compared with state-of-the-art methods, providing valuable insights into the effectiveness of the proposed CNN architecture in brain tumor classification.


3.1. Dataset and Preprocessing
The research utilized a publicly available CE-MRI dataset collected from Nanfang Hospital Guangzhou China and General Hospital Tianjin Medical University in China. The dataset comprises 3062 MRI images from 233 patients with three types of BTs: gliomas (1426), meningiomas (708), and pituitary tumors (930).The image dataset utilized in this study comprises a collection from 233 distinct patients, capturing images across three planes: sagittal (1025 images), axial (994 images), and coronal (1045 images). This multidimensional dataset ensures a comprehensive representation of brain tumor images, providing valuable insights into tumor characteristics and enabling a robust evaluation of the proposed Convolutional Neural Network (CNN) architecture's performance. The images, in 2D volumes with a resolution of 512 × 512 and a pixel size of 0.49 × 0.49 mm², were manually annotated by experienced radiologists. The dataset was preprocessed by normalizing the MRI images, converting them to .jpg format, and resizing to 224 × 224 pixels. 
fig 1.

3.2. Image pre processing and data augmentation
The magnetic resonance images sourced from the database exhibited variations in sizes and were originally formatted in int16. As these images serve as the input layer for the network, a crucial pre-processing step involved normalizing and resizing them to a uniform dimension of 256 × 256 pixels.

To further enrich the dataset, two distinct transformations were applied to each image. Firstly, an augmentation involved rotating the images by 90 degrees. Secondly, a vertical flipping transformation was applied [23]. Through these augmentation techniques, the dataset was effectively expanded threefold, culminating in a total of 9192 images. This augmentation process enhances the diversity of the dataset, contributing to a more robust and effective training of the neural network.

Figure 2. Architecture of proposed hybrid model.

 3.3.Training Network
The training of the network utilized a k-fold cross-validation method, employing two distinct approaches, each involving a 10-fold cross-validation. The first approach, termed record-wise cross-validation, randomly partitioned the data into 10 roughly equal subsets, ensuring an equal representation of each tumor category in each subset. The second approach, subject-wise cross-validation, randomly divided the data into 10 portions, with each set exclusively containing data from a couple of subjects, regardless of the tumor class. This approach aimed to evaluate the network's generalization capability in medical diagnostics, assessing its effectiveness in predicting diagnoses based on data from subjects not observed during training.

To compare the network's performance with other state-of-the-art methods, a test without k-fold cross-validation (one test) was also conducted. In all the mentioned methods, two data portions were allocated for testing, two for validation, and six for training. Both the normal and augmented datasets underwent testing using all the methods.

The network's training employed an Adam optimizer with a mini-batch size of 16, incorporating data shuffling in each iteration. The early-stop condition, determining when the training process concludes, was set to one epoch, stopping when the loss began to increase. A regularization factor of 0.004 and an initial learning rate of 0.0004 were specified. The weights of the convolutional layers were initialized using the Glorot initializer, also known as the Xavier initializer [23]. I stopped training stopped when the loss on validation set got larger than or was equal to the previous lowest loss over 11 times. This training was done on a system with a single CUDA GPU- Geforce RTX 2060.

4. Results:
The results of the developed CNN are presented in Table 2, and visual representations are provided through confusion matrices in Figures 3 and 5–7. In the confusion matrices, non-white rows depict network output classes, while non-white columns correspond to real classes in Figures 3 and 5–7. The diagonal entries display the numbers/percentages of correctly classified images. The last row indicates sensitivity, while the last column corresponds to specificity. The overall accuracy is presented in the bottom-right field. The upper number in the non-white boxes indicates the number of images, and the lower number represents the percentage of the entire class database in the training or test set. To address class imbalance in the database, mean average precision, recall, and F1-score are also provided:

Results from testing the network with 10-fold cross-validation 
5. Conclusion and Improvements:
This study introduced a novel CNN architecture for brain tumor classification, utilizing a T1-weighted contrast-enhanced MRI image database encompassing three tumor types. The classification involves whole images, eliminating the need for preprocessing or tumor segmentation. The designed neural network is more straightforward than pre-trained networks, making it executable on standard personal computers with significantly fewer resources required for both training and implementation. The significance of developing smaller networks is underscored by the potential deployment on mobile platforms, particularly crucial for diagnostics in developing countries . Moreover, the network demonstrates an impressive execution speed.

To assess the network's performance, we employed both record-wise and subject-wise 10-fold cross-validation on both the original and augmented image databases. In clinical diagnostics, generalization capability entails predicting outcomes for subjects with no prior observations. To ensure robust evaluation, we adhered to subject-wise cross-validation, preventing observations from the training set from appearing in the test set. This approach guards against unrealistically high prediction accuracy resulting from a confounding dependency between patient identity and diagnosis [26].

Comparing with analogous state-of-the-art methods, our network exhibits superior performance. The record-wise 10-fold cross-validation method on the augmented dataset yielded the best result, achieving an accuracy of 96.7%. Notably, there is a dearth of literature showcasing tested generalization, particularly through subject-wise k-fold methods, for this specific image database. For the subject-wise approach, we attained an accuracy of 88.48% on the augmented dataset. The average test execution time was under 45 ms per image. These findings affirm the network's robust generalization capability and swift execution speed, positioning it as an effective decision-support tool for radiologists in medical diagnostics.
For future work, experimenting with the dataset with a small number of malignant brain MRI images and a significant number of normal brain MRIs should be performed, as the proposed model extracted more detailed, discriminative, and accurate features.
An essential enhancement for future iterations involves adapting the network architecture for application during brain surgery, facilitating the accurate classification and localization of tumors. The imperative in this context is real-time detection under authentic surgical conditions. Consequently, a significant improvement would encompass the adjustment of the network to operate in a 3D system, aligning with the demands of surgical environments. The strategic simplicity embedded in the network's architecture serves as a pivotal factor for enabling real-time detection. In subsequent investigations, we plan to assess the performance of our neural network design, along with potential refinements, across diverse medical images.





References:


Zhao, L.; Jia, K. Multiscale CNNs for brain tumors segmentation and diagnosis. Comput. Math. Methods Med. 2016,
Saddique, M.; Kazmi, J.H.; Qureshi, K. A hybrid approach of using symmetry technique for brain tumors. Comput. Math. Methods Med. 2014
Shree, N.V.; Kumar, T.N. Identification and classification of BTMRI images with feature extraction using DWT and probabilistic neural network. Brain Inform. 2018,
Komninos, J.; Vlassopoulou, V.; Protopapa, D.; Korfias, S.; Kontogeorgos, G.; Sakas, D.E.; Thalassinos, N.C. Tumors metastatic to the pituitary gland: Case report and literature review. 
J. Clin. Endocrinol. Metab. 2004,
Rehman, A.; Naz, S.; Razzak, M.I.; Akram, F.; Imran, M. A deep learning-based framework for automatic brain tumors classification using transfer learning. Circuits Syst. Signal Process. 2020
A Hybrid Deep Learning-Based Approach for Brain Tumor Classification by Asaf Raza, Huma Ayub,Javed Ali- https://www.mdpi.com/2079-9292/11/7/1146
DeAngelis, L.M. Brain tumors. N. Engl. J. Med. 2001,.
Sajjad, M.; Khan, S.; Muhammad, K.; Wu, W.; Ullah, A.; Baik, S.W. Multi-grade brain tumors classification using deep CNN with extensive data augmentation. J. Comput. Sci. 2019,
Kharrat, A.; Neji, M. Feature selection based on hybrid optimization for magnetic resonance imaging brain tumor classification and segmentation. Appl. Med. Inform. 2019
Rehman, A.; Naz, S.; Razzak, M.I.; Akram, F.; Imran, M. A deep learning-based framework for automatic brain tumors classification using transfer learning. Circuits Syst. Signal Process. 2020 
Anaraki, A.K.; Ayati, M.; Kazemi, F. Magnetic resonance imaging-based brain tumor grades classification and grading via convolutional neural networks and genetic algorithms. Biocybern. Biomed. Eng. 2019, 
Howard, A.G.; Zhu, M.; Chen, B.; Kalenichenko, D.; Wang, W.; Weyand, T.; Andreetto, M.; Adam, H. Mobilenets: Efficient convolutional neural networks for mobile vision applications. arXiv 2017
Ramamurthy, D.; Mahesh, P.K. Whale Harris Hawks optimization-based deep learning classifier for brain tumors detection using MRI images. J. King Saud Univ. Comput. Inf. Sci. 2020
Wang, Y.; Zu, C.; Hu, G.; Luo, Y.; Ma, Z.; He, K.; Wu, X.; Zhou, J. Automatic tumor segmentation with deep convolutional neural networks for radiotherapy applications. Neural Process. Lett. 2018 
Cheng, J.; Huang, W.; Cao, S.; Yang, R.; Yang, W.; Yun, Z.; Wang, Z.; Feng, Q. Enhanced performance of brain tumors classification via tumor region augmentation and partition. PLoS ONE 2015, 
Jégou, S.; Drozdzal, M.; Vazquez, D.; Romero, A.; Bengio, Y. The one hundred layers tiramisu: Fully convolutional denseness for semantic segmentation. In Proceedings of the IEEE Conference on Computer Vision and Pattern Recognition Workshops, Honolulu, HI, USA, 21–26 July 2017
Zhang, Q.; Cui, Z.; Niu, X.; Geng, S.; Qiao, Y. Image segmentation with pyramid dilated convolution based on ResNet and U-Net. In Proceedings of the International Conference on Neural Information Processing, Guangzhou, China, 14 November 2017 
Szegedy, C.; Vanhoucke, V.; Ioffe, S.; Shlens, J.; Wojna, Z. Rethinking the inception architecture for computer vision. In Proceedings of the IEEE Conference on Computer Vision and Pattern Recognition, Las Vegas, NV, USA, 26 June–1 July 2016
Ding, Y.; Zhang, C.; Lan, T.; Qin, Z.; Zhang, X.; Wang, W. Classification of Alzheimer’s disease based on the combination of morphometric feature and texture feature. In Proceedings of the 2015
Ijaz, A.; Ullah, I.; Khan, W.U.; Ur Rehman, A.; Adrees, M.S.; Saleem, M.Q.; Cheikhrouhou, O.; Hamam, H.; Shafiq, M. Efficient algorithms for E-healthcare to solve multiobject fuse detection problem. J. Healthc. Eng. 2021
