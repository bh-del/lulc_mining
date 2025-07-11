# 📊 Results

We provide sample results from the U-Net-based classification of Sentinel-2 imagery over the **Strzegom** mining area (scene acquired on **2023-07-09**):

- 🖼️ **Classified image**: [`strzegom_20230709_33u_class.tif`](./strzegom_20230709_33u_class.tif)  
  → GeoTIFF raster showing pixel-wise LULC classification output

- 🧮 **Confusion matrix**: [`Confusion_matrix_strzegom_20230709.csv`](./Confusion_matrix_strzegom_20230709.csv)  
  → Tabular accuracy summary comparing predicted vs. reference classes

🎯 These results can be used as a **benchmark** for evaluating your own models or algorithms on the same task.



## 🚀 Want to improve the accuracy?

Try using:
- ⚙️ Alternative classifiers (e.g., Random Forest, CNN, transformers)
- 🧽 Preprocessing techniques (e.g., cloud masking, normalization)
- 🧠 Data augmentation or temporal stacking

We’re excited to see how our dataset performs under various approaches.  
📬 *Feel free to share your results or improvements!*


# Our selected accuracy metrics

📊 Classification Metrics (Per Class, Overall, and Mean)

| Class   | Accuracy (ACC) | Specificity (TNR) | Producer Accuracy (PA) | User Accuracy (UA) | F1-score |
|---------|----------------|-------------------|-------------------------|---------------------|----------|
| 1       | 0.9842         | 0.9852            | 0.9547                  | 0.6857              | 0.7981   |
| 2       | 0.9751         | 0.9972            | 0.8962                  | 0.9889              | 0.9402   |
| 3       | 0.9946         | 0.9964            | 0.8954                  | 0.8213              | 0.8568   |
| 4       | 0.9764         | 0.9772            | 0.9733                  | 0.9119              | 0.9416   |
| 5       | 0.9932         | 0.9931            | 0.9948                  | 0.8173              | 0.8974   |
| 7       | 0.9967         | 0.9974            | 0.7024                  | 0.3688              | 0.4836   |
| 8       | 0.9989         | 0.9998            | 0.9449                  | 0.9906              | 0.9673   |
| 9       | 0.9773         | 0.9923            | 0.9422                  | 0.9814              | 0.9614   |
| 10      | 0.9964         | 0.9995            | 0.9827                  | 0.9976              | 0.9901   |
| **Overall Accuracy (OA)** | **0.9464**     | --                | --                      | --                  | --       |
| **Mean**    | **0.9881**     | **0.9931**         | **0.9207**              | **0.8404**          | **0.8707** |


The following classes were adopted in our study:

1. <span style="color:#2e8b57;">🌲 <strong>Conifer forest</strong></span>
2. <span style="color:#3cb371;">🌳 <strong>Mix forest</strong></span>
3. <span style="color:#8b0000;">🏙️ <strong>Urban</strong></span>
4. <span style="color:#deb887;">🌾 <strong>Crops</strong></span>: crops before harvest or in spring before carrying out agrotechnical treatments
5. <span style="color:#a0522d;">🟤 <strong>Bare soils</strong></span>
6. <span style="color:#32cd32;">🌿 <strong>Permanent grassland</strong></span>
7. <span style="color:#808080;">🛣️ <strong>Roads</strong></span>
8. <span style="color:#1e90ff;">🌊 <strong>Waters</strong></span>
9. <span style="color:#228b22;">🌱 <strong>Crops in vegetation stage</strong></span>
10. <span style="color:#696969;">⛏️ <strong>Quarries, open pits</strong></span>

---

## 🧮 Interpreting Accuracy: Overall Accuracy vs. Mean Class ACC

### 📌 Metric Definitions

- **Overall Accuracy (OA)**  
  OA = sum(TP) / (TP + TN + FP + FN)  
  → Proportion of all correctly classified samples across the dataset.

- **Per-Class Accuracy (ACC)**  
  ACC = (TP + TN) / (TP + TN + FP + FN)  
  → Accuracy for a single class, including both true positives and true negatives.

- **Mean ACC**  
  Arithmetic mean of ACC values across all classes.

---

### ⚠️ Why ACC Can Be Misleading

In multi-class classification, the number of **true negatives (TN) is very large** for each individual class — because TN includes all samples that do **not** belong to that class.  
This inflates the ACC value, especially for **minority classes**.

#### Example from our results:

- **Overall Accuracy (OA):** 0.9464  
- **Mean ACC:** 0.9881 ✅ ← artificially high due to large TN counts

---

### 🧠 Key Takeaways

| Metric       | Represents                                     | Be careful when...                                  |
|--------------|------------------------------------------------|-----------------------------------------------------|
| **OA**       | Overall correct predictions                    | Dataset is imbalanced (dominant classes inflate OA) |
| **Mean ACC** | Mean per-class accuracy (incl. true negatives) | TN dominates — risk of inflated accuracy            |

🟡 **Always complement OA and ACC with**:
- **F1-score** – harmonic mean of precision and recall  
- **PA (Producer Accuracy)** – sensitivity / recall  
- **UA (User Accuracy)** – precision  

These metrics give a more realistic view of class-wise performance.



# 🧠 Accuracy Analysis Made Easy

Run powerful and flexible accuracy evaluations with just one script!  
Our companion tool lets you plug in your own data and instantly compute a wide range of accuracy metrics.

👉 Try it here: [**accuracy_checker**](https://github.com/python-edu/accuracy_checker)


1.The input is a single *.csv file:
- raw data: data2cols.csv or data3cols.csv
- confusion matrix: cross_raw.csv, cross.csv or cross_full.csv
- binary_cross.csv
- accuracy file.csv
- accuracy file.csv class_map.json


2. Input raster / vector:
- an image, after classification - usually of type *.tif
- reference data: image/mask *.tif or vector data e.g. *.shp, *.gpkg
- raster.tif
- raster.tif class_map.json
- raster.tif reference_raster.tif
- raster.tif reference_raster.tif class_map.json
- raster.tif reference_vector.shp
- raster.tif reference_vector.shp class_map.json


# Metrics help

### 1. Symbols:

The definitions of the metrics are mainly based on the binary error matrix with the following symbols:
 - TP true positive
 - TN true negative
 - FP false positive
 - FN false negative.


### 2. Accuracy metrics classically used in remote sensing:

 - OA (overall_accuracy):
   >$OA = \sum(TP) / (TP + TN + FP + FN)$

 - PA (producer_accuracy):
   >$PA = TP / (TP + FN)$

 - UA (user_accuracy)
   >$UA = TP / (TP + FP)$

 - OME (omission errors / errors_of_omission):
   >$OME = FN / (TP + FN)$

 - CME (errors_of_commision):
   >$CME = FP / (TP + FP)$

 - NPV (negative predictive value):
   >$NPV = TN/(TN + FN) = 1 − FOR$


### 3. Classification accuracy metrics found in contemporary scientific publications

 >some metrics overlap with some of the metrics mentioned in point 1.

These metrics can be conventionally divided into simple metrics (calculated directly from the TP, TN, FP and FN values) and
   complex metrics (calculated using simple metrics).

3.1. Simple metrics:

 - ACC (accuracy):
   >$ACC = (TP+TN) / (P+N) = (TP+TN) / (TP+TN+FP+FN)$

 - PPV (precision or positive predictive value):
   >$PPV = TP / (TP + FP)$

 - TPR (sensitivity, recall, hit rate, or true positive rate):
   >$TPR = TP / P = TP / (TP + FN) = 1 − FNR$

 - TNR (specificity, selectivity or true negative rate):
   >$TNR = TN / N = TN / (TN + FP) = 1 − FPR$

 - NPV (negative predictive value):
   >$NPV = TN / (TN + FN) = 1 − FOR$

 - FNR (miss rate or false negative rate):
   >$FNR = FN / P = FN / (FN + TP) = 1 − TPR$

 - FPR (fall-out or false positive rate):
   >$FPR = FP / N = FP / (FP + TN) = 1 − TNR$

 - FDR (false discovery rate):
   >$FDR = FP / (FP + TP) = 1 − PPV $

 - FOR (false omission rate):
   >$FOR = FN / (FN + TN) = 1 − NPV $

 - TS / CSI (Threat score (TS) or critical success index (CSI)):
   >$TS = TP / (TP + FN + FP) $

 - MCC (Matthews correlation coefficient):
   >$mcc = (TP \cdot TN - FP \cdot FN) / ((TP+FP) \cdot (TP+FN) \cdot (TN+FP) \cdot (TN+FN))^{0.5}$


3.2. Complex metrics:

 - PT (Prevalence Threshold):
   >$PT = ((TPR \cdot (1 − TNR))^{0.5} + TNR − 1) / (TPR + TNR − 1)$

 - BA (Balanced accuracy):
   >$ba = (TPR + TNR) / 2$

 - F1 score (is the harmonic mean of precision and sensitivity):
   >$f1 = 2 \cdot (PPV \cdot TPR) / (PPV + TPR) = (2 \cdot TP + FP + FN)$

 - FM (Fowlkes–Mallows index):
   >$fm = ((TP/(TP+FP)) \cdot (TP/(TP+FN)))^{0.5} = (PPV \cdot TPR)^{0.5}$

 - BM (informedness or Fowlkes–Mallows index):
   >$bm = TPR + TNR - 1$

 - MK (markedness (MK) or deltaP):
   >$mk = PPV + NPV - 1$

