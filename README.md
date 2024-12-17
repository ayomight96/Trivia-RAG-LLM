RAG-Powered Question Answering Pipeline

Overview

This project implements a Retrieval-Augmented Generation (RAG) pipeline to process multiple-choice questions using:
1. Document Retrieval: FAISS (Facebook AI Similarity Search) for fast document similarity matching.
2. Context Augmentation: Retrieved documents are used to create a context-enriched prompt.
3. Response Generation: An LLM (Microsoft Phi-3.5-mini-instruct) generates answers based on the query and augmented context.

The pipeline processes questions from an input CSV file in batches, handles errors like GPU memory exhaustion, and appends results to an output CSV file.

Project Workflow
Steps:
1. Prepare Documents: Combine predefined documents with additional question-answer sentences from an Excel file.
2. Embed Documents:
   . Use SentenceTransformer to create vector embeddings of all documents.
   . Save embeddings as a .npy file for efficient loading.
3. Create FAISS Index:
   . Build a FAISS index using the embeddings for similarity search.
4. Process Questions:
   . Read questions in batches from a CSV file.
   . For each question:
   	a. Retrieve top-k similar documents using FAISS.
   	b. Create a context-enriched prompt.
	c. Generate an answer using the LLM pipeline.
5. Handle Memory Errors:
   . If a CUDA out-of-memory error occurs:
   	a. The batch retries after clearing GPU memory.
	b. After max retries, the batch is skipped, and processing continues.
6. Save Results:
   . Append answers (in letter format, e.g., A, B, C) to an output CSV file.

Note: The Embedded Document and Faiss index files are to large to be uploaded here so the link are as follows:
1. Embedded Document: https://drive.google.com/file/d/1-44Sr7SVuG9Fjs7MrZi4MNyKoa_jMJbF/view?usp=drive_link
2. Faiss Index: https://drive.google.com/file/d/1-DDPfo96CDoPvHkpYC9Bib3uxVASvAxz/view?usp=drive_link 

Technologies Used
1. Python (Data Processing)
2. Google Colab (Execution Environment)
3. FAISS (Document Similarity Search)
4. SentenceTransformer (Document Embedding)
5. Transformers Library (LLM Inference)
6. PyTorch (Model Execution)
7. Pandas (CSV Handling)

Error Handling
1. CUDA Out-of-Memory:
   . The pipeline retries processing a batch after clearing GPU memory.
   . After reaching the maximum retries, the batch is skipped.

Improvements
1. Implemented GPU memory management with retries on failure.
2. Supports batch processing for scalability.
3. Handles exceptions gracefully.
