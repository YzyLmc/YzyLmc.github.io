---
layout: post
title: GASCN：Graph Attention Shape Completion Network
excerpt: A shape completion network utilizes graph attention and surface normal
# theme: simple

tags: [presentation]
category: presentation
---
_Haojie Huang, **Ziyi Yang**, Robert Platt*_

## Table of Contents
  * [3D Shape Completion](#3d-shape-completion)
  * [Related Works](#related-works)
  * [Model](#model)
    * [General Structure](#general-structure)
    * [Encoder Structure](#encoder-structure)
    * [Decoder Structure](#decoder-structure)
  * [Experiments](#experiments)
    * [Quantitative Result](#quantitative-result)
    * [Qualitative Result](#qualitative-result)
  * [More information](#more-information)

---
## 3D Shape Completion
3D shape completion from partial point clouds is a fundamental problem in computer vision and computer graphics. Recent approaches can be characterized as either data-driven or learning-based. Data-driven approaches rely on a shape model whose parameters are optimized to fit the observations. Learning-based approaches, in contrast, avoid the expensive optimization step and instead directly predict the complete shape from the incomplete observations using deep neural networks. [\[Stutz et al.\]](https://davidstutz.de/wordpress/wp-content/uploads/2018/04/shape-completion-cvpr2018-paper.pdf)

![shapecompletion](/images/pcn.png)
<center>A common shape completion task appears in daily life</center>
---
## Related Works
PointNet is a pioneer in using the MLP-based approach to learn point clouds. It combines pointwise multi-layer perceptrons with a max-pooling aggregation function to achieve invariance to permutation and robustness to perturbation. After PointNet, FoldingNet proposed a folding-based decoder that deforms a 2D grid onto the 3D surface of a point cloud. Following previous works, PCN proposed the coarse-to-fine procedure to densify the point cloud.  

However, these approaches just aggregated the global information from the whole point cloud without focusing on the local information of each point’s neighbors, neither did they take the various local properties of different points into account during the generation process. Compared with MLP-based approaches, graph-based methods could extract local information of each point. Most recent graph-based convolution methods operate on groups of spatially close neighbors. ECC is the first one to apply graph convolutions to point cloud classification. After that, DGCNN  proposed a more generalized edge convolution method with dynamic graph updates to encode the local neighborhood information for point clouds. Inspired by DGCNN, DCG introduced this method to point cloud completion following a coarse-to-fine fashion. However, the edge convolution is computation expensive in large graphs. After Graph Attention Network, GAC inherited its ideas to apply attention mechanism to the point cloud segmentation area.  

To the best of our knowledge, we are the first to directly combine the graph-level local information with the global structure information in the encoder and utilize surface normals to incorporate pointwise local properties for shape completion.

----
## Model
#### General Structure

![model_structure](/images/model.png)

The architecture of GASCN. It has a graph-based encoder that integrates each point’s local information with the point cloud’s global structure information. The decoding process utilizes surface normals and coarse points to rotate and translate adaptive 3D grids to densify coarse point clouds.
#### Encoder Structure
![encoder](/images/encoder.png)

Graph-based Encoder of GASCN model. It encodes each node feature with its neighbors’ information by graph attention layer, its mapped Cartesian feature by point-wise MLP, and two types of global vectors, extracted from the max-pooling operation.
#### Decoder Structure
![decoder](/images/decoder.png)

Decoder Architecture. The coarse points decoder consists of three fully connected layers. The normal decoder takes as inputs the mapped coarse point coordinate, its neighbors’ information, and the mapped global vector. The sigma decoder takes as inputs the normal internal embeddings, and then applies three pointwise MLP layers to output pointwise-attentive sigmas.

---
## Experiments
#### Quantitative Result
![quantitative](/images/quant.png)
Point completion results comparison on ShapeNet using Chamfer Distance (CD) with L2 norm computed on 16,384 points and multiplied by 10^3. The best results are highlighted in bold.
#### Qualitative Result
![qualitative](/images/quali.png)
Visual Results Comparison. A partial point cloud is given and our method generates better complete point clouds.

---
## More Information
The complete version of our paper is available at [here](https://drive.google.com/file/d/1VoMU8Q99GDv1KbkigsF-E3GQsozhlkIr/view). It's still under review, and we'll release the codes later.
