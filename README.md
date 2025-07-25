# **Website Technology Detector**

A comprehensive Python tool for identifying the technology stack of any website by combining backend and frontend analysis.

## **Table of Contents**

1. Project Goals
2. How It Works
3. Directory Structure
4. Setup and Installation
5. Usage
6. For Developers
7. Troubleshooting

## **1\. Project Goals**

The **Tech Detector** was built to provide a holistic view of a website's technology stack. It solves a common problem where a single scanner is often insufficient:

- **Backend scanners** (like WhatWeb) are excellent at identifying server-side technologies but often miss client-side libraries.
- **Frontend scanners** are great at identifying JavaScript frameworks but have no visibility into the server infrastructure.

This tool merges the strengths of both approaches to create a single, unified, and accurate report.

## **2\. How It Works**

The application uses a dual-engine analysis process:

- **Backend Detection:** A self-contained, **portable WhatWeb environment** performs an in-depth analysis of server-side technologies. This custom package requires no Docker or local Ruby installation, making the tool highly portable.
- **Frontend Detection:** A powerful **frontend analysis library** identifies client-side technologies like JavaScript frameworks, UI libraries, and analytics tools.

The results from both scanners are then intelligently merged, deduplicated, and normalized to produce a clean JSON output.

### **Understanding the WhatWeb Portable Environment**

A key component of this project is the backend scanner, **WhatWeb**. To ensure this tool works on any Windows machine without requiring complex setup (like Docker or a separate Ruby installation), we use a **self-contained, portable environment**.

- **What is it?** The WhatWeb-Portable folder, included in this repository, is a complete, pre-configured package that contains the WhatWeb source code, a portable Ruby interpreter, and all necessary dependencies.
- **Why this approach?** It guarantees that WhatWeb runs in the exact same, predictable environment on every machine, eliminating "it works on my machine" problems and making setup incredibly simple.

## **3\. Directory Structure**

The project is organized into distinct modules for clarity and maintainability:

tech_detector/  
├── backend_detection/ # Handles all WhatWeb scanning and analysis  
│ ├── bin/  
│ │ └── WhatWeb-Portable/ # The self-contained WhatWeb environment  
│ ├── core/  
│ │ └── whatweb_scanner.py # Python script that runs the scan  
│ └── ...  
├── frontend_detection/ # Handles all frontend scanning and analysis  
│ └── ...  
├── data/ # Data maps for technology categorization  
├── main.py # The main entry point to run the application  
├── requirements.txt # All Python dependencies for the project  
└── README.md # This documentation file  

## **4\. Setup and Installation**

Follow these steps to get the project running from scratch.

### **Step 1: Clone the Repository**

Clone this repository to your local machine. This will include the WhatWeb-Portable directory.

git clone &lt;your-repository-url&gt;  
cd tech_detector  

### **Step 2: Set Up the Python Environment**

It is highly recommended to use a virtual environment to manage project dependencies.

\# Create the virtual environment (named 'env')  
python -m venv env  
<br/>\# Activate the environment  
\# On Windows:  
.\\env\\Scripts\\activate  
\# On macOS/Linux:  
source env/bin/activate  

### **Step 3: Install Python Dependencies**

Install all the required Python packages from the requirements.txt file.

pip install -r requirements.txt  

The project is now fully set up and ready to run.

## **5\. Usage**

The main entry point for the application is main.py.

1. **Open main.py** in a code editor.
2. **Set the target URL** in the designated variable within the script.
3. **Execute the script** from the root of the project directory:  
    python main.py  

### **Expected Output**

The script will run both analyses and print a final, merged JSON object to the console.

{  
"Web frameworks": \["Django"\],  
"Web servers": \["Nginx"\],  
"CDN": \["Cloudflare", "Google Cloud"\],  
"JavaScript libraries": \["jQuery"\]  
}  

## **6\. For Developers**

### **Adding Custom WhatWeb Plugins**

The portable WhatWeb environment makes it easy to add custom detection plugins.

1. Navigate to the plugins directory:  
    backend_detection/bin/WhatWeb-Portable/WhatWeb/my-plugins/
2. Add your custom .rb plugin files to this folder. The scanner will automatically load them on the next run.

## **7\. Troubleshooting**

| **Error** | **Cause** | **Solution** |
| --- | --- | --- |
| FileNotFoundError: Could not find the launcher script... | The WhatWeb-Portable folder has been moved or renamed. | Ensure the folder is located at backend_detection/bin/WhatWeb-Portable/ as the script's path is hardcoded. |
| --- | --- | --- |
| ModuleNotFoundError | Python dependencies are not installed. | Activate your virtual environment and run pip install -r requirements.txt. |
| --- | --- | --- |
| WhatWeb command fails with a non-zero exit code. | The run_whatweb.bat script may have incorrect paths or permissions issues. | Verify the paths inside the .bat file match the directory structure.|
| --- | --- | --- |
