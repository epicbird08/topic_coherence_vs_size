# Topic Modeling with BERTopic

## Summary
This project applies BERTopic to text datasets (20 Newsgroups or PubMed) to discover meaningful topics. The code is designed to compare models by calculating **topic coherence** and **topic diversity**. It also supports optional **quantization** for faster and lighter models.

## Installation
Clone the repository and install requirements:

```bash
pip install -r requirements.txt
```

## Usage

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

## License
This project is licensed under the MIT License.
