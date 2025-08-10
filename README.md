# Resume-Refiner-AI-Workflow

##### _Production Link:_ https://djtolerkura.app.n8n.cloud/form/a0fd0f52-8be7-4c0b-b5c6-901ae7f7e59e

--- 


## Overview

#### _This AI agent workflow, made in N8N, was designed to give a user suggestions on how to modify their resume to better fit a given job description._


## AI Agent Flow Diagram

![Diagram](https://github.com/djtoler/Resume-Refiner-AI-Workflow/blob/main/images/n8n_diagram01.png)


## Building the Agent

##### _We approach building the workflow by starting with considering the desired output (resume modification suggestion), ask what input data (resume, job posting link & email address) do we need to get the desired output & how should we process our input data to get our desired output._

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

#### _4. Finally, we pass the single merged output (job description data w/ resume text), to our OpenAI AI Agent that'll read the job description, resume & output the suggested modifications... then our GMail node write an email containing the resume modification suggestions to send to the user._

| AI Agent Node | GMail Node |
|---|---|
| ![Alt text for Image 1](https://github.com/djtoler/Resume-Refiner-AI-Workflow/blob/main/images/ai_node.jpeg) | ![Alt text for Image 2](https://github.com/djtoler/Resume-Refiner-AI-Workflow/blob/main/images/email_node.jpeg) |

#### _5. Below, we can see our AI workflow successfully delivered us an email with a summary of how to tailor my resume for a particular job description._

![Workflow](https://github.com/djtoler/Resume-Refiner-AI-Workflow/blob/main/images/email_inbox.jpeg)

#### Later we added a output parser tool to the AI agent to reliably return outputs in a specified JSON structure.

## Troubleshooting

#### _Finding a out-of-the-box solution to extract relevant job data from HTML code was the initial challenge. I initially wanted to pass the entire HTML code along to the lAi agent and allow the agent to extract the job data. The agents available models did not provied a large enough input token limit so we decided to use a customized Code node to write a script that searches for keywords, extracts overlapping surrounding text, then passes the text along to the AI agent._


## Optimization

#### _To optimize this workflow, I would allow users to upload various file formats, add more keywords to the HTML parser code file, enhance the formatting of the email message, possibly select a lower cost language model to do the modification suggestions._
