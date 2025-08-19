# Autonomous AI Data Analyst Agent 🤖📊

This project is a sophisticated, autonomous AI agent capable of performing end-to-end data analysis tasks. It interprets natural language requests, dynamically formulates a plan after inspecting the raw data, and executes the necessary Python code in a secure, sandboxed environment to deliver the final analysis.

*You can add a GIF of your Streamlit app in action here!*
`![Agent Demo GIF]`

---

## About The Project

The goal of this project was to overcome the limitations of traditional "plan-then-execute" AI agents, which often fail when they have to operate on unseen, real-world data. This agent implements a more advanced **"See, then Plan, then Act"** architecture. It first gathers raw data, inspects it to understand its structure and content, and *then* generates a detailed, data-aware plan for cleaning, analysis, and final answer generation.

This approach, combined with a self-correcting execution loop, makes the agent significantly more robust and capable of handling the complexities and inconsistencies of real-world data.

### Key Features

* **🧠 Dynamic Multi-Stage Planning:** The agent first performs a data gathering phase to create a raw DataFrame. It then analyzes a preview of this messy data to generate a second, more intelligent and accurate plan for the final cleaning and analysis steps.

* **🔒 Secure Sandboxed Code Execution:** All AI-generated Python code is executed in an isolated **Docker** container. This provides a secure environment that prevents the code from accessing the host file system or network, allowing for the safe execution of complex data manipulation tasks with **Pandas**.

* **🔁 Intelligent Self-Correction Loop:** The agent is built for resilience. If a piece of AI-generated code fails, the agent captures the error and a snapshot of the data state, sends this rich context back to an AI "debugger" prompt, and attempts to run the newly corrected code, retrying up to 3 times.

* **📄 Multi-Modal Input with OCR:** The **FastAPI** endpoint can accept both text files and image uploads. An OCR pipeline using **Pytesseract** extracts text from images, which is then combined with the text prompt to form a complete user request.

* **🌐 Interactive User Interface:** A user-friendly web application built with **Streamlit** provides a front-end to the agent, allowing non-technical users to upload their requests and view the final, structured answer in real-time.

---

### ## Tech Stack

* **Python**
* **AI & Agentic Frameworks:** Large Language Models (Google Gemini API)
* **Backend & API:** FastAPI, Uvicorn
* **Frontend & UI:** Streamlit
* **Containerization & Sandboxing:** Docker
* **Data Manipulation:** Pandas
* **Web Scraping & Automation:** Selenium
* **OCR:** Pytesseract, Pillow

---

## Getting Started

Follow these steps to get a local copy up and running.

### Prerequisites

* Python 3.10+
* **Docker Desktop:** Make sure it is installed and running on your system.
    * [Download Docker Desktop](https://www.docker.com/products/docker-desktop/)
* **Tesseract OCR Engine:** (Required for the API's image upload feature)
    * On macOS: `brew install tesseract`
    * On other systems, follow the [official Tesseract installation guide](https://tesseract-ocr.github.io/tessdoc/Installation.html).

### Installation

1.  **Clone the repository:**
    ```sh
    git clone [https://github.com/your_username/your_repository_name.git](https://github.com/your_username/your_repository_name.git)
    cd your_repository_name
    ```

2.  **Create and activate a virtual environment:**
    ```sh
    python3 -m venv venv
    source venv/bin/activate
    ```

3.  **Install Python dependencies:**
    ```sh
    pip install -r requirements.txt
    ```
    *(Note: If you don't have a `requirements.txt` file, you can create one from your working virtual environment with `pip freeze > requirements.txt`)*

4.  **Build the Docker Sandbox Image:**
    ```sh
    docker build -t data-analyst-sandbox .
    ```

5.  **Set up your Environment Variables:**
    Create a file named `.env` in the root directory and add your API key:
    ```
    GOOGLE_API_KEY="YOUR_GOOGLE_GEMINI_API_KEY"
    ```

---

## Usage

You can interact with the agent in two ways:

### 1. Via the API Server

1.  **Run the FastAPI server:**
    ```sh
    uvicorn main:app --reload
    ```
2.  The API will be available at `http://127.0.0.1:8000`. You can access the interactive documentation at `http://127.0.0.1:8000/docs`.

3.  **Send a request using `curl`:**
    Make sure you have a `question.txt` file with your request.
    ```sh
    curl -X POST "[http://127.0.0.1:8000/analyse/](http://127.0.0.1:8000/analyse/)" -F "question_file=@question.txt"
    ```

### 2. Via the Streamlit Web App

1.  **Run the Streamlit app:** (Assuming your Streamlit code is in a file named `app.py`)
    ```sh
    streamlit run app.py
    ```
2.  Open your web browser to the local URL provided by Streamlit.
