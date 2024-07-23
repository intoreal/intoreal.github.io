---
layout: post
title: "PLT 고급 사용 예시"
date: 2024-07-24 +0900
categories: [python, plt]
tags: [python, matplotlib]
published: true
author: jihwan
toc: true
---

## 목표 그래프
![PLT figure](/assets/img/2024-07/plt-advance.png)

## 코드
```python
import matplotlib.pyplot as plt

# Data
batch_sizes = [1, 2, 4, 8, 16, 32, 64, 128]
ideal = [4, 4, 4, 4, 4, 4, 4, 4]
marlin = [4, 4, 4, 4, 4, 4, 4, 4]
torch_nightly = [3.5, 3.5, 3.2, 2.8, 2.5, 2, 1.5, 1.2]
exllamav2 = [3.8, 3.7, 3.5, 3.2, 3, 2.5, 2, 1.5]
awq = [3, 2.5, 2, 1.5, 1.2, 1, 0.8, 0.6]
bitsandbytes = [3.5, 2.5, 1.5, 1, 0.5, 0.3, 0.2, 0.1]

# Plotting
plt.figure(figsize=(12, 6))
plt.plot(batch_sizes, ideal, 'ko-', label='Ideal')
plt.plot(batch_sizes, marlin, 'bo-', label='Marlin')
plt.plot(batch_sizes, torch_nightly, 'o-', label='torch-nightly', color='orange')
plt.plot(batch_sizes, exllamav2, 'go-', label='exllamav2')
plt.plot(batch_sizes, awq, 'ro-', label='AWQ')
plt.plot(batch_sizes, bitsandbytes, 'mo-', label='bitsandbytes')

# Labels and Title
plt.xlabel('Batchsize')
plt.ylabel('Speedup over FP16 PyTorch (calling CUTLASS)')
plt.title('16bit×4bit (group=128) mul with 72k×18k matrix on NVIDIA A10')

# Set x-axis to log scale
plt.xscale('log')

# Set x-axis ticks to match batch_sizes
plt.xticks(batch_sizes, batch_sizes)

# Enable grid for major x-axis and y-axis only, then manually add vertical lines at each batch size
plt.grid(True, which="major", ls="--")

# Remove existing minor grid lines
plt.grid(False, which="minor")

# Add vertical lines at each batch size
for bs in batch_sizes:
    plt.axvline(x=bs, color='gray', linestyle='--', linewidth=0.5)

# Adjust y-axis limits to extend beyond the maximum y value
plt.ylim(0, 4.5)

# Adjust legend to be inside the plot and placed just above the horizontal grid line at y=4
plt.legend(loc='center', bbox_to_anchor=(0.5, 0.95), ncol=6, frameon=True)

# Adjust layout to make space for the legend
plt.tight_layout()

# Show plot
plt.show()


```