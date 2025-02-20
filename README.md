## Project Overview

It is a project focused on the classification of Alzheimer's disease using advanced AI techniques and brain MRI (Magnetic Resonance Imaging) images. The goal of the project is to develop an accurate and robust model that can assist in the early detection and diagnosis of Alzheimer's disease.

## Objective

The objective of the project is to leverage AI techniques and machine learning algorithms to classify brain MRI images into different stages of Alzheimer's disease. By accurately identifying the disease's progression, the model can aid healthcare professionals in making timely diagnoses and developing appropriate treatment plans.

The specific objectives of the project are as follows:

1. Preprocess the MRI images to enhance their quality, remove noise, and standardize the data.

2. Develop and train deep learning models using TensorFlow and Keras to accurately classify MRI images into different stages of Alzheimer's disease. Optimize and fine-tune the models to achieve high classification accuracy, precision, recall, and other performance metrics.

3. Evaluate the trained models using appropriate evaluation metrics and compare their performance to identify the most effective model.

4. Visualize the results, including the MRI images, model predictions, and evaluation metrics, to facilitate interpretation and analysis. Create a comprehensive report summarizing the project, including the methodology, results, limitations, and potential areas for further improvement.

## Dataset: Alzheimer MRI Preprocessed Dataset


The project utilizes the [Alzheimer MRI Preprocessed Dataset](https://www.kaggle.com/datasets/sachinkumar413/alzheimer-mri-dataset) obtained from Kaggle. The dataset consists of 6400 preprocessed MRI images, resized to 128 x 128 pixels, representing different stages of Alzheimer's disease.

### Dataset Details

- Total Images: 6400
- Classes:
  - Class 1: Mild Demented (896 images)
  - Class 2: Moderate Demented (64 images)
  - Class 3: Non Demented (3200 images)
  - Class 4: Very Mild Demented (2240 images)


## Technologies Used

- TensorFlow: An open-source machine learning framework used for building and training deep learning models.
- Keras: A high-level neural networks API that runs on top of TensorFlow. It provides an intuitive interface for designing and training models.
- Pandas: A powerful data manipulation library used for data preprocessing and analysis.
- Matplotlib: A popular plotting library used for data visualization, including the visualization of MRI images and performance metrics.
- NumPy: A fundamental library for scientific computing in Python, used for numerical operations and array manipulation.
- Scikit-learn: A machine learning library that provides tools for data preprocessing, model evaluation, and performance metrics.

## Data Preprocessing and Augmentation

In the initial steps of the project, the dataset of Alzheimer's disease brain MRI images undergoes preprocessing and augmentation to enhance the data quality and increase the robustness of the model. The following steps are performed:

- Splitting the Dataset: The original dataset, obtained from Kaggle, is split into train, validation, and test sets.
- Image Preprocessing: The images are resized to 128 x 128 pixels.
- Data Augmentation: The training data is augmented using techniques such as rescaling, shearing, and zooming to increase its diversity and improve the model's ability to generalize.
- Data Normalization: The validation and test data are rescaled for normalization.
- Directory Setup: Directories are set up to specify the location of the split images for the train, validation, and test sets.
- ImageDataGenerators: The Keras `ImageDataGenerator` is used to generate batches of augmented images for the training set and normalized images for the validation and test sets.
- Class Mode: The class mode is set to 'categorical' to support multi-class classification.

These steps ensure that the dataset is properly prepared for training and evaluating deep learning models for the classification of Alzheimer's disease using brain MRI images.

Please refer to the code provided for more details on the implementation.

```python
import splitfolders
from keras.preprocessing.image import ImageDataGenerator
# Set the path of the directory containing the original images
input_folder = '/kaggle/input/alzheimer-mri-dataset/Dataset'
output_folder = '/kaggle/working/Splitted'
train_ratio = 0.8
validation_ratio = 0.1
test_ratio = 0.1
# Split the images into train-validation-test sets
splitfolders.ratio(input_folder, output_folder, seed=42, ratio=(train_ratio, validation_ratio, test_ratio))
# Define the ImageDataGenerators for data augmentation and normalization
train_datagen = ImageDataGenerator(rescale=1./255, shear_range=0.2, zoom_range=0.2)
validation_datagen = ImageDataGenerator(rescale=1./255)
test_datagen = ImageDataGenerator(rescale=1./255)
# Set the directories for train, validation, and test sets
train_dir = '/kaggle/working/Splitted/train'
validation_dir = '/kaggle/working/Splitted/val'
test_dir = '/kaggle/working/Splitted/test'
# Create generators for train, validation, and test sets
train_generator = train_datagen.flow_from_directory(train_dir, target_size=(128, 128), shuffle=True, seed=SEED, batch_size=64, class_mode='categorical')
validation_generator = validation_datagen.flow_from_directory(validation_dir, target_size=(128, 128), seed=SEED, shuffle=True, batch_size=64, class_mode='categorical')
test_generator = test_datagen.flow_from_directory(test_dir, target_size=(128, 128), shuffle=True, seed=SEED, batch_size=64, class_mode='categorical')
```


## AI Models Used

The project incorporates the following AI models for Alzheimer's disease classification:

### 1. CNN Models

The project utilizes various CNN models for classification:

- Custom CNN architecture
- CNN (Convolutional Neural Network) 

### 2. Transfer Learning Models

The project employs transfer learning using pre-trained models:


- VGG16: 
- VGG19: 
- ResNet: 
- MobileNetV2:
- InceptionV3: 
- DenseNet169: 
- EfficientNetb0: 

### 3. Machine Learning Models

The project includes traditional machine learning algorithms for classification:

- Logistic Regression
- SVM (Support Vector Machine)
- Random Forest

### 4. Hybrid Deep Learning Models

The project implements hybrid deep learning models combining deep learning with other algorithms:

- Alzheimer-CNN-with-XGBoost-GNB-SVM: A hybrid model combining CNN with XGBoost, Gaussian Naive Bayes (GNB), and SVM algorithms.

- Alzheimer-VGG-with-SVM-GNB-XGBoost: A hybrid model combining VGG16 with SVM, GNB, and XGBoost algorithms. 

## Model Performances

The following table shows the evaluation metrics for different models used in the HealthCoder project:

### Transfer Learning and Conventional CNN

| Model       | Test Loss | Test Accuracy | Test AUC | Test Precision | Test Recall |
|-------------|-----------|---------------|----------|----------------|-------------|
| VGG16       | 0.193     | 0.927         | 0.993    | 0.928          | 0.924       |
| VGG19       | 0.279     | 0.897         | 0.986    | 0.898          | 0.891       |
| ResNet      | 0.324     | 0.900         | 0.982    | 0.903          | 0.897       |
| MobileNetV2 | 0.941     | 0.581         | 0.842    | 0.620          | 0.483       |
| InceptionV3 | 0.426     | 0.858         | 0.974    | 0.867          | 0.852       |
| DenseNet169 | 0.304     | 0.896         | 0.981    | 0.899          | 0.889       |
| EfficientNetb0 | 0.110  | 0.962         | 0.997    | 0.964          | 0.962       |
| CNN         | 0.035     | 0.991         | 0.999    | 0.991          | 0.991       |

### Machine Learning Models


|      Model            | Accuracy | Precision | Recall |
|-----------------------|----------|-----------|--------|
| Logistic Regression   |   0.75   |    0.81   |  0.73  |
|        SVM            |   0.99   |    0.99   |  0.99  |
|    Random Forest      |   0.71   |    0.64   |  0.42  |



## Overall Accuracy of all Models Comparison Plot



This plot shows that we get our highest accuracies from our **Conventional CNN model** and **PCA-SVM model** . While other models have also acquired quite decent accuracies.

For more of these plots over different performance metrics such as loss, precison, recall, auc etc.



## Future Scope and Limitations
- Larger and more diverse datasets: Acquiring larger and more diverse datasets can help improve the performance and generalizability of the CNN model.
- Multi-modal data fusion: Incorporating multiple imaging modalities, such as functional MRI (fMRI), positron emission tomography (PET), or cerebrospinal fluid (CSF) biomarkers, along with MRI data, can provide complementary information for more accurate prediction. 
- Longitudinal analysis: Alzheimers disease is a progressive condition that evolves over time. Incorporating longitudinal data and analyzing disease progression can offer valuable insights into the temporal patterns and changes in brain structures.
- Integration with clinical data: Combining MRI data with clinical information, such as cognitive test scores, medical history, genetic data, or lifestyle factors, can lead to a more comprehensive and accurate prediction model. 




