# reflection_removal_ai
![image](https://github.com/user-attachments/assets/0d0c0b0a-ea27-4182-98bd-fb36c12e0c25)


# Enhancements to FunieGAN Model for Image Enhancement

This project enhances the **FunieGAN** model by modifying the Generator and introducing additional image processing techniques. Below is a breakdown of all the key enhancements made to the original implementation.

## **1. Model-Specific Enhancements**

- **Removed Discriminator for Faster Inference**: The original FunieGAN model used a **Generator-Discriminator** pair, but in this implementation, only the **Generator** is used. This reduces computational overhead while still maintaining high-quality enhancements.
- **Standalone Generator Usage**: The Generator is treated as a standalone image-to-image enhancement model rather than part of a full GAN framework.
- **Compensated for Missing Discriminator**: Since the Discriminator is not used to assess output quality, additional image processing techniques (listed below) were added to refine the results.

## **2. Improvements in the Generator Model**

- **Modified the UNetUp Layer**: 
  - Ensured **spatial size consistency** between layers by applying `F.interpolate()` when required. 
  - This prevents shape mismatches and ensures seamless feature propagation.
- **Refined Final Upsampling Layer**: 
  - Used `nn.Upsample(scale_factor=2)` instead of transposed convolutions for more stable upscaling.
  - Maintained zero padding and `nn.Conv2d` for output generation.

## **3. Image Preprocessing Enhancements**

- **Original Size Preservation**: Before transformation, the original image size is stored and restored after model processing to prevent resolution distortions.
- **Improved Normalization Strategy**: Used `transforms.Normalize(mean=[0.5, 0.5, 0.5], std=[0.5, 0.5, 0.5])` for better stability and contrast enhancement.

## **4. Post-Processing Enhancements**

To improve the quality of the generated images, multiple **post-processing techniques** were added:

- **Contrast Limited Adaptive Histogram Equalization (CLAHE)**: 
  - Enhances local contrast without over-amplifying noise.
- **White Balance Correction**: 
  - Adjusts color temperature by averaging LAB color channels.
- **Denoising with Bilateral Filtering**: 
  - Smooths the image while preserving edges to remove unwanted noise.
- **Image Sharpening**: 
  - Uses `ImageEnhance.Sharpness` with an enhancement factor of `2.0` for better texture details.

## **5. Practical Implementation Enhancements**

- **Optimized for Real-World Use**: Since the model runs only the Generator and applies additional processing, it is significantly **faster** than a full GAN setup.
- **Lightweight and Efficient**: Reduces memory and computational load while achieving high-quality results.
- **Automated Image Enhancement Pipeline**: The framework automatically enhances images with minimal manual intervention.

## **Conclusion**

These enhancements improve **speed, stability, and quality** while making FunieGAN more practical for real-world **underwater image enhancement** or general low-light image restoration tasks. The combination of **deep learning and traditional image processing** ensures optimal results without requiring adversarial validation.

---

