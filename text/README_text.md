# Question Answering Pipeline

The goal here is to build a pipeline that has two steps, summarization and question answering.

The premise behind building this pipeline is to use small question answering models that
can easily run on edge devices.

Thus, we will use extractive question answering models, mainly models part of the BERT architecture
to perform question answering.

It is widely known that these BERT models have a token limit of 512, thus they are unable to ingest
large inputs without truncating them. Through this process, valuable information can be lost, leading
to the model being unable to answer the question.

Thus as a preprocessing step, we will generate a summary of the text before passing it to the 
question answering step.

## Step 1: Summarization

To do summarization, implement the following set up:

We will create a RAG based set up to imitate the summarization step. This is a setup that can scale will
with the size of the size of the contexts being used.
Using the given embedding models create a vectorstore using Langchain. We use ChromaDB as an opensource easy-
to-implement option to create the vectorstore locally.

Some embedding models have been listed here:
1. sentence-transformers/all-MiniLM-L6-v2
2. sentence-transformers/all-mpnet-base-v2
3. sentence-transformers/all-MiniLM-L12-v2

You are free to look for other options and use other embedding models as well.

Since the contexts are mostly greater than 2800 characters, which roughly translates into 512 tokens,
you must first store the context into the vectorstore by first cutting up the context using an appropriate
chunk size and chunk overlap. Then using the embedding model, embed the contexts, now a series of documents,
and store these embedded chunks into the vectorstore.

After this step, embed the question using the same embedding model and query the vectorstore with the question
and return an appropriate number of chunks to further pass to the question answering model.

The code to load the models into the cache of the container is in the notebook: ```load_models.ipynb```,
the notebook also has some sample code on how the embeddings work.

## Step 2: Question Answering Step

To do question answering, we have provided you with a plethora of models to start out with mainly:

1. deepset/tinyroberta-squad2
2. deepset/roberta-base-squad2
3. google-bert/bert-large-uncased-whole-word-masking-finetuned-squad

All these models are available on Huggingface, along with many others that are not mentioned here.
It is up to you to choose which models to use to set up the pipeline.

To load the models into cache, you can run the notebook ```load_models.ipynb``` in jupyterlabs.

## Assertion

As an example, we provide a very simple assertion to check the accuracy of the pipeline.

You may define a threshold for the confidence score of the question answering model to roughly check
whether the answer is correct or not.

## Datasets

We provide you the option between two datasets that all serve the same purpose of extractive question
answering with a summarization preprocessing step.

1. HotPotQA
2. QASPER

The Dockerfile automatically copies the script to download the datasets, just run the jupyter notebook
```load_dataset.ipynb``` which wll download the dataset and print the path of where it is stored.