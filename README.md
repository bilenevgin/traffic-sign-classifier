Traffic Sign Classification and Detection Project

This project combines object detection and image classification into a hybrid system for traffic sign recognition. It was developed to use the strengths of two approaches: YOLOv11 for real-time traffic sign detection and localization, and a Custom CNN Classifier trained on the GTSRB dataset for classification of cropped traffic sign images. Together, this hybrid system can both detect traffic signs in an image and classify them into their correct categories.

The goal of this project is to build a reliable pipeline for traffic sign recognition that can be used in autonomous driving or driver assistance technologies. YOLO detects traffic signs and draws bounding boxes. The detected sign images are cropped and passed into the CNN classifier. The CNN then outputs the final predicted class. The processed images with bounding boxes and predicted labels are saved in the try_predict directory.

The CNN classifier was trained on the German Traffic Sign Recognition Benchmark (GTSRB) dataset. This dataset contains 43 distinct traffic sign classes and includes thousands of real-world images from Germany with variations in lighting, angles, and weather conditions.

The YOLO model was trained on a separate dataset with 21 traffic sign categories such as stop, do_not_enter, traffic_light, bus_stop, and others. This dataset was used specifically for detection.

Since the YOLO dataset and the GTSRB dataset are not the same, there are some limitations. Some classes overlap directly such as stop, no entry, and traffic lights. Some are similar but not identical, for example warning in YOLO compared with classes like general caution or slippery road in GTSRB. Many classes exist only in one dataset and not the other. This mismatch sometimes leads to misclassifications when the CNN receives crops of traffic signs that do not have a direct equivalent in its training set.

The project was implemented using PyTorch for building and training the CNN model. Ultralytics YOLOv11 was used for traffic sign detection. Pillow and OpenCV libraries were used for image processing and preprocessing. Pandas, NumPy and Matplotlib were used for data handling and visualization.

The custom CNN architecture consists of multiple convolutional layers with batch normalization, ReLU activations and max pooling layers. The input images were resized to 64x64 and normalized before training. The fully connected layers end with 43 outputs representing the GTSRB classes.

The CNN model was trained for 20 epochs using the Adam optimizer and CrossEntropyLoss. The training loss decreased steadily and reached a very low value of 2.73×10⁻⁶. The final accuracy on the test dataset was 96.22 percent.

In the hybrid system, YOLO detects and crops traffic signs, and the CNN classifies these cropped images. Annotated results are stored in the try_predict folder. The system works well for overlapping classes but misclassifications occur due to dataset mismatches.

There are several areas for improvement. One is to retrain YOLO and CNN on a common dataset with the same classes and labeling rules, or at least map YOLO outputs to CNN equivalents more systematically. Data augmentation such as random rotations, zooming and brightness changes could be applied to improve generalization. Dropout layers can be added to the fully connected layers to reduce overfitting. Another possible improvement is to combine YOLO predictions and CNN confidence values for better decision making. Transfer learning approaches with pre-trained models like ResNet or VGG could also be explored.

Annotated results of the hybrid system can be found in the try_predict folder.

Thank you for reviewing this project. I welcome feedback and suggestions, especially regarding dataset harmonization and real-time deployment on embedded systems such as Raspberry Pi.
