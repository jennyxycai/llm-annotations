# Automatic BioNER Data Annotation with Large Language Models
Research by Victoria Gao, Isabella Struckman, Ryan Welch, Jenny Cai. Paper is available [here](https://drive.google.com/file/d/1zE9SACgeOmFf-YnIjh4R_YxhP68edxqz/view?usp=sharing).

### Overview
This is the source code for our paper which introduces a novel approach for biomedical Named Entity Recognition (BioNER) that leverages OpenAI's GPT-3.5 for efficient dataset annotation. As the landscape of biomedical literature rapidly expands, the status quo for labeling BioNER datasets using human annotators is time-consuming and expensive. We propose an automated data-labeling system that employs GPT-3.5's zero-shot, one-shot, and few-shot learning capabilities to generate datasets that mirror the quality of expert human annotation. We validate our approach intrinsically by comparing it against human-labeled datasets and extrinsically by evaluating the performance of two state-of-the-art Biomedical Pretrained Language Models (BPLMs) -- BioLinkBERT and BioGPT -- after fine-tuning on our GPT-labeled datasets. Our approach achieves a promising level of accuracy, comparable to human-annotated data, and demonstrates that BPLMs fine-tuned with our datasets perform well. This study highlights the potential of large language models to revolutionize BioNER dataset annotation, which will result in significant advancements in the field of biomedical natural language processing.

### Status Quo BioNER Labeling Pipeline
<img width="544" alt="Screen Shot 2023-12-15 at 11 15 37 PM" src="https://github.com/jennyxycai/llm-annotations/assets/69180033/489c37b0-bc25-4b65-ab43-d3950b4ce273">

### Proposed Automated Data Labeling Pipeline
<img width="576" alt="Screen Shot 2023-12-15 at 11 15 20 PM" src="https://github.com/jennyxycai/llm-annotations/assets/69180033/c79d2e9b-2b54-4477-beb1-d5edd53c3b0e">

### Evaluation of GPT-label Quality Pipeline
<img width="525" alt="Screen Shot 2023-12-15 at 11 16 27 PM" src="https://github.com/jennyxycai/llm-annotations/assets/69180033/597d5104-6f69-4c6e-8af5-b842bfe8c48c">

### BLURB Datasets Used
| Dataset  | Entities |
| ------------- | ------------- |
| BC5DR-chem  | chemicals |
| BC5DR-disease  | disease  |
| NCBI-disease  | disease  |
| BC2GM  | genes |
| JNLPBA | proteins |

All of these Biomedical NER datasets use the BIO scheme for encoding entity annotations as token tags. Labels B, I, and O are in the 2nd column of tsv files.<br>
B: begin (beginning of the entity)<br>
I: inside (middle of the entity)<br>
O: outside of named entities (e.g. label O in BC5DR-chem dataset means token isn't a chemical; is equivalent to O-Chemical tag written in the format &lt;B/I/O&gt;-&lt;Entity&gt;)

Source: [HuggingFace BigBio/Blurb](https://huggingface.co/datasets/bigbio/blurb)

### Navigating the Repo
Our code is organized into the following folders:
1. `datasets`, `intrinsic_data`, `devel_gpt_labeled_datasets`: the first contains the original BLURB human-annotated datasets, and the latter two contain the GPT-labeled datasets. The folder `intrinsic_data` contains all pre-processed data from `devel_gpt_labeled_datasets` that significantly facilitates intrinsic evaluation.
2. `generating_labels`: this contains code for generating zero, one, and few-shot GPT labels on any specified BLURB dataset. There is an archived notebook included in this folder to demonstrate our experiments with using concurrency libraries in Python to speed up and parallelize OpenAI API calls.
3. `intrinsic_evaluation`: this contains the code for comparing LLM labels to human expert labels. We first corrected output validity, to ensure that LLM-labels were syntactically correct (most syntactic mistakes were due to hallucinations). We then measured GPT's ability to exactly and approximately match human-labeled entities.
4. `extrinsic_evaluation`: this contains code for fine-tuning both BioGPT and BioLinkBERT-base on human-annotated and GPT-annotated BLURB datasets. It then evaluates the performance of either BioGPT and BioLinkBERT-base on test splits of BLURB datasets and outputs a classification performance report.

