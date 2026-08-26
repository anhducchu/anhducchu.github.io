---
title: "Research"
layout: post
weight: 20
build:
  render: never
  list: local
---

**AI4LIFE Lab, Hanoi University of Science and Technology**  
Undergraduate Researcher  
*2024 – Present*
- Supervisor: Assoc. Prof. Nguyen Phi Le

*Physics-aware diffusion models for medical imaging*
- Investigated SPECT acquisition physics to develop a CT-free attenuation correction method for myocardial perfusion imaging
- Implemented diffusion and GAN-based baselines for NAC-to-AC image translation on 73,680 cardiac SPECT slices, achieving 13.83% RMSE improvement over state of the art

*Optimal transport for cross-modal knowledge distillation*
- Co-designed the first cross-modal knowledge distillation framework for unpaired audio-visual data
- Aligned feature and prediction distributions across modalities using bilevel optimization with Wasserstein optimal transport
- Implemented the full training pipeline and validated the theoretical bounds across 4 benchmarks (VGGSound, 200,000+ videos, ViT up to 300M parameters)
- Achieved 14.3% over cross-entropy and 7.5% over feature distillation on all 8 unpaired tasks; ranked 1st on 4 of 6 paired tasks

*Theory of long-tailed generation in diffusion models*
- Deriving theoretical lower bounds on tail-class generation error for conditional DDPMs, characterizing regimes where classifier-free guidance provably fails on rare classes
