# ddos-detection-classical-vs-quantum-ml
Comparing classical and quantum machine learning models for binary DDoS detection using the DrDoS_SSDP dataset.


````markdown
# كشف هجمات DDoS: مقارنة النماذج التقليدية والكمومية
# DDoS Detection: Classical vs. Quantum Models

## نبذة عن المشروع | About

يقارن هذا المشروع أداء نماذج تعلم آلي تقليدية وكمومية في تصنيف حركة الشبكة إلى **BENIGN** أو **ATTACK**، باستخدام مجموعة بيانات **DrDoS_SSDP**.

This project compares classical and quantum machine learning models for classifying network traffic as **BENIGN** or **ATTACK**, using the **DrDoS_SSDP** dataset.

## النماذج | Models

- **تقليدية | Classical:** SVM، KNN، CNN
- **كمومية | Quantum:** QSVM، QKNN، QCNN

تُحاكى الدوائر الكمومية باستخدام PennyLane و`default.qubit`. لم يُستخدم جهاز كمومي حقيقي.

Quantum circuits are simulated using PennyLane and `default.qubit`. No physical quantum device was used.

## المنهجية | Methodology

1. تنظيف البيانات، وحذف الأعمدة التعريفية والصفوف المكررة.
2. ترميز التصنيف الثنائي: `BENIGN = 0` و`ATTACK = 1`.
3. اختيار عينة مشتركة بحجم 12,000 سجل لجميع النماذج.
4. تقسيم البيانات طبقيًا إلى Train وValidation وFinal Test بنسبة 60% و20% و20%.
5. تطبيق المعالجة على Train فقط: التعويض بالوسيط، StandardScaler، PCA، ثم MinMax إلى المجال `[-1, 1]`.
6. اختيار إعدادات النماذج باستخدام Validation و`Macro-F1`.
7. تقييم النماذج على Final Test، وتكرار التجربة باستخدام خمسة Seeds: `42–46`.

1. Clean the data and remove metadata columns and duplicate rows.
2. Encode the binary labels as `BENIGN = 0` and `ATTACK = 1`.
3. Select a shared sample of 12,000 records for all models.
4. Use stratified Train, Validation, and Final Test splits of 60%, 20%, and 20%.
5. Fit preprocessing on Train only: median imputation, StandardScaler, PCA, and MinMax scaling to `[-1, 1]`.
6. Select model settings using Validation and `Macro-F1`.
7. Evaluate on the Final Test set and repeat the experiment with five seeds: `42–46`.

## النماذج الكمومية | Quantum Models

يستخدم QSVM وQKNN ترميزًا زاويًا ونواة مبنية على Fidelity. أما QCNN فيستخدم دائرة كمومية قابلة للتدريب، مع PyTorch للتدريب.

QSVM and QKNN use angle encoding and a fidelity-based kernel. QCNN uses a trainable quantum circuit with PyTorch for training.

## مقاييس التقييم | Evaluation Metrics

يشمل التقييم Accuracy وBalanced Accuracy وPrecision وRecall وF1 وMacro-F1 وF1-BENIGN وMCC وROC-AUC وPR-AUC، بالإضافة إلى مصفوفة الالتباس وأزمنة التدريب والضبط والتنبؤ.

Evaluation includes Accuracy, Balanced Accuracy, Precision, Recall, F1, Macro-F1, F1-BENIGN, MCC, ROC-AUC, and PR-AUC, as well as confusion matrices and training, tuning, and prediction times.

## تشغيل المشروع | Run the Project

يمكن تشغيل الدفتر باستخدام Google Colab:

1. افتح ملف `Worksession_DDoS_Classical_vs_Quantum_REVIEWED.ipynb` في Colab.
2. ضع ملف البيانات في Google Drive.
3. حدّث قيمة `DATA_PATH` في الدفتر لتشير إلى ملف CSV أو ZIP.
4. شغّل الخلايا بالترتيب. الدفتر يثبت الحزم المطلوبة.

To run the notebook in Google Colab:

1. Open `Worksession_DDoS_Classical_vs_Quantum_REVIEWED.ipynb`.
2. Place the dataset file in Google Drive.
3. Update `DATA_PATH` in the notebook to point to the CSV or ZIP file.
4. Run the notebook cells in order. Required packages are installed by the notebook.

استخدم `QUICK_TEST=True` للتحقق السريع من تشغيل الدفتر فقط. لا تستخدم نتائج هذا الوضع في الاستنتاجات.

Use `QUICK_TEST=True` only to check that the notebook runs. Do not use quick-test results for conclusions.

## المخرجات | Outputs

يحفظ الدفتر النتائج والجداول وسجلات ضبط الإعدادات والرسوم في مجلد `ddos_qml_outputs`.

The notebook saves result tables, tuning logs, and plots in the `ddos_qml_outputs` folder.

## ملاحظات وحدود الدراسة | Notes and Limitations

- نتائج النماذج الكمومية مبنية على المحاكاة، ولا تمثل أداء جهاز كمومي حقيقي.
- تعتمد النتائج على العينة والتقسيم المستخدمين في هذه التجربة، ولا تثبت التعميم على شبكات أو فترات زمنية أخرى.
- في التشغيل المحفوظ، لم يظهر تفوق عملي واضح للنماذج الكمومية وفق عتبة المقارنة المستخدمة في الدفتر (`0.005`).

- Quantum results are based on simulation and do not represent performance on real quantum hardware.
- Results depend on the sample and split used in this experiment and do not establish generalization to other networks or time periods.
- In the saved run, no clear practical quantum advantage was observed under the comparison threshold used in the notebook (`0.005`).

## مصدر البيانات | Dataset Source

DrDoS_SSDP: [https://www.unb.ca/cic/datasets/ddos-2019.html]
````
