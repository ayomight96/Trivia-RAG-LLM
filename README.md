#RAG-Powered Question Answering Pipeline

#Overview

This project implements a Retrieval-Augmented Generation (RAG) pipeline to process multiple-choice questions using:
	1.	Document Retrieval: FAISS (Facebook AI Similarity Search) for fast document similarity matching.
	2.	Context Augmentation: Retrieved documents are used to create a context-enriched prompt.
	3.	Response Generation: An LLM (Microsoft Phi-3.5-mini-instruct) generates answers based on the query and augmented context.

The pipeline processes questions from an input CSV file in batches, handles errors like GPU memory exhaustion, and appends results to an output CSV file.

#Project Workflow

#Steps:

	1.	Prepare Documents:
	    •	Combine predefined documents with additional question-answer sentences from an Excel file.
	2.	Embed Documents:
	    •	Use SentenceTransformer to create vector embeddings of all documents.
	    •	Save embeddings as a .npy file for efficient loading.
	3.	Create FAISS Index:
	    •	Build a FAISS index using the embeddings for similarity search.
	4.	Process Questions:
	    •	Read questions in batches from a CSV file.
	    •	For each question:
	        a	Retrieve top-k similar documents using FAISS.
	        b	Create a context-enriched prompt.
	        c	Generate an answer using the LLM pipeline.
	5.	Handle Memory Errors:
	    •	If a CUDA out-of-memory error occurs:
	        a	The batch retries after clearing GPU memory.
	        b	After max retries, the batch is skipped, and processing continues.
	6.	Save Results:
	    •	Append answers (in letter format, e.g., A, B, C) to an output CSV file.

#Technologies Used

	•	Python (Data Processing)
	•	Google Colab (Execution Environment)
	•	FAISS (Document Similarity Search)
	•	SentenceTransformer (Document Embedding)
	•	Transformers Library (LLM Inference)
	•	PyTorch (Model Execution)
	•	Pandas (CSV Handling)

#Error Handling

	•	CUDA Out-of-Memory:
	•	The pipeline retries processing a batch after clearing GPU memory.
	•	After reaching the maximum retries, the batch is skipped.

#Improvements

	•	Implemented GPU memory management with retries on failure.
	•	Supports batch processing for scalability.
	•	Handles exceptions gracefully.
