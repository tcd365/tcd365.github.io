# Temporal Calibrating and Distilling for Scene-Text Aware Text-Video Retrieval

## [1/9] Task Introduction


<div style="display: flex; justify-content: space-between;">
    <figure>
        <img src="images/task.png" alt="Introduction Image" style="width: 100%;">
    </figure>
</div>

<p align="justify">
<b>Figure 1:</b> (a) Existing methods overlook fine-grained scene text in videos. (b) SOTA method treats scene text as isolated instances, resulting in token imbalance issue that limits fine-grained interactions. (d) Our window-OCR captioner condenses scene text into OCR captions, achieving better performance with lower complexity (c).
</p>

### Examples in the TextVR Dataset
<style>
  .video-grid {
    display: grid;
    grid-template-columns: repeat(auto-fill, minmax(350px, 1fr));
    gap: 25px;
    margin: 20px;
  }
  .grid-item {
    background: #fff;
    border: 1px solid #e2e8f0;
    border-radius: 8px;
    overflow: hidden;
    box-shadow: 0 4px 6px -1px rgba(0,0,0,0.05);
  }
  .grid-header {
    padding: 15px;
    background: #f8fafc;
    border-bottom: 1px solid #e2e8f0;
    font-weight: 500;
  }
  .grid-video {
    padding: 15px;
    text-align: center;
  }
  .video-label {
    display: block;
    margin-top: 8px;
    font-size: 14px;
    color: #666;
    font-style: italic;
    text-align: center;
  }
</style>

<div class="video-grid">
  <div class="grid-item">
    <div class="grid-header">Query Text: The gold medalist from the cycling sports branch is Jason Kenny.</div>
    <div class="grid-video">
      <video controls width="330" height="170">
        <source src="video/5jKLoEt7RBg_00000_00010.mp4" type="video/mp4">
      </video>
      <span class="video-label">Target Video</span>
    </div>
  </div>
  <div class="grid-item">
    <div class="grid-header">Query Text: The store TESCO express offers fresh vegetables.</div>
    <div class="grid-video">
      <video controls width="330" height="170">
        <source src="video/i-DkWPfL4N4_00090_00105.mp4" type="video/mp4">
      </video>
      <span class="video-label">Target Video</span>
    </div>
  </div>
</div>



## [2/9] Model Architecture
![TCD Model Architecture](images/TCD.png)

<p align="justify">
<b>Figure 2:</b> 
Pipeline of <b>TCD</b>. Window-OCR captioner condenses abundant scene text into OCR captions. Heterogeneous semantics calibrating leverages scene text present in both video and OCR captions as a self-supervised signal for temporal alignment. Context-guided temporal clue distilling assigns each modality a learnable clue token to extract clear temporal clues.
</p>



<!-- <div style="display: flex; justify-content: space-between;">
    <figure>
        <video controls style="width: 100%;">
            <source src="video.mp4" type="video/mp4">
            Your browser does not support the video tag.
        </video>
    </figure>
</div> -->

## [3/9] Window-OCR Captioner 🌟🌟🌟

<div style="display: flex; justify-content: space-between;">
    <figure>
        <img src="images/Visualization_demo.gif" alt="New Visualization" style="width: 100%;">
    </figure>
</div>
<p align="justify">
<b>Figure 3:</b> Visualization of the proposed Window-OCR Captioner. We aggregrate different kinds of scene texts appearing within a window length of ∆t into a single caption to reduce the feature length from N in previous works (e.g., StarVR [53]) to 1.
</p>

## [4/9] Visualization of Our Window-level Sampling Strategy

<div style="display: flex; justify-content: space-between;">
    <figure>
        <img src="images/OCR_ratio.png" alt="New Visualization" style="width: 100%;">
    </figure>
</div>
<p align="justify">
<b>Figure 4:</b> Our window-level sampling strategy samples scene text using non-overlapping sliding windows. We sample scene text with a window centered around each video frame. Here, a larger window length value corresponds to sampling more scene text. 
</p>

## [5/9] Heterogeneous Semantics Calibrating

<div style="display: flex; justify-content: space-between;">
    <figure>
        <img src="images/HSC_demo.gif" alt="HSC demo" style="width: 100%;">
    </figure>
</div>
<p align="justify">
<b>Figure 5:</b> Demo of the proposed Heterogeneous Semantics Calibrating. We leverage heterogeneous scene text as the calibration signal to align sequences with different time-scales. The nearest semantic match follows the highest similarity score between the element in the first sequence and each element in the second sequence.
</p>

<!-- <div style="display: flex; justify-content: space-between;">
    <figure>
        <video controls style="width: 100%;">
            <source src="video2.mp4" type="video/mp4">
            Your browser does not support the video tag.
        </video>
    </figure>
</div> -->


## [6/9] Text→Video Retrieval Results (1/2)
![Text→Video Retrieval (1/2)](images/t2v_2.png)
<p align="justify">
<b>Figure 6:</b> Visualization of retrieval results comparing our method (left) with the model without OCR information (right). Sim indicates the overall similarity
score, calculated as the average of text-OCR, text-video, and text-hybrid matching scores, denoted as OCR, Video, and Hybrid, respectively. Our TCD captures fine-grained scene text, such as "GRILL" and "Thank you" with high similarity and hybrid scores. Please zoom in for a better view of the details.
</p>

## [7/9] Text→Video Retrieval Results (2/2)
![Text→Video Retrieval (2/2)](images/t2v_1.png)
<p align="justify">
<b>Figure 7:</b> Visualization of retrieval results comparing our method (left) with the model without OCR information (right). Sim represents the overall similarity
score, calculated as the average of text-OCR, text-video, and text-hybrid matching scores, denoted as OCR, Video, and Hybrid, respectively. Our TCD captures fine-grained scene text, such as "SAC MIA", "School", and "SDY 288H" with high similarity and hybrid scores. Please zoom in for a better view of the details.
</p>

## [8/9] Appendix
![Appendix-1](images/pdf/appendix_1.png)
![Appendix-1](images/pdf/appendix_2.png)
![Appendix-1](images/pdf/appendix_3.png)
![Appendix-1](images/pdf/appendix_4.png)

## [9/9] Abstract
<div style="text-align: justify;">
Existing text-video retrieval methods mainly focus on single-modal video content (i.e., visual entities), often overlooking heterogeneous scene text that is ubiquitous in human environments. Although scene text in videos provides fine-grained semantics for cross-modal retrieval, effectively utilizing it presents two unique challenges: (1) Temporally dense scene text disrupts sync with sparse video frames, obstructing video understanding; (2) Redundant scene text and irrelevant video frames hinder the learning of discriminative temporal clues for retrieval. In this paper, we address these challenges by proposing a temporal scene-text calibrating and distilling (TCD) network for text-video retrieval. Specifically, we first design a window-OCR captioner that aggregates dense scene text into OCR captions to facilitate feature interaction. Next, we devise a heterogeneous semantics calibration module that leverages scene text as a self-supervised signal to temporally align window-level OCR captions and frame-level video features. Further, we introduce a context-guided temporal clue distillation module to learn the complementary and relevant details between scene text and video modalities, thereby obtaining discriminative temporal clues for retrieval. Extensive experiments show that the proposed TCD achieves state-of-the-art performance on three scene-text related benchmarks.
</div>

**The source code and trained models will be released soon.**
