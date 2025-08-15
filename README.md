# Lecture Lens: Automated Note Generation from Video Lectures

## 💡 Overview

Lecture Lens is a Python-based project designed to automate the process of generating high-quality lecture notes. It takes a collection of video files and their corresponding presentation slides (in PDF or PPTX format), transcribes the audio, extracts text from the slides, and then uses a Large Language Model (LLM) to synthesize a comprehensive, well-structured set of academic notes.

This tool is ideal for students, researchers, and educators who need to quickly create organized study materials from raw lecture content.

## ✨ Features

* **Audio Extraction:** Converts video files (MP4, MKV) into high-quality WAV audio files using `ffmpeg`.

* **Speech-to-Text Transcription:** Transcribes the extracted audio into text using the powerful `Whisper` model from Hugging Face.

* **Presentation Content Extraction:** Extracts text, titles, and presenter notes from PowerPoint (`.pptx`) and PDF (`.pdf`) files.

* **LLM-Powered Synthesis:** Integrates transcripts and presentation content using a large language model (like Gemini or Llama 3) to create synthesized lecture notes in Markdown format.

* **Scalable Processing:** Implements a chunking strategy to handle long lectures that exceed the context window of the LLM, ensuring that even lengthy content can be processed effectively.

* **Structured Output:** Generates clean, organized notes with clear headings, bullet points, and bolded keywords, optimized for easy learning and review.

## ⚙️ How It Works

The workflow is broken down into the following stages:

1. **Environment Setup:** Installs all necessary libraries and checks for GPU availability to accelerate processing.

2. **Audio Extraction:** Processes a directory of video files and saves the extracted audio as WAV files.

3. **Transcription:** Utilizes a state-of-the-art speech-to-text model (`Whisper-medium` is configured by default) to generate a detailed transcript for each audio file.

4. **Presentation Processing:** Extracts structured text content from all PDF and PPTX files in the dataset.

5. **Note Generation:** For each lecture, the script combines the generated transcript and the extracted presentation content.

   * If the content is too long for a single API call, it is split into smaller, overlapping chunks.

   * Each chunk is passed to an LLM (currently configured for Gemini or Llama 3) with a detailed prompt that guides the model to produce academic-quality notes.

   * The notes from all chunks are then combined into a single Markdown file.

## 🛠️ Prerequisites

* Python 3.8+

* A Google or Groq API key for the LLM.

* A Kaggle environment is recommended, as the notebooks are written for that environment, with dependencies managed via Kaggle's secrets and dataset features.

## 🚀 Getting Started

1. **Clone the repository:**

   ```bash
   git clone [https://github.com/your-username/lecture-lens.git](https://github.com/your-username/lecture-lens.git)
   cd lecture-lens
   
   ```

2. **Set up your environment:**
   The notebooks are designed to be run on Kaggle. You will need to upload your video and presentation files as a Kaggle dataset.

3. **Run the notebooks:**

   * **`lecture_lens_part1.ipynb`:** This notebook handles the data preparation pipeline: environment setup, audio extraction, transcription, and presentation content extraction.

   * **`lecture_lens_part2.ipynb`:** This notebook focuses on the LLM-driven note generation. It sets up the LLM, defines the prompting strategy, and processes the pre-processed data to create the final Markdown notes.

## 📂 Project Structure

```
.
├── lecture_lens_part1.ipynb      # Data Preprocessing: Audio/PPTX/PDF to Text
├── lecture_lens_part2.ipynb      # LLM Processing: Text to Final Notes
├── data/                       # Your raw lecture files (videos, presentations)
└── output/
    ├── [subject_name]/
    │   ├── audio/              # Extracted WAV files
    │   ├── transcripts/        # Generated TXT transcripts
    │   ├── presentation_data/  # Extracted JSON from presentations
    │   └── final_notes/        # Final Markdown lecture notes
```
