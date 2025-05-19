# 🌈 RGB to Hyperspectral Image Generation using AWAN

This project uses a **pretrained AWAN model** ([Adaptive Weighted Attention Network](https://openaccess.thecvf.com/content_CVPRW_2020/papers/w31/Li_Adaptive_Weighted_Attention_Network_With_Camera_Spectral_Sensitivity_Prior_for_CVPRW_2020_paper.pdf)) to convert standard RGB images into 31-band hyperspectral (HS) images. The goal is to explore spectral reconstruction from natural images in different datasets and evaluate performance.

## 📚 Model

- **AWAN**: Adaptive Weighted Attention Network
- Pretrained on a standard HS reconstruction dataset (e.g., NTIRE challenge dataset)
- Input: RGB image (`.jpg` or `.png`)
- Output: HS cube (`.mat` file, 31 spectral bands from 400nm to 700nm)

## 🧪 Evaluation Results

After applying the AWAN model to different datasets, we evaluated its performance using PSNR, SSIM, and RMSE:

### ✅ On CAVE DB (Unseen Test Set)

```
📊 AVERAGE RESULTS:
  Average PSNR: 14.13
  Average SSIM: 0.431
  Average RMSE: 0.183
```

These results are acceptable but lower than those reported on the training/test set used in the original AWAN paper, which is expected when applying to out-of-distribution datasets.

## 🗂️ Datasets Used

### 📦 1. **CAVE Hyperspectral Dataset** 

- Only if you want to check the model
- 32 scenes (indoor objects, fabric, skin, food, etc.)
- Each scene contains 31 grayscale PNGs from 400nm to 700nm at 10nm intervals
- Each image is a 16-bit grayscale PNG
- Used as a real-world benchmark to test AWAN's generalization
- Download: [CAVE Dataset](http://www.cs.columbia.edu/CAVE/databases/multispectral/)

### 🐘 2. **ImageNet-R**

- A rendition-style subset of ImageNet (cartoons, paintings, sketches, etc.)
- Contains ~30,000 images across 200 classes
- Used to test AWAN on visually diverse, non-photographic inputs
- In this project, the **first class (`n01443537`) with 230 images** was fully converted to hyperspectral
- You can also:
  - Convert any specific class by changing `cls_path`
  - Or sample randomly across all classes

## ⚙️ How to Use

1. Load the pretrained AWAN model
2. Call `RGB_2_HS(model, input_path, output_path)`
3. Outputs are `.mat` files containing 31-band hyperspectral data

You can visualize the result using the `show_hs_rgb()` function (selecting bands for R/G/B, e.g., 650/550/450nm).

## 📁 File Structure

```
├── CAVE_DB/               # 31-band hyperspectral images
├── ImageNet-R/            # Original RGB classes
├── imagenet_results/      # AWAN-generated HS reconstructions
├── imagenet-r-sample/     # Sampled RGB images
├── MS_RGB_to_HS_Database_using_AWAN_Network.ipynb  # Main Colab notebook
└── README.md              # This file
```


@InProceedings{Li_2020_CVPR_Workshops,
author = {Li, Jiaojiao and Wu, Chaoxiong and Song, Rui and Li, Yunsong and Liu, Fei},
title = {Adaptive Weighted Attention Network With Camera Spectral Sensitivity Prior for Spectral Reconstruction From RGB Images},
booktitle = {The IEEE/CVF Conference on Computer Vision and Pattern Recognition (CVPR) Workshops},
month = {June},
year = {2020}
}
