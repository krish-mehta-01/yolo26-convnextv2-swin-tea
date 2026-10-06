# Label_Crop_Dataset: Tea Leaf Disease Lesion Crops

Lesion-crop dataset accompanying the manuscript *"YOLOv26m-Guided Lesion Cropping with Adaptive Image Enhancement and ConvNeXtV2–Swin Transformer Ensemble for Automated Tea Leaf Disease Classification"* (under review). It was used to train and evaluate the ConvNeXtV2-Base and Swin-Base-384 classifiers.

It contains one enhanced 256 × 256 lesion crop for each of the 885 images in the **tea sickness dataset** (see [Source and licence](#source-and-licence)).

## Contents

```
Label_Crop_Dataset/
├── Algal Leaf Spot/   # 113 crops
├── Anthracnose/       # 100
├── Bird_s Eye Spot/   # 100
├── Brown Blight/      # 113
├── Gray Blight/       # 100
├── Healthy/           # 74
├── Red Leaf Spot/     # 143
└── White Spot/        # 142
```

Each file is named `<original file name>_crop.jpg`, so every crop can be traced back to its source image. `Bird_s Eye Spot` uses an underscore in place of the apostrophe.

## How the crops were made

1. A YOLO26m lesion detector, trained on manually annotated bounding boxes, was run on each original image (confidence threshold 0.25), and the highest-confidence box was used.
2. The box was padded by 8 px on each side (clipped to the image) and cropped from the full-resolution image. For the one image with no detection (Gray Blight), the central 70% of the image was used instead.
3. The class label was taken from the original dataset's class folder, never from the detector's prediction.
4. Each crop was enhanced with Pillow:
   - resize to 256 × 256 (LANCZOS)
   - `ImageFilter.UnsharpMask(radius=1.5, percent=120, threshold=3)`
   - `ImageEnhance.Contrast(1.25)`
   - `ImageEnhance.Color(1.15)`
   - `ImageEnhance.Sharpness(1.3)`
5. Saved as JPEG (quality 95).

## Source and licence

The original images are from:

> Kimutai, G., & Förster, A. (2022). *tea sickness dataset* (Version 2) [Data set]. Mendeley Data. https://doi.org/10.17632/j32xdt2ff5.2 (CC BY 4.0)

also mirrored on Kaggle as [Identifying Disease in Tea leaves](https://www.kaggle.com/datasets/shashwatwork/identifying-disease-in-tea-leafs) (CC BY-SA 4.0).

This dataset is an adaptation of those images (cropped and enhanced as described above) and is shared under [CC BY-SA 4.0](https://creativecommons.org/licenses/by-sa/4.0/). If you use it, please cite the original dataset above and our paper (citation will be added on publication).
