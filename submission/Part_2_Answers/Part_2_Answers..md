\# Part 2: Reasoning-Based Questions (Write-up)



\## Q1: Choosing the Right Approach

You are tasked with identifying whether a product is missing its label on an assembly line. The products are visually similar except for the label.



Q: Would you use classification, detection, or segmentation? Why? What would be your fallback if the first approach doesn’t work?

A1. The correct approach is as follows-

* For detecting whether a product is missing its label I would start with detection.
* A detector can localize the product and the label area, letting you explicitly verify presence/absence or compute label coverage.
* If the label location is very consistent and crops are small, a simpler classification on a cropped region might suffice and is cheaper.
* Segmentation could be used if the label shape/coverage matters (e.g., partially peeled labels) because it provides pixel-level detail.
* If detection fails due to subtle label cues, my fallback would be a hybrid: use segmentation on the label area or a classification model trained on high-resolution cropped patches to capture finer texture/print differences.



\## Q2: Debugging a Poorly Performing Model

You trained a model on 1000 images, but it performs poorly on new images from the factory.



Q: Design a small experiment or checklist to debug the issue. What would you test or visualize?



A2. My steps will be as follows-

* First to check data distribution: I would visualize examples from train vs test and ensure labels are correct and representative of factory images (lighting, viewpoint, occlusion).
* Next I will run the inference on a few failing images and visualize predicted boxes, confidences, and heatmaps or class scores to see whether the model is underconfident or mis-localizing.
* Then I will Verify augmentation and preprocessing steps (resizing, color space), and test performance with and without augmentations to look for mismatch.
* Finally try ablation: reduce to a small curated validation set, train for a few epochs to overfit a handful of samples (sanity check), and inspect class-wise precision/recall to identify class imbalance or label noise.



\## Q3: Accuracy vs Real Risk

Your model has 98% accuracy but still misses 1 out of 10 defective products.



Q: Is accuracy the right metric in this case? What would you look at instead and why?



A3. What i would look through will be-

* Accuracy can be misleading when class imbalance or asymmetric risk exists; here the cost of missing a defective product is high, so accuracy alone is insufficient.
* Instead, emphasize \*\*recall\*\* (sensitivity) for the defective class because missing defects produces real safety/financial risk, paired with precision to control false alarms.
* Also monitor confusion matrix, per-class precision/recall/F1, and ROC/PR curves to choose an operating point that balances risk and workload.
* If false negatives are catastrophic, tune threshold to maximize recall and use human-in-the-loop review for high-uncertainty cases.





\## Q4: Annotation Edge Cases

You’re labeling data, but many images contain blurry or partially visible objects.



Q: Should these be kept in the dataset? Why or why not? What trade-offs are you considering?

A4. My Ans is as followed-

* Blurry or partially visible objects should not be automatically discarded — they reflect real-world conditions and improve model robustness if labeled correctly.
* However, they increase label noise: if the object is impossible to label reliably, it might be better to exclude or flag such samples to avoid confusing the model.
* A compromise is to include those images with an "uncertain" tag or lower weight during training, or create a separate class that represents partial/uncertain instances.
* The trade-off is between robustness to messy inputs (include) versus cleaner signal for faster convergence and higher peak accuracy (exclude).
