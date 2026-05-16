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
