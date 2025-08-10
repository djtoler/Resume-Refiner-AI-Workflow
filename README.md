# Resume-Refiner-AI-Workflow


## Overview

#### _This AI agent workflow, made in N8N, was designed to give a user suggestions on how to modify their resume to better fit a given job description._


## AI Agent Flow Diagram

![Diagram](https://github.com/djtoler/Resume-Refiner-AI-Workflow/blob/main/images/n8n_diagram01.png)


## Building the Agent

![Workflow](https://github.com/djtoler/Resume-Refiner-AI-Workflow/blob/main/images/workflow.png)

#### _1. We start with a way to capture and input data into the system. In this case, we use a native N8N form to allow users to upload a resume, input a link to a job description and provide an email address to recieve results._

| Form | Form w/ data |
|---|---|
| ![Alt text for Image 1](https://github.com/djtoler/Resume-Refiner-AI-Workflow/blob/main/images/form2.jpeg) | ![Alt text for Image 2](https://github.com/djtoler/Resume-Refiner-AI-Workflow/blob/main/images/form1.jpeg) |

#### _2. The form in step 1 outputs a JSON object that we can use in our current HTTP node, which we use to access the HTML of a job description link a user submits. Then we implement a Code node that uses JavaSript to parse the HTML data._

| HTTP Node | Code Node |
|---|---|
| ![Alt text for Image 1](https://github.com/djtoler/Resume-Refiner-AI-Workflow/blob/main/images/http_node.jpeg) | ![Alt text for Image 2](https://github.com/djtoler/Resume-Refiner-AI-Workflow/blob/main/images/code_node.jpeg) |

#### _3. Next, we access the binary data of the PDF file to convert it to text, then we merge the text from the PDF with the output from the Code node (only relevant job description data), giving us a single output to pass to the AI Agent._

| Extraction Node | Merge Node |
|---|---|
| ![Alt text for Image 1](https://github.com/djtoler/Resume-Refiner-AI-Workflow/blob/main/images/extraction_node.jpeg) | ![Alt text for Image 2](https://github.com/djtoler/Resume-Refiner-AI-Workflow/blob/main/images/merge_node.jpeg) |

## Troubleshooting


## Optimization

