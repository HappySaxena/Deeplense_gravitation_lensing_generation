# &#x20;**Discussion of Strategy and Implementation**



### 1\. Data Preservation and Scaling Strategy

A primary goal of this implementation was to generate images that are indistinguishable from the provided dataset. While non-linear scaling methods like ArcSinh were explored to handle the high dynamic range typical of astronomical data, they were ultimately discarded. I found that such transformations altered the visual and statistical characteristics of the images compared to the ground truth. To ensure the model learned to replicate the exact "look and feel" of the training data, I opted for a more conservative scaling approach that maintained the original flux ratios. Furthermore, the entire pipeline operates on 32-bit float tensors, preventing the data loss and "posterization" effects that occur when converting scientific data into 8-bit formats.



### 2\. Architectural Evolution: Traditional vs. Equivariant DDPM

I implemented two distinct versions of the Denoising Diffusion Probabilistic Model (DDPM) to compare their effectiveness in capturing astrophysical structures:

Approach 1 (Traditional): A standard U-Net architecture. While capable of generating lensing-like features, it treats every orientation as a unique feature, requiring the model to "re-learn" the same physics at different angles.



Approach 2 (Equivariant): To leverage the inherent symmetries of gravitational lensing, I implemented a custom Group-Equivariant layer (SymConv2d). By enforcing C4 rotational symmetry through Reynolds averaging, the model treats rotated versions of the same mass distribution as fundamentally identical. This structural prior allows the model to generalize more effectively from the 10,000-image dataset.



### 3\. Quantitative Analysis (FID Scores)

The effectiveness of the Equivariant approach is reflected in the Fréchet Inception Distance (FID):

Traditional DDPM FID: 51.3931

Equivariant DDPM FID: 43.9150

The improvement in the FID score for the second approach suggests that the symmetry-aware architecture produces a distribution of images that more closely aligns with the real data. The reduced score indicates better capturing of the global geometric structures, such as the curvature of Einstein rings and the positioning of multiple images.



### 4\. Critique of Metrics and t-SNE Distribution

Despite the improvement in FID, the t-SNE feature distribution plots (Figures provided) show a distinct separation between the "Real Data" (blue) and "Generated Data" (red) clusters. While this often suggests a "model failure" in standard computer vision, in the context of physics-based generation, it highlights the limitations of the FID metric itself:

Inception Bias: The FID and t-SNE plots are based on InceptionV3 features, which were trained on natural images (animals, objects). The Inception network is sensitive to low-level textures, such as the specific grain of telescope noise, which the diffusion model tends to smooth out.



Feature Mismatch: The separation in t-SNE space likely indicates that the model has not perfectly replicated the stochastic background noise of the real images, even though it has captured the macro-scale lensing physics.

Metric Unsuitability: This result confirms that FID is an imperfect proxy for realism in astrophysics. A generated image may be physically perfect (satisfying lensing equations) but still appear "different" to a network trained on ImageNet. This underscores the need for domain-specific, physics-informed evaluation metrics that prioritize mass-density profiles and geometric consistency over generic pixel-level textures.



### Conclusion

By moving from a traditional architecture to an Equivariant DDPM, I achieved a significant gain in generation quality. The separation in the feature space serves as a valuable lesson: while equivariance improves the underlying structural generation, standard vision metrics like FID remain biased toward superficial textures rather than the underlying physical truth of the gravitational lens.

