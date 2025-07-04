# 🧪 Experiment: *The Vanishing Canvas – When CNNs Shrink Too Much*

I was exploring how **CNN depth impacts performance**.

The experiment was simple on paper:  
> Stack more convolutional layers and check if the model's accuracy improves on a classification task.

I built a flexible CNN architecture in **PyTorch**, where the number of layers could be dynamically configured.  
With each layer, I applied:

1. `Conv2D` operation  
2. `ReLU` activation  
3. `MaxPool2D(kernel_size=2, stride=1)`

---

## ✅ Behavior up to 9 Layers

This setup worked beautifully up to **9 layers**.  
Both training and test accuracies were strong, and the model clearly learned meaningful features.

---

## ❌ What Happened Beyond 9 Layers?

Once I added the **10th layer**, something strange happened:

- Accuracy dropped to ~10%, as if the model was randomly guessing.
- There were **no signs of gradient explosion or vanishing gradients**.
- The optimizer was functioning normally.

---

## 🔍 Root Cause: **Feature Map Shrinkage**

Each `MaxPool2D(2, stride=1)` reduces the spatial dimensions by **1 pixel per layer** in both height and width.

Given an input image of **28×28**, after 10 such layers, it shrinks to **18×18**.

As the spatial canvas gets smaller:

- The receptive field becomes too compressed  
- Higher layers lose meaningful spatial structure  
- Eventually, there's **too little information left to learn from**

> **"If you blindly stack layers without managing spatial dimensions, you risk building a network that's too *blind* to learn."**

---
### Accuracy
<img src="https://github.com/user-attachments/assets/31c04d0e-9a48-4c20-ae9a-47257da5e549" width="400"/>
<img src="https://github.com/user-attachments/assets/ccfa863d-3089-4f33-9882-e0f103764040" width="400"/>

### Loss
<img src="https://github.com/user-attachments/assets/b2183ca8-340d-4e3b-980b-e22a0567bceb" width="400"/>
<img src="https://github.com/user-attachments/assets/a6425a1a-66d4-40a1-a3c4-8602ba880abe" width="400"/>







