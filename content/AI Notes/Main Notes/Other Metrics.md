---
title: Other Metrics
created: 2023-09-01T20:10:00
last modified: Friday 1st September 2023 20:10
aliases: 
tags:
  - AI
  - UL
  - SL
type: Optimization
---
## Sensitivity
---
- Sometimes referred to as recall, **sensitivity** is one of the possible alternatives to accuracy for measuring your model’s success.
- Using sensitivity as the main unit of measurement allows you to find out how many of the actually true data points were identified correctly.
![[confusion-matrix-layout.png]]
$$Sensitivity = {TP \over (FN + TP)}$$
- In other words, a model with no false negatives whatsoever has perfect sensitivity.
- This makes sensitivity the ideal measurement for models wherever avoiding false negatives is your biggest priority.
## Specificity
---
- **Specificity** measures how many of the actually false data points were correctly identified as negative.
![[confusion-matrix-layout.png]]
$$Specificity = {TN \over (TN + FP)}$$
- Specificity should be a priority for models where false positives are highly undesirable.
## Precision
---
- **Precision** is handy for when you want to avoid false positives.
- Precision identifies how many of the predicted true results were actually true.
![[confusion-matrix-layout.png]]
$$Precision = {TP \over (TP + FP)}$$
## Balancing Risk
---
- It's crucial to select the right measurement for a specific problem.
- In the context of identifying patients with cancer, precision and sensitivity are two important metrics.
- **High sensitivity** means that among individuals with cancer, most will be correctly diagnosed. It focuses on minimizing false negatives.
- **High precision** means that if a test is positive, there's a high likelihood that the patient has cancer. It focuses on minimizing false positives.
- Sensitivity and precision aim to achieve different goals and can lead to different outcomes.
- In a scenario where 50 out of 100 people have cancer and an aggressive screening algorithm labels everyone as having cancer, sensitivity is 100%, but precision is low (50%) due to many false positives.
- In the context of a machine learning algorithm determining guilt in the criminal justice system, precision is more crucial than sensitivity.
- Perfect sensitivity might lead to wrongful convictions, while perfect precision ensures that those declared guilty are indeed guilty.
![[precision-sensitivity-comparison.png]]
## F1 Score
---
- Sometimes referred to as the **harmonic mean**, the **F1 score** is a summarizing statistic describing how balanced your sensitivity and precision scores are.
- $$F1 \ Score = {2(Precision * Specificity) \over (Precision + Specificity)}$$
- Or in terms of values used in the confusion matrix:
![[confusion-matrix-layout.png]]
$$F1 \ Score = {2TP \over (2TP + FP + FN)}$$
- The closer your F1 score is to 1, the more balanced the two measurements are. The closer to 0, the more imbalanced.
---
>Related Notes: [[Accuracy]]

>Tags: #AI #UL #SL 
