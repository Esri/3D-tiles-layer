# LCC and LCC2 Format

---

## Quick Links

[Introduction](#introduction) <br />
[LCC format](#lcc-format) <br />

## Introduction

The [LCC](https://github.com/xgrids/LCCWhitepaper) and [LCC2](https://github.com/xgrids/LCC2Whitepaper) data organization format are developed by [XGRIDS](https://github.com/xgrids) to visualize Gaussian splatting.
XGRIDS high-precision real-time scanners are adopted in diverse industries allowing users to rapidly scan outdoor and indoor areas to generate Gaussian splat datasets.

## LCC format

The LCC format as described in the [LCC data organization format white paper](https://github.com/xgrids/LCCWhitepaper) provides high-fidelity solution for spatial data captured via Multi-SLAM technology. LCC files can be input to create Gaussian splat layer. For example, in ArcGIS Pro 3.8 the Create Gaussian Splat Layer Content geoprocessing tool allows you to define LCC files as input. If the LCC file contains meta data defining the spatial reference and data origin so the Gaussian splat layer will display the data in the correct spatial location.
