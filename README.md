# Image Processing Fundamentals | Option C

## Question

How do Gaussian noise and smoothing change the edge maps produced by Sobel and Canny on MATLAB's 256 × 256 grayscale sample image `cameraman.tif`? The sample is supplied by Image Processing Toolbox. This project contains the generated edge maps and uses the MATLAB installation's copy of the input.

## Environment and settings

The experiment ran in **MATLAB R2025b Update 3 (25.2.0.3123386)** with **Image Processing Toolbox 25.2**. The full version strings are in [matlab_version.txt](results/matlab_version.txt).

The noisy image was generated once with `rng(42); In = imnoise(I,'gaussian',0,0.01);`. Both images were processed independently with the three detectors below. Each call uses MATLAB's default automatic threshold selection.

| Method | MATLAB call for input `X` |
| --- | --- |
| Sobel after Gaussian smoothing, σ = 1 | `edge(imgaussfilt(X,1),'Sobel')` |
| Canny, σ = 1 | `edge(X,'Canny',[],1)` |
| Canny, σ = 3 | `edge(X,'Canny',[],3)` |

## Run the Live Script

1. Open the project folder in MATLAB R2025b with Image Processing Toolbox available. Set the current folder to the project folder.
2. Open [analysis.mlx](analysis.mlx) in Live Editor and click **Run** to execute all sections. The six maps, tables, chart and sky crop appear inline. The script regenerates the files in `results/`.
3. Save the Live Script to retain its outputs. Use **Export > PDF** with code and output visible if you need a fresh copy of [analysis.pdf](analysis.pdf).

## Results

| Edge pixels (`nnz`) | Sobel, Gaussian σ = 1 | Canny σ = 1 | Canny σ = 3 |
| --- | ---: | ---: | ---: |
| Clean | 2,099 | 7,816 | 2,780 |
| Noisy | 2,026 | 18,112 | 3,184 |

The [six edge maps](results/edge_maps.png) show how noise affected each configuration. In the [sky crop](results/region_inspection.png) at rows 20–65 and columns 165–225, Canny σ = 1 marks 0 pixels on the clean image and 916 on the noisy one. Noisy Canny σ = 3 and smoothed Sobel each mark 0 pixels in the same crop. Stronger smoothing retains the main outline but reduces fine background detail, so the appropriate scale depends on which boundaries matter.

The [counts](results/edge_counts.csv), [comparison](results/edge_comparison.csv) and [bar chart](results/edge_pixel_counts.png) quantify the change. A count measures the number of marked pixels. Evaluating accuracy requires annotated boundaries. A slight shift in a detected boundary can create pixels that appear in only one map.
