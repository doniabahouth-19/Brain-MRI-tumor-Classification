# Brain MRI Tumor Classification Assistant

## Final Project

This project is an AI-assisted dashboard for classifying brain MRI images into four classes:

- Glioma
- Meningioma
- Pituitary tumor
- No tumor

The system is intended to support physician review and does not replace clinical diagnosis.

## Final Classification Method

The final classifier is a fine-weighted probability ensemble using three trained convolutional neural network models:

- EfficientNetV2S
- InceptionV3
- EfficientNetB0

### Ensemble Weights

- EfficientNetV2S: 0.185
- InceptionV3: 0.305
- EfficientNetB0: 0.510

The final class is selected from the weighted combination of the probability outputs from the three models.

## Suspicious-Region Assistance

When the final prediction is one of the tumor classes, the dashboard runs a grayscale-based suspicious-region analysis and displays up to three candidate regions for physician review.

When the prediction is `notumor`, the suspicious-region analysis is skipped and no candidate boxes are displayed.

The highlighted regions are automatically detected candidates and are not confirmed tumor boundaries.

## Project Structure

```text
DASHBOARD/
│
├── models/
│   ├── fresh_efficientnetb0_V2_final.keras
│   ├── fresh_efficientnetv2s_V2_deep_final.keras
│   └── fresh_inceptionv3_V2_phase1_final.keras
│
├── app.py
├── grayscale_detector.py
├── logo.png
├── requirements.txt
└── README.md
```

## Installation

Open a terminal inside the `DASHBOARD` folder and install the required packages:

```bash
pip install -r requirements.txt
```

## Run the Dashboard

```bash
streamlit run app.py
```

The dashboard should open automatically in the web browser.

## Final Evaluation Results

- Internal Mendeley test accuracy: 87.11%
- Untouched external Kaggle test accuracy: 84.89%

Logistic Regression and XGBoost stacking methods were also evaluated, but they did not provide a reliable improvement across both untouched test sets. Therefore, the fine-weighted three-model ensemble was selected as the final classification method.

## Clinical Disclaimer

This AI prediction is intended to support clinical decision-making and should always be confirmed by a qualified radiologist or physician.
