<h2><strong>Task-01: Dataset Understanding & Preprocessing</strong></h2>

<h3><strong>Dataset Overview</strong></h3>

<p>
This project uses the <strong>VisDrone Dataset</strong>, a drone-based aerial image dataset for object detection and tracking. The dataset contains high-resolution drone images captured in urban and suburban environments. It includes objects such as pedestrians, people, cars, vans, trucks, bicycles, buses, motorcycles, and other traffic-related objects.
</p>

<p>
The dataset used in this project is already converted into <strong>YOLO format</strong>, so each image has a corresponding <code>.txt</code> label file.
</p>

<p>Each label line follows this YOLO format:</p>

<pre><code>class_id x_center y_center width height</code></pre>

<h3><strong>Original Classes</strong></h3>

<pre><code>0: pedestrian
1: people
2: bicycle
3: car
4: van
5: truck
6: tricycle
7: awning-tricycle
8: bus
9: motor</code></pre>

<p>
The assessment requires detecting <strong>humans</strong> and <strong>cars</strong>. Therefore, only the required classes were selected.
</p>

<p>The class mapping used in this project is:</p>

<pre><code>Original class 0: pedestrian → New class 0: human
Original class 1: people     → New class 0: human
Original class 3: car        → New class 1: car</code></pre>

<p>
All other classes were removed from the training and validation labels.
</p>

<h3><strong>Final Classes</strong></h3>

<pre><code>0: human
1: car</code></pre>

<h2><strong>Task-02: Model Training & Evaluation</strong></h2>

<h3><strong>1. Environment Setup and Dataset Configuration</strong></h3>

<p>
A YOLO-compatible <code>data.yaml</code> file was created after preprocessing the dataset. This file defines the training and validation image paths and the two final classes used in this project.
</p>

<pre><code>path: /kaggle/working/drone_human_car_dataset
train: images/train
val: images/val

names:
  0: human
  1: car</code></pre>

<p>
This configuration is required so that YOLO can locate the dataset and correctly map class IDs to class names.
</p>

<h3><strong>2. Model Selection and Training</strong></h3>

<p>
A pre-trained <strong>YOLO11m</strong> model was used and fine-tuned on the processed VisDrone dataset. YOLO was selected because it is fast, suitable for real-time detection, and effective for object detection tasks in drone imagery.
</p>

<pre><code>Model: YOLO11m
Image size: 960
Epochs: 50
Batch size: 8
Classes: human, car
Training type: Transfer learning / fine-tuning</code></pre>

<p>
The model was trained using filtered training images and labels. Validation was done using filtered validation images and labels.
</p>

<h3><strong>3. Training Outputs</strong></h3>

<p>
After training, the following main files were generated:
</p>

<pre><code>best.pt
last.pt
results.png
confusion_matrix.png
PR_curve.png
P_curve.png
R_curve.png
F1_curve.png</code></pre>

<p>
The <code>best.pt</code> file was used for final prediction, human counting, tiled detection, heatmap visualization, and test evaluation.
</p>

<h3><strong>4. Validation Results</strong></h3>

<p>
The trained model was evaluated on the validation dataset. The validation result showed that car detection performed better than human detection because cars are larger and easier to detect in aerial images.
</p>

<pre><code>Overall Precision: 0.8197
Overall Recall: 0.7182
Overall mAP50: 0.7124
Overall mAP50-95: 0.4505

Human mAP50: 0.602
Car mAP50: 0.822</code></pre>
