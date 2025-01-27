# CIFAR-10 Image Classification  

## Dataset Preparation  
I kicked things off by loading the CIFAR-10 dataset into my environment. I then split it into training, validation, and testing sets to make sure the model was evaluated on unseen data, ensuring accurate performance measurements.  

Since the images in the CIFAR-10 dataset are on the smaller side (32×32 pixels), I trained a baseline model using the original image size to set a benchmark before moving on to transfer learning and fine-tuning.  

## Baseline Model  
The baseline model hit an accuracy of **70%** on the test dataset. This gave me a solid reference point for seeing how much I could improve by bringing in a pre-trained model.
![Screenshot 2025-01-27 175510](https://github.com/user-attachments/assets/4f3e9237-1ba8-4835-80b6-d6d0241ed942)

## Transfer Learning with MobileNetV2  
To improve on my results, I brought in the MobileNetV2 model pre-trained on the ImageNet dataset. I picked MobileNetV2 because of its lightweight architecture, which is perfect for training on my laptop compared to bulkier models.  

MobileNetV2 works best with larger input sizes, so I resized the CIFAR-10 images from 32×32 to 96×96 pixels. Although I initially aimed for 128×128 pixels, my hardware couldn't handle it, so 96×96 it was.  

I froze all layers of the MobileNetV2 model to keep the pre-trained weights intact and added a custom classification head:  
- A **Global Average Pooling** layer to cut down spatial dimensions.  
- Two fully connected dense layers, with a **dropout layer** for regularization.  
- A final softmax layer to output class probabilities for the 10 CIFAR-10 categories.
![Screenshot 2025-01-27 182710](https://github.com/user-attachments/assets/372012b9-9cba-4460-88de-ce6e77f3f03d)


With this setup, the model's accuracy rose to **79.7%** on the test dataset.
![Screenshot 2025-01-27 180440](https://github.com/user-attachments/assets/36d45027-1423-42aa-9e34-2f395c285397)


## Fine-Tuning  
To squeeze out even more performance, I unfroze the last four layers of the MobileNetV2 model and lowered the learning rate to fine-tune without overwriting the pre-trained features. This bumped the test accuracy up to **83.8%**.
![Screenshot 2025-01-27 180836](https://github.com/user-attachments/assets/b662dbe6-d983-4df4-83b2-6e6cd76bef4b)


## Next Steps and Potential Improvements  
While I'm pretty pleased with the current performance, I see room for further improvements with more time and computational power. Here are a few ideas:  
1. **Data Augmentation**: Applying transformations like rotation, flipping, and cropping to enhance the model's robustness.  
2. **Larger Image Sizes**: Bumping up the input size to at least 128×128 or even 224×224 pixels for better feature extraction.  
3. **Experimenting with Other Architectures**: Trying out other pre-trained models like EfficientNet or ResNet for comparison.  
