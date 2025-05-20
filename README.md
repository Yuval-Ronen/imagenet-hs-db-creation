# 🌈 RGB to Hyperspectral Image Generation using AWAN
 
This project uses a **pretrained AWAN model** ([Adaptive Weighted Attention Network](https://openaccess.thecvf.com/content_CVPRW_2020/papers/w31/Li_Adaptive_Weighted_Attention_Network_With_Camera_Spectral_Sensitivity_Prior_for_CVPRW_2020_paper.pdf)) to convert standard RGB images into 31-band hyperspectral (HS) images.
The primary goal is to provide a practical tool for generating large-scale, diverse synthetic hyperspectral datasets from RGB sources like ImageNet-R — helping address the scarcity of publicly available HS databases. While AWAN was originally designed for spectral reconstruction, this project leverages it specifically for dataset creation

## 📚 Model

- **AWAN**: Adaptive Weighted Attention Network
- Pretrained on a standard HS reconstruction dataset (e.g., NTIRE challenge dataset)
- Input: RGB image (`.jpg` or `.png`)
- Output: HS cube (`.mat` file, 31 spectral bands from 400nm to 700nm)

## 🧪 Evaluation Results

After applying the AWAN model to different datasets, we evaluated its performance using PSNR, SSIM, and RMSE:
### ✅ On one image of the test set from the original DB used to train the model

```
📊 RESULTS:
PSNR: 30.332356889477786
SSIM: 0.8704928806007087
RMSE: 0.030566415
```
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
- Optional, if you want to validate the model
- 32 scenes (indoor objects, fabric, skin, food, etc.)
- Each scene contains 31 grayscale PNGs from 400nm to 700nm at 10nm intervals
- Each image is a 16-bit grayscale PNG
- Used as a real-world benchmark to test AWAN's generalization
- You can copy this folder into your Drive and try the model on the RGB folder:
https://drive.google.com/drive/folders/10kbbvLUQ4fSmEQ4cm_xt3VvN3zORsDax?usp=sharing
- You can use CAVE sample drive to process it yourself:
https://drive.google.com/drive/folders/1DbWTa7EOyvowKSsqGEqtYIUxMYhaadj3?usp=sharing
- Link for the entire DB:
https://cave.cs.columbia.edu/old/databases/multispectral/zip/complete_ms_data.zip
- Link for the Website:
https://cave.cs.columbia.edu/repository/Multispectral

### 🐘 2. **ImageNet-R**
This project focuses on converting **ImageNet-R RGB classes into a hyperspectral dataset** using the AWAN model.
-ImageNet-R
  - A rendition-style subset of ImageNet (cartoons, paintings, sketches, etc.)
  - Contains ~30,000 images across 200 classes
  - Used to test AWAN on visually diverse, non-photographic inputs
  - As a demonstration, the **first class (`n01443537`) containing 230 images** has been fully converted to 31-band hyperspectral format.
- You can also:
  - Convert any specific class by changing `cls_path`
    run "Choose specific class you want to convert"
  - Or sample randomly across all classes
    run "Sample randomly images from every class"
You can optionally test the model first on the **CAVE dataset** — but it's **not required** to use this workflow.

## ⚙️ How to Use

1. Run Utils and preperations to connect to Google Drive and install all the requirements
2. Check GPU- you must have GPU to use the model
3. Run **Model setup** and **Model loading and preperation**
4. **Use ImageNet-R** with the option you want. sampel from all classes or choose the class you want to convert from.
5. Optionally, test the model on the CAVE DB. Run **HS reconstruction from RGB and evaluation on CAVE DB**

- Use the model:
You can convert any RGB image by using 'RGB_2_HS(model, jpg_folder, reconstructed_folder)'. - Evaluation: You can Show evaluation by using 'output_evaluation_res(original_folder, reconstructed_folder)'.
- Visualization: You can visualize the result using the `show_hs_rgb()` function (selecting bands for R/G/B, e.g., 650/550/450nm). Or with HS_RGB_show() function that will visiualize the rgb image next to it's Hyperspectral constructed file.



@InProceedings{Li_2020_CVPR_Workshops,
author = {Li, Jiaojiao and Wu, Chaoxiong and Song, Rui and Li, Yunsong and Liu, Fei},
title = {Adaptive Weighted Attention Network With Camera Spectral Sensitivity Prior for Spectral Reconstruction From RGB Images},
booktitle = {The IEEE/CVF Conference on Computer Vision and Pattern Recognition (CVPR) Workshops},
month = {June},
year = {2020}
}
