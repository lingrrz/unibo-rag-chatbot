# unibo-rag-chatbot

## 📌 Project Overview
This project extends the baseline RAG-based chatbot, focusing on Master's Degree programs at the **University of Bologna (Unibo)**. 

Our primary goal is to overcome the limitations of the static `query -> retrieve -> generate` pipeline by framing the LLM as a **Large Action Model (LAM)**. We test different agentic paradigms to resolve major retrieval inefficiencies and benchmark them against a standard RAG pipeline.

## 🎯 Problem Statement
Static retrieval pipelines struggle with two main types of complex queries:
1. **Issue 1: Multi-topic Queries:** If a user asks for multiple distinct things in one prompt (e.g., *"Where are the Text-Mining lectures held and when is the next exam date?"*), the query embedding becomes noisy, often returning incorrect or diluted sources.
2. **Issue 2: Multi-hop Queries:** Composed queries require intermediate information. For example, *"What other courses does the Text-Mining teacher hold?"* requires first finding out who teaches Text-Mining before searching for their other courses. Static RAG fails because it lacks backtracking.

---

## 🚀 Methodology & Assignments

### Scraping & Data Preparation
A clean, functional, and customizable scraping script is included in this repository. It extracts up-to-date `.md` data starting from predefined Unibo URLs. Specifically, the scraper is configured to target 8 specific Master's degree programs (along with their sub-pages and related professor profiles):
* **Artificial Intelligence** (`ai-msc`)
* **Computer Science Engineering** (`cs-msc`)
* **Automation Engineering** (`automation`)
* **Aerospace Engineering** (`aerospace`)
* **Physics of the Earth System** (`physics-earth`)
* **Digital Humanities** (`digital-humanities`)
* **Legal Studies** (`legal-studies`)
* **GIOCA** (`gioca`)

### Assignment 1: Query Decomposition (Issue 1)
Focuses on building a pre-processing step to clean, rewrite, and decompose messy initial user inputs. The LLM breaks down multi-topic questions into multiple, highly targeted search queries to improve embedding precision and search performance.

### Assignment 2: Agentic Retrieval Loop (Issue 2)
Focuses on creating a classic agentic loop. Here, **retrieval acts as a tool** the LLM can call at will. The LLM is instructed to read the initial search results, determine what information is still missing, and autonomously generate new, customized queries (multiple `search-read-generate` iterations) to complete the answer.

---

## 📊 Benchmark Dataset
We created a benchmark dataset of exactly **100 Q&A pairs** tailored to Unibo domains, divided into 3 splits:
1. **The "Hard Set" (Standard FAQs):** Real questions and answers extracted directly from the scraped Unibo websites.
2. **Synthetic Multi-topic Set:** LLM-generated questions combining multiple concepts to test Query Decomposition.
3. **Synthetic Multi-hop Set:** LLM-generated questions requiring sequential reasoning to test the Agentic Loop.

---

## 📈 Evaluations & Benchmarking
The final deliverable is a **unified Colab Notebook** that implements both techniques and benchmarks them against the baseline static RAG pipeline.

We evaluate the trade-off between performance and computational cost. For instance, we assess whether a 2-5% gain in accuracy justifies a potential 10x increase in processing time.
* **Accuracy:** Measured using **ROUGE scores** against our benchmark dataset.
* **Efficiency:** Measured by tracking **total latency** (processing time).
* **Agentic Statistics:** Tracking the number of times the retriever tool is called autonomously, and how often the LLM decides to decompose a query.

---

--------TBC--------

👥 Contributors

Xiyan.W, Lingrui.Z
