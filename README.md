# Transforming-Photography-into-Pixel-Art
This study introduces a novel approach for converting standard photographs into pixel art using Generative Adversarial Networks (GANs), addressing the time and skill constraints in pixel art creation for video game development. We employ CycleGAN with enhancements, including CycleGAN with Learned Perceptual Image Patch Similarity (CycleGAN + LPIPS), CycleGAN with channel attention layer (CycleGAN + Attention) and CycleGAN integrated with Variational Autoencoders (CycleGAN + VAE) to conduct landscape and face pixel art transformation. Our results reveal that the CycleGAN + Attention approach notably excels in landscape pixel art by closely matching the color tone of traditional pixel art styles, and in human faces, it precisely captures artistic strokes and expresses facial features with good accuracy. 

## Problem statement
In contemporary independent video game development, pixel art has experienced a notable revival, attributed to its minimalist aesthetic. Despite its appeal, the creation of pixel art is a time-intensive and skill-dependent process. This poses a significant challenge in an industry increasingly geared towards efficiency and rapid prototype development. Our research proposes an innovative solution to this challenge: an automated system for transforming standard photographs into pixel art using Generative Adversarial Networks (GANs). Existing methods for converting photos to pixel art face limitations, especially in accurately reproducing color tones, impacting the final quality. By learning from unpaired images, GANs-based approach can overcome these challenges, facilitating high-quality and efficient pixel art transformations. The input and output of our system are shown as follows:
input: A photograph from any source in standard image formats.
output:A pixel art representation of the input image.

## Solution
###CycleGan
CycleGAN is a framework designed for learning image-to-image translation from unpaired datasets. Its architecture incorporates two generators and two discriminators, as illustrated in Figure 1. In our CycleGAN framework, 'Real A (Pixel Art)' refers to genuine pixel art images and 'Real B (Photos)' to actual photographs. We use two generators, both based on ResNet networks: Generator B inputs Real B (Photos) and aims to produce Fake A (pixel art-like images), testing its ability to create outputs indistinguishable by Discriminator B. Similarly, Generator A inputs Real A (Pixel Art) and strives to generate Fake B (photo-like images), with the goal of convincing Discriminator A of their authenticity. This setup facilitates efficient unpaired image-to-image translation between the pixel art and photographic domains.

CycleGAN utilizes cycle consistency for training with unpaired data. Rec B reconstructs original photos from generated pixel art (Fake A), while Rec A reconstructs original pixel art from generated photos (Fake B), each incurring a cycle consistency loss. Essentially, the Pixel Art Generator converts pixel art to photos, and the Photo Generator does the reverse. This process, illustrated in Figure 1, ensures image conversion fidelity, with discriminators and loss functions guiding quality and consistency in the photo-to-pixel art conversion.


To enhance the simulation results of the CycleGAN model, we have implemented the following three distinct improvements.
![Figure 1. CycleGAN workflow.](https://github.com/ASmellyCat/Transforming-Photography-into-Pixel-Art/assets/110814688/002799aa-390b-42a1-87d6-207f1875b79a)


###CycleGan+Attention
Our study primarily addresses a key limitation in the basic CycleGAN method, which often results in color inconsistencies during image translations (see result 3.1). Attention, which allows a model to focus on the most relevant parts of the input when generating output, might alleviate this problem. Therefore, We introduce a channel attention mechanism within the model. This channel attention, particularly integrated into the end of decoder stages of the generator's ResNet, most informative features by re-weighting the channels of the input data, thereby preserving the original colors in essential parts of the image and significantly reducing unnatural color shifts.

###Dataset
Our training and testing datasets are categorized into two primary groups: landscapes and human faces. For landscapes, we compiled 700 pixel art images (Real A) and 2,000 landscape photos (Real B) from the internet, resized them to 256x256, and applied data augmentation including flips, translations, and rotations. In the human faces category, Real A contains 300 pixel art faces sourced online, resized to 256x256 and augmented with horizontal flips. The 6000 Real B images for human faces was obtained from the open-source Kaggle dataset (https://www.kaggle.com/datasets/yewtsing/pretty-face).


##Result
###Landscape
In the first part of our project, we focused on the relatively straightforward task of transforming landscape photographs into Pixel Art. The outcomes of this process are displayed in Figure 2. Each case reveals distinct characteristics and levels of success in capturing the essence of Pixel Art style.
![Figure 2: Comparison of different CycleGAN models for landscape photo-to-Pixel Art transformation.](https://github.com/ASmellyCat/Transforming-Photography-into-Pixel-Art/assets/110814688/febfcb7b-8e9c-4d36-b94e-7d551eb186c2)

The Pixel Art effect in the baseline CycleGAN case is achieved but with a compromise on color fidelity and subject definition. However, a tendency towards color distortion and a lack of detail clarity in the subject matter are noted. CycleGAN + Lpips case results in a moderate enhancement. There is a reduction in color distortion compared to the baseline model, while the improvement in the clarity of the subject is limited. 
CycleGAN + Attention  case exhibits a significant improvement in capturing the color palette characteristic of Pixel Art. The attention layer effectively focuses on salient features, thus not only pixelating the subject but also refining the color scheme to align with the distinctive hues associated with the Pixel Art genre.
CycleGAN + VAE case has led to the most accurate color reproduction compared to the input photographs, but lack of artistic expression. 

###Face
In the second part of our project, we delved into the intricate challenge of converting human faces into Pixel Art. The outcomes of this phase are illustrated in Figure 3.
![Figure 3. Comparison of different CycleGAN models for face photo-to-Pixel Art transformation.](https://github.com/ASmellyCat/Transforming-Photography-into-Pixel-Art/assets/110814688/beee7b51-078c-47bc-9ac8-3f839c497f3f)
The baseline CycleGAN model could generally produce recognizable pixel art, yet the color tones tended to be somewhat dull and facial features were not distinctly clear. It also produced some superfluous information in the generated images. The CycleGAN + LPIPS variant showed a slight improvement in clarity and naturalness of skin tones. The CycleGAN + Attention model notably excelled, adeptly capturing the nuanced brushstrokes and vibrant color palette characteristic of the training dataset's pixel art style. It particularly stood out in its precise rendering of facial features, offering clarity and artistic value that closely mirrored the aesthetics of traditional pixel art.  While the CycleGAN + VAE variant effectively replicated the photo's appearance, it was less successful in emulating the artistic strokes of the training set's pixel art style. This analysis reflects a rigorous and precise assessment of each model's capabilities in transforming photos into pixel art.

##Conclusion
In conclusion, each model brings its unique strengths to the photo-to-Pixel Art transformation process.  The CycleGAN + Attention variant stands out by offering a balanced approach with its color alignment and attention to detail. Additionally, the CycleGAN + Attention excels in simulating human faces, offering a clearer and more precise depiction of facial features. The CycleGAN + LPIPS shows improvement over the baseline but is outperformed by the other enhancements.

