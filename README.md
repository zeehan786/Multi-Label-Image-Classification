# Multi-Label-Image-Classification
Using Transfer Learning to classify upto 5 classes

Methodology:

The data are heavily imbalanced. For example, there are 1994 images of person present in the training
53 data. However, about one tenth of images pertains to the animal "cow". We test this imbalance data
54 using a CNN built from scratch with about 21 million parameters with dataset comprimising on
55 person, aeroplane, bicycle, car, cat and car. We see a accuracy of 70 percent in traning. However,
56 when evaluating the model on a test data comprimising of images containing only the person, the
57 accuracy reaches near 100 percent. Interestingly, the accuracy barely touches 10 percent when the
58 test images contains everything but person.
59 This explains an important concept in the field of machine learning. The model has learnt the features
60 of humans very well as the input data is heavily skewed towards person. Therefore, it performs
61 exceptionally well in recognizing person given an image. However, since the number of images
62 for other classes are comparatively low than the person class, the model fails to capture the unique
63 features (patterns) of the other four classes. Reading several articles, I realized class imbalance is a
64 common problem in multilabel image classification. Articles [3] demonstrates some promising ways
65 to tackle the issue by using different performance metric and using data augmentation.
66 However, since the project requires only 5 classes in the multilabel problem, I decided to choose
67 those 5 classes that are about the same in numbers. I also made sure to pick the classes that are
68 high in number. This way the model can have as many data to be trained with. These classes were
69 bird(395),car(590), cat(539), chair(566), and dog(632). Running the model with the same architecture,
70 caused the accuracy score to go down to 10 percent during training. As a first instinct I suspected
71 the model with 21 million parameters might not be too simple for a complex data. Therefore, I
72 bumped the parameters to about 768 million parameters by decreasing the strides in all layers, and
73 significantly increase the neurons in the dense layers. My attempt to intentionally overfit the data
74 failed as the accuracy score remained almost the same. I also employed intense hyperparameter tuning
75 like chaning the activation function from relu to tanh, selu or using a different weight initialization
2
76 like "he-initializer" (as i suspected the expoding/vanishing gradient problem might be the issue).
77 However, the accuracy score did not show any significant improvements. Using data augmentaion
78 might have made the problem more worse, as the model stuggled to fit with the current data.
79 I suspected the data might be still unbalanced as the number of images pertaining to the five chosen
80 classes comprimised of about 2500 images while the remaining half of the training images consisted
81 of images not containing any of the chosen five classes. In order to fix the heavy imbalance, I
82 performed downsampling of the data by incorporating only 260 (almost equal to the frequency of
83 bird class) images that did not consist any of the chosen five classes. The change resulted in a 20
84 percent overall accuracy score. (Note: I decided to stick with the accuracy metric instead of precison,
85 recall or f1-score as the frequency of the five classes were almost the same (balanced dataset). After
86 doing the necessary preprocessing and gaining a mere 20 percent in the accuracy, I suspected the
87 CNN created from ground up might be flawed in harvesting the essential features of the input images.
88 Therefore, I decided to rely on pretrained models and did some study on transfer learning[4].
89 Many pretrained models were studied to choose the most ideal pretrained model. Upon research
90 Xception model was selected for the problem. Firstly, Xception consisted of the inception module
91 used by GoogleNet. The inception module enabled GoogleNet to make efficient use of parameters.
92 Moreover, it had 10 times fewer parameters than AlexNet. The inception module has four different
93 branch. Each branch with different sizes of filters captures patterns at different scales. Moreover, the
94 module also consist of 1X1 kernels. Even though these pixels cannot detect features as they study
95 only pixel at a time, they can capture patterns in the depth dimension of the feature maps. Using these
96 unit size kernels also reduces number of parameters. Contrary to a linear fashioned CNN, model
97 incorporating the inception module is able to run different pairs of filters across the input capturing
98 more complex patterns.
