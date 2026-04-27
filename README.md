his notebook demonstrates a complete end-to-end workflow for training a deep learning model to classify Alzheimer's MRI scans. Here is a breakdown of what happens:

Data Acquisition: It starts by downloading the 'Best Alzheimer MRI Dataset' from Kaggle using kagglehub. The dataset consists of four classes: Mild Impairment, Moderate Impairment, No Impairment, and Very Mild Impairment.

Preprocessing & Balancing: The original training set is balanced, but to manage resources, we created a balanced subset of 1,000 images per class (4,000 total). This ensures the model doesn't become biased toward any specific category.

Data Augmentation: We use ImageDataGenerator to artificially expand the dataset. By applying random rotations, zooms, and flips during training, the model learns to recognize features regardless of their orientation, which helps prevent overfitting.

Transfer Learning with DenseNet121: Instead of training from scratch, we use DenseNet121 pre-trained on ImageNet. We freeze the original layers (to keep the general image-recognition features) and add a custom 'head':

GlobalAveragePooling2D: Reduces the spatial dimensions.
Dense (512 units): A fully connected layer to learn specific MRI patterns.
Dropout (0.5): Randomly deactivates neurons to ensure the model remains robust.
Softmax Output: Predicts the probability for each of the 4 classes.
Training: The model was trained for 10 epochs on a T4 GPU. You can see the accuracy rising over time as the loss decreases.

Evaluation & Persistence: Finally, the model is evaluated on a separate test set to check its real-world performance. The final .keras model file is saved locally and backed up to your Google Drive in the Aggregation folder
