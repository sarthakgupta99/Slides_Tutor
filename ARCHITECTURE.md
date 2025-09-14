# AI Agent Architecture: The Genetics Tutor

This document outlines the architecture of the AI agent built to automate studying for the BT301 Genetic Engineering course.

## 1. Task Automation

The agent is designed to automate the manual task of searching through lecture notes to find answers to specific questions.  
It acts as a reliable "Genetics Tutor" that can reason and execute answers based on a specialized knowledge base.

## 2. Components and Interaction Flow

The agent has a simple, single-model architecture.

1. **Input:** The user provides a question in natural language (e.g., "What is a gene?").
2. **Processing:** The question is formatted into a standardized prompt and tokenized for the model.
3. **Model:** The core of the agent is a fine-tuned `meta-llama/Llama-2-7b-chat-hf` model.  
   This model processes the tokenized prompt and generates an answer.
4. **Output:** The generated tokens are decoded back into text, providing a concise and accurate answer to the user's question.

## 3. Rationale for Fine-Tuning

A fine-tuned model was a mandatory requirement of the project.  
The decision to fine-tune the Llama-2 model on the specific `genetics.txt` lecture notes was driven by the need for high reliability and task specialization.

- **Task Specialization:** The agent learns the specific terminology, scope, and concepts of the BT301 course.  
  A general model might provide information that is too broad or irrelevant to the course syllabus.
- **Improved Reliability:** By training exclusively on the course material, the agent is significantly less likely to "hallucinate" or provide incorrect information from outside sources.  
  This makes it a dependable study tool.
- **Adapted Style:** The agent's responses are stylistically aligned with the lecture notes, ensuring consistency for the student.

The model was tuned using LoRA for parameter efficiency, and 4-bit quantization was used to make the process computationally feasible on available hardware.

