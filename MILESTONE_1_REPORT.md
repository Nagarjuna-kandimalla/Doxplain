# QA Pipeline - Milestone 1

### 1. Objective and Pipeline Overview  

The objective of this project is to design and evaluate a machine learning pipeline for question answering (QA) over scientific and encyclopedic documents. The pipeline integrates data ingestion, embedding-based retrieval, reranking, and answer generation into a unified framework. Two benchmark datasets are used: **QASPER**, consisting of scientific research papers and associated questions, and **HotpotQA**, consisting of Wikipedia-based multi-hop reasoning questions.  

The end-to-end workflow is deployed across two Jupyter notebooks, executed within a Docker container. The first notebook handles **data ingestion and storage into ChromaDB**, while the second notebook performs **retrieval, answer generation, and assertion-based evaluation**.  

---

### 2. Architecture  

The pipeline is modular, with distinct components for datasets, embedding models, reranking models, and QA models.  

**Datasets.**  
- **QASPER**: Research-paper-based dataset with annotated QA pairs.  
- **HotpotQA**: Wikipedia-based multi-hop QA dataset.  

**Embedding.**  
- **all-MiniLM-L6-v2**: Used for chunk-level embeddings to support semantic retrieval via ChromaDB.  

**Reranking.**  
- **cross-encoder/ms-marco-MiniLM-L-6-v2**: Applied to refine retrieved passages, ensuring higher contextual relevance for downstream QA models.  

**Question Answering Models.**  
- **google-bert/bert-large-uncased-whole-word-masking-finetuned-squad**  
- **deepset/tinyroberta-squad2**  
- **deepset/roberta-base-squad2**  

**Pipeline Configurations.**  
A configuration is defined as a unique combination of dataset and QA model (embedding and reranker are fixed). This results in:  

- 2 datasets  
- 1 embedding model  
- 1 reranker  
- 3 QA models  

Total = **6 pipeline configurations**. 

---

### 3. Results  

Each configuration is evaluated on three criteria:  

- **Accuracy**: measured as the number of assertions passed.  
- **Latency**: average per-question response time.  
- **SLA Met**: whether the configuration satisfies the required service-level agreement.  

At present, SLA benchmarks have not yet been released; therefore, placeholders are provided for all results.  

| Dataset   | QA Model                                                   | Accuracy (Assertions) | Latency (s) | SLA Met |
|-----------|-------------------------------------------------------------|------------------------|-------------|---------|
| QASPER    | google-bert/bert-large-uncased-whole-word-masking-squad    | TBD                    | TBD         | TBD     |
| QASPER    | deepset/tinyroberta-squad2                                 | TBD                    | TBD         | TBD     |
| QASPER    | deepset/roberta-base-squad2                                | TBD                    | TBD         | TBD     |
| HotpotQA  | google-bert/bert-large-uncased-whole-word-masking-squad    | TBD                    | TBD         | TBD     |
| HotpotQA  | deepset/tinyroberta-squad2                                 | TBD                    | TBD         | TBD     |
| HotpotQA  | deepset/roberta-base-squad2                                | TBD                    | TBD         | TBD     |  

---

### 4. Team Organization  

The team collaborates primarily via a shared **Discord channel**, which supports rapid communication and iteration. Responsibilities are divided as follows:  

- **Data Ingestion (load_dataset.ipynb):** drafted primarily by Deshan, focusing on acquisition, preprocessing, and ChromaDB ingestion.  
- **Model Integration (load_models.ipynb):** drafted primarily by Nagarjuna, focusing on retrieval, reranking, and QA model integration.  
- **Pipeline Integration and Documentation:** led by Katelyn, responsible for unifying both components, cleaning and documenting the pipeline, and reporting metrics. Plans include hosting the pipeline on AWS to enable scalable deployment and external evaluation.  

No major teamwork challenges have arisen. To strengthen collaboration in future milestones, the team intends to:  
- Use GitHub for clearer version control and issue tracking.  
- Define explicit deadlines for metric reporting and SLA validation.  
- Maintain Discord as the main communication channel, supplemented by structured weekly check-ins.  

---

### 5. Conclusion  

The pipeline integrates multiple QA models across two datasets in a modular architecture, yielding six total configurations. Results will be benchmarked on accuracy, latency, and SLA compliance once metrics are available. The team’s division of labor and collaborative workflow have supported efficient development, with plans to extend evaluation and deployment in future milestones.  