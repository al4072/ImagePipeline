# Real-Time LiDAR Perception Pipeline

An end-to-end 3D perception pipeline that detects and tracks vehicles from raw LiDAR point cloud data in real time. Built to isolate vehicle positions from noisy point cloud scans and maintain stable tracking across frames.

## Key Results

- Processed 500+ point clouds through the full pipeline (segmentation → clustering → filtering → tracking)
- Improved multi-metric tracking performance from 20/80 to 40/80, evaluated across localization accuracy, motion consistency, and bounding box accuracy
- Designed a 6-constraint geometric filter that eliminates false-positive detections using point count, height, XY dimensions, and ground-relative position

## Pipeline Overview

1. **Voxel Downsampling** — reduces point cloud density while preserving structure, for faster downstream processing
2. **RANSAC Ground Segmentation** — separates ground plane points from object points
3. **DBSCAN Clustering** — groups remaining points into candidate object clusters
4. **Geometric Filtering** — applies a 6-constraint check (point count, height, XY extent, ground-relative position, etc.) to reject non-vehicle clusters
5. **Tracking** — matches clusters across frames using the Hungarian algorithm, with dead-reckoning prediction to bridge frames with missed detections

## Tech Stack

- Python
- Open3D (point cloud processing)
- NumPy
- SciPy (`linear_sum_assignment` for Hungarian algorithm matching)

## Repo Structure

```
├── data/           # sample point cloud frames [update to match your actual layout]
├── src/
│   ├── segmentation.py
│   ├── clustering.py
│   ├── filtering.py
│   └── tracking.py
├── notebooks/      # exploration / visualization notebooks, if any
├── requirements.txt
└── README.md
```

## Setup

```bash
git clone https://github.com/AAzurez/<repo-name>.git
cd <repo-name>
pip install -r requirements.txt
```

## Usage

```bash
python src/main.py --input data/sample.pcd   # [update to your actual entry point / args]
```

## Results

Tracking performance improved from a baseline score of 20/80 to 40/80 (2x) across three evaluation dimensions: localization accuracy, motion consistency, and bounding box accuracy, after adding Hungarian algorithm assignment and dead-reckoning prediction.
