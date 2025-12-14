DS_TASK_PS03 — Visual Search, Retrieval & Detection
===================================================

Satellite Image Chip-Based Object Matching Using Deep Feature Embeddings
------------------------------------------------------------------------

This repository contains a complete, working solution for DS_TASK_PS03.  
The goal is to perform visual search and retrieval across large multi-spectral satellite TIFF images using small exemplar chips.  
The system extracts chip embeddings using a deep neural network and searches for visually similar regions in a sliding-window manner.

This repository follows all official task requirements.

---------------------------------------------------
Repository Structure
---------------------------------------------------

notebook.ipynb             -> Final polished Jupyter Notebook for submission  
tiff_results.txt           -> Detection results from sliding window TIFF search  
custom_results.txt         -> Detection results for custom chip search  
README.txt or README.md    -> This documentation  
data/                      -> The given data in the question


---------------------------------------------------
Problem Overview
---------------------------------------------------

The task requires designing a system that:

1. Accepts sample chips or bounding-box-selected regions.
2. Extracts features from the chip using a deep model (ResNet18).
3. Searches through multi-spectral TIFF images for visually similar matches.
4. Produces detections in the required output format:

xmin ymin xmax ymax object_name image_filename similarity_score

The similarity score is produced using cosine similarity between embedding vectors.


---------------------------------------------------
Technical Approach
---------------------------------------------------

1. ResNet18 Feature Extraction
   - Pretrained ResNet18 is used.
   - Final FC layer is removed.
   - Embeddings are 512-dimensional.

2. Memory-Safe TIFF Handling
   - TIFFs can exceed 10,000×10,000 pixels.
   - Entire TIFF is never loaded into memory.
   - Images are processed tile-by-tile (1024×1024).

3. Bounding Box Scaling
   - JSON annotations correspond to the full TIFF size.
   - Preview images are scaled down.
   - Bounding boxes are scaled using a preview_scale factor.

4. Sliding Window Search
   - Window size: 128×128
   - Stride: 64 px
   - Similarity threshold: 0.7
   - Applied on each tile independently.

5. Custom Chip Search
   - Uses obj_1.jpg as query.
   - Searches inside annotated.jpg.


---------------------------------------------------
Notebook Contents
---------------------------------------------------

The notebook is divided into the following sections:

1. Imports & Setup
2. TIFF Preview Loading
3. JSON Annotation Parsing
4. Bounding Box Scaling
5. Chip Extraction
6. Feature Extraction (ResNet18)
7. Sliding Window Search
8. Tile-Based TIFF Search
9. Visualization
10. Output File Generation
11. Custom Chip Search


---------------------------------------------------
Output Files
---------------------------------------------------

The system generates two output text files:

tiff_results.txt
custom_results.txt

Both follow the required space-delimited format:

xmin ymin xmax ymax class_name image_filename similarity_score


---------------------------------------------------
How to Run
---------------------------------------------------

1. Place TIFF, JSON, and query images inside a folder named:

   data/

2. Open arms4ai1.ipynb.
3. Run all cells in order.
4. Output files will be generated automatically:
   - tiff_results.txt
   - custom_results.txt

I personally did it on Google Colab due to memory constraints 
of my local computer. I would also advise to import all files to 
google colab and run the .ipynb file to get the desired 
results.

---------------------------------------------------
Dependencies
---------------------------------------------------

python >= 3.8  
torch  
torchvision  
opencv-python  
rasterio  
tqdm  
numpy  
matplotlib  

Install with:

pip install torch torchvision opencv-python rasterio tqdm matplotlib


---------------------------------------------------
Author
---------------------------------------------------

Ankit Kumar Singh 
Email: ankitkumar_24afi23@dtu.ac.in
Personal Email: ankitkusingh33@gmail.com
GitHub:   https://github.com/AnkitJr2608/DS_TASK__PS03_AnkitKumarSingh


---------------------------------------------------
End of Documentation
---------------------------------------------------
