# Foreign-Object-Detection

The detection of Tuberculosis, Asthma, Bronchitis, and/or other pulmonary diseases uses the automated Chest X-Ray (CXR) screening process designed by computer scientists along with medical experts. Although this screening process helps in detecting diseases, it does not consider detecting foreign objects such as coins, buttons, rings, pins, and other objects which may hinder the performance of the process. The circle-like foreign objects can be confused with nodules, one of the primary indicators of Tuberculosis. Thus, foreign object detection in the automated screening process is required. \
We propose a YOLO algorithm for the detection of foreign objects in Chest X-Ray images. Additionally, we have compared YOLO v5 and YOLO v6 on the same dataset and studied the difference in performance. For this dataset, we got better results with the YOLO v5 model than with YOLO v6.

## Dataset
The dataset we used is collected from about 300 township hospitals in China. 12 medically-trained radiologists with 1 to 3 years of experience annotated all the images. Each annotator manually annotates the potential foreign objects on a given chest X-ray presented within the lung field. Foreign objects were annotated with bounding boxes, bounding ellipses, or masks depending on the shape of the objects. The dataset consists of 5000 frontal chest X-ray images with foreign objects presented and 5000 frontal chest X-ray images without foreign objects.\
A typical frontal chest X-ray with a foreign object present looks like [Figure 1](http://url/to/img.png)

## Data Pre-Processing
As we planned to use the YOLO algorithm for training and YOLO only detects images in rectangles, we eliminated the objects with polygon annotations. The annotations in the given dataset were in a CSV file, hence, we created an object-level annotation text file for the entire dataset. Then, we converted the annotations to the YOLO recognizable format (x, y, w, h) for both rectangle and ellipse classes and scaled the width and height to the range of 0-1.

## Model
YOLO (you only look once) predicts what objects are present and where they are in a single iteration. It is refreshingly simple and extremely fast. It recognizes each bounding box using four numbers: Center of the bounding box ((b_{x}, b_{y})), width of the box (b_{w}), and height of the box (b_{h}). In addition to that, YOLO predicts the corresponding number c for the predicted class as well as the probability of the prediction (P_{c}).\
We used YOLO v5 and v6 for training the dataset. Image sizes for both versions were 640. Batch sizes as 16 over 150 epochs and 32 over 100 epochs for YOLO v5 and v6 respectively.

## Results
After training YOLO v5 and v6 on the dataset, we observed that v5 performed better than v6. The mAP@50 was 0.475 and 0.351 for v5 and v6 respectively. At the same time, mAP@50-90 was 0.22 and 0.179 for v5 and v6 respectively. The training time for v6 was more than that or v5. YOLO v6 took around 4 hours while YOLO v5 took around 1.3 hours for training.
