# Machine Learning Model Architectures 
Model Selection: 

● Backbone CNNs

To establish a comprehensive performance baseline, we implemented a comparative 
framework encompassing both custom and pre-trained architectures. 
A Vanilla CNN with 12 convolutional neural networks is set up as the baseline model 
to evaluate other pretrained models, comprising four convolutional blocks 
(Conv2D-BatchNorm-ReLU-MaxPool), followed by two fully-connected layers. 


For transfer learning, three pre-trained models are applied with fine-tuning: 

● VGG-16 is chosen for its hierarchical feature extraction capability , which captures 
spatial patterns from local textures to global pathological structures. The input layers 
are reconfigured to accommodate single-channel OCT grayscale images while 
preserving spatial resolution(Tajbakhsh et al., 2016). The last four convolutional 
blocks are fine-tuned to adapt to OCT-specific features, while earlier layers remained 
frozen to preserve ImageNet-learned texture features.

● ResNet-50 is selected  to mitigate gradient vanishing through residual connections, 
ensuring stable training on limited OCT datasets. Its multi-task output layer employs 
adaptive loss weighting (classification-to-regression ratio 1:0.7), enabling 
simultaneous optimization of discrete diagnostic classes and continuous severity 
scores.

● InceptionV3 is selected for its ability to fuse multi-scale features through parallel 
convolutional pathways, enabling robust detection of variable-sized pathologies such 
as small drusen. It removes auxiliary classifiers to prevent gradient conflicts while 
retaining depthwise separable convolutions to maintain sensitivity of scale-invariant 
features ,which is critical for enhanced cross-device generalization. 

Collectively, these architectural choices form a strategic approach to enhance 
OCT analysis. By leveraging VGG-16’s strength in processing spatial 
hierarchies, ResNet-50’s stability in deep layer optimization, and 
InceptionV3’s capability for multi-scale feature fusion, this multi-model 
approach supports a robust evaluation of both specialized learning tasks and 
the general transfer of features for retinal disease diagnosis. 

● Layer Customization: Attention MechanismsIn order to enhance the clinical 
relevance of these pre-trained architectures, we introduce attention mechanisms 
after mid-level convolutional blocks to highlight pathological features such as fluid 
accumulation in DME,thereby ensuring that the networks focus on clinically 
significant regions within the images.  

● Output System: Dual-Branch Output Heads 
The classification head is further modified into a dual-output system:  
  ● Multi-class classification: The first output branch employs a multi-class 
Softmax classifier to categorize Optical Coherence Tomography (OCT) scans 
into 4 categories  (CNV, DME, Drusen, Normal)  

  ● Risk score regression : The second branch implements a regression-based 
risk scoring system that quantifies disease severity(0-10 scale) 
Explainability Framework: Grad-CAM-Based Visualizations 

To address the critical need for model interpretability in clinical deployment, we apply 
gradient-weighted class activation mapping (Grad-CAM), generating heat maps that 
visually localize decision-influencing regions on OCT scans. By overlaying these heat 
maps onto raw OCT images, the system highlights clinically plausible biomarkers , 
improving clinical trust and reliability.
