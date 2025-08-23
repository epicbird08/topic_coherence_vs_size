# Topic Modeling with BERTopic

## Summary
This project applies BERTopic to text datasets (20 Newsgroups or PubMed) to discover meaningful topics. The code is designed to compare models by calculating **topic coherence** and **topic diversity**. It also supports optional **quantization** for faster and lighter models.

## Installation
Clone the repository and install requirements:

```bash
pip install -r requirements.txt
```

## Usage

First run experiments on the **Dummy dataset** to ensure things run smoothly:

```bash
python topic_model_pipeline.py --dataset dummy_dataset
```

Run experiments on the **20 Newsgroups dataset**:

```bash
python topic_model_pipeline.py --dataset 20newsgroups
```

Run experiments on the **PubMed dataset**:

```bash
python topic_model_pipeline.py --dataset pubmed
```

Enable **quantization** for efficiency:

```bash
python topic_model_pipeline.py --dataset pubmed --quantize
```

After running, results are written to `results.csv` in the project root. Each row records the model, whether quantization was used, and the corresponding coherence and diversity scores, so you can easily compare model performance.

## Install packages using uv 

Alternatively, you can install packages using **uv**. uv is "An extremely fast Python package and project manager, written in Rust". You can download it from [here](https://github.com/astral-sh/uv).

To run the code using uv (instructions for Windows but should be similar on other OS) you can:

1- Install uv following the instructions here: https://github.com/astral-sh/uv

2- Clone this repository and go to the experiments folder

3- Create a virtual environment using uv:

```bash
uv venv --python 3.11
```

4- Activate the virtual environment

```bash
.venv/bin/activate
```

5- Install the required packages

```bash
uv pip install -r requirements.txt
```

6- Run the python script

```bash
python .\topic_model_pipeline.py
```

## Models Used

The following embedding models were tested in this pipeline:

- **Sentence-Transformers**
  - [`all-MiniLM-L6-v2`](https://huggingface.co/sentence-transformers/all-MiniLM-L6-v2) (22M params)  
- **Hugging Face Transformers**
  - [`distilbert-base-uncased`](https://huggingface.co/distilbert-base-uncased) (66M params)  
  - [`bert-base-uncased`](https://huggingface.co/bert-base-uncased) (110M params)  
  - [`roberta-base`](https://huggingface.co/roberta-base) (125M params)  
  - [`microsoft/MiniLM-L12-H384-uncased`](https://huggingface.co/microsoft/MiniLM-L12-H384-uncased) (33M params)  
- **Large Language Models**
  - [`meta-llama/Llama-2-7b-hf`](https://huggingface.co/meta-llama/Llama-2-7b-hf) (7B params)  
  - [`meta-llama/Llama-2-13b-hf`](https://huggingface.co/meta-llama/Llama-2-13b-hf) (13B params, may fail to run without quantization)  

Other models may be swapped in and evaluated by changing the pipeline code.

## Used Datasets
* **20 Newsgroups** – a classic text classification dataset. It can be downloaded [here](http://qwone.com/~jason/20Newsgroups/).  
* **PubMed Abstracts** – Abstracts from PubMed articles published between 1/1/24 and 5/31/25 that contain at least one of "Artificial Intelligence", "Large Language Models", or "AI-assisted diagnosis" in the title or abstract. It can be downloaded at [willyrv/pubmed2024_IA-LLM-diagnostic](https://huggingface.co/datasets/willyrv/pubmed2024_IA-LLM-diagnostic).

## Metrics

The pipeline evaluates the topic models using the following metrics:

- **Topic Coherence**: Measures the semantic coherence of the topics using gensim's CoherenceModel with the 'c_v' coherence measure.
- **Topic Diversity**: Calculates the average pairwise cosine similarity between topics, converted to a diversity score (1 - similarity).
- **Number of Topics**: The number of unique topics identified by the model.
- **Running Time**: The time taken (in seconds) for the full pipeline per encoder.

## License
This project is licensed under the MIT License.
