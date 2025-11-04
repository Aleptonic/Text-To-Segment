![Python 3.8+](https://img.shields.io/badge/python-3.8+-blue.svg)
![PyTorch](https://img.shields.io/badge/PyTorch-%23EE4C2C.svg?style=flat&logo=PyTorch&logoColor=white)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)

## Table of Contents
1. [Text-Driven Image Segmentation with SAM 2](#text-driven-image-segmentation-with-sam-2)
   - [Pipeline Overview](#pipeline-overview)
   - [Example Result](#example-result)
   - [How to Run](#how-to-run)
   - [Limitations](#limitations)
2. [Acknowledgements](#acknowledgements)
   - [Papers](#papers)
  
  # Text-Driven Image Segmentation with SAM 2

> This project implements a pipeline to perform segmentation on an image using an arbitrary text prompt. It demonstrates a powerful modern AI technique of composing two different state-of-the-art models, GroundingDINO and the Segment Anything Model (SAM 2), to achieve a task that neither can perform alone.

#### Pipeline Overview


<p align="center">
  <img src="https://github.com/user-attachments/assets/c09eb155-8308-493b-b60b-5f704eb7731d" alt="image" width="400" height="400" />
</p>

The system operates on a "Finder-Painter" principle:

1.  **Input:** The user provides an image and a free-form text prompt (e.g., "a person on a surfboard").
2.  **The "Finder" (GroundingDINO):** The text prompt is fed to the GroundingDINO model, an open-set object detector. It identifies and draws bounding boxes around the object(s) described in the text.
3.  **The "Painter" (SAM 2):** The original image and the bounding boxes from GroundingDINO are then passed to the Segment Anything Model. The boxes act as spatial prompts, guiding SAM to generate precise, pixel-perfect segmentation masks for the detected objects.
4.  **Visualization:** The final output overlays the generated masks and bounding boxes onto the original image, clearly highlighting the segmented object.



#### Example Result

Here is an example of the pipeline segmenting **"a skateboard"** and **"a cap"** from an image.

- **Text Prompt:**  
  `"skateboard, cap"`

<p align="center">
  <table>
    <tr>
      <td align="center">
        <img src="https://github.com/user-attachments/assets/11dbfb4f-364d-4903-8c25-e7fe905544a0" alt="Input image" width="400" height="400" style="border-radius:10px;" /><br>
        <sub><b>Input Image</b></sub>
      </td>
      <td align="center">
        <img src="https://github.com/user-attachments/assets/b612004e-cae7-4e8a-8fce-a87f68e90866" alt="Final output" width="400" height="400" style="border-radius:10px;" /><br>
        <sub><b>Final Output</b></sub>
      </td>
    </tr>
  </table>
</p>


#### How to Run

1.  Open the `q2_dino_sam.ipynb` notebook in Google Colab.
2.  Ensure the runtime is set to a **GPU** instance (`Runtime` > `Change runtime type`).
3.  Run all cells from top to bottom. The initial cells will handle all installations and model downloads.
4.  The final cell launches an interactive UI. Use the "Upload Image" button to select a local image, enter your desired object in the "Prompt" text box, and click "Run Segmentation".

#### Limitations

* **Dependency on Detection:** The final mask quality is entirely dependent on the initial bounding box from GroundingDINO. If the "Finder" fails to locate the object, the "Painter" has nothing to segment.
* **Ambiguous Prompts:** Vague text prompts (e.g., "the person") in a crowded scene can lead to multiple or incorrect detections, resulting in poor segmentation.
* **No Semantic Link in SAM:** SAM segments whatever is in the prompt box, it does not understand the text itself. If GroundingDINO incorrectly boxes a car when prompted for a "dog", SAM will diligently segment the car.

## Acknowledgements

This implementations were made possible by studying the following seminal papers and high-quality open-source repositories.

### Papers
1.  **Grounding DINO:** Skalski, P. (2023, March 30). *Grounding DINO: SOTA Zero-Shot Object Detection*. Roboflow Blog. [https://blog.roboflow.com/grounding-dino-zero-shot-object-detection/](https://blog.roboflow.com/grounding-dino-zero-shot-object-detection/)
2.  **Segment Anything Model (SAM):** Skalski, P. (2024, January 22). *How to Use the Segment Anything Model (SAM)*. Roboflow Blog. [https://blog.roboflow.com/how-to-use-segment-anything-model-sam/](https://blog.roboflow.com/how-to-use-segment-anything-model-sam/)
