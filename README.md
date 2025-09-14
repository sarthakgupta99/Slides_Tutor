# AI Agent Prototype: The Slides Tutor

This repository contains the submission for the Data Science Internship Assignment.

- **Name:** Sarthak Gupta
- **University:** IIT Jodhpur
- **Department:** Bioengineering

## Project Overview

This project features an AI agent designed to automate the task of studying and retrieving information from a specific university course on Genetic Engineering (BT301). The agent acts as a knowledgeable tutor, answering user questions based on a corpus of 20 lecture slides. This agent can be furthur used on the lecture slides of any other course.

The core of the agent is a `meta-llama/Llama-2-7b-chat-hf` model that has been fine-tuned using Parameter-Efficient Fine-Tuning (PEFT) with LoRA. This specialization ensures that the agent's responses are accurate, reliable, and consistent with the specific terminology and scope of the course material.

## Deliverables

- **Source Code:** `Slides_Tutor.ipynb`
- **AI Agent Architecture:** `ARCHITECTURE.md`
- **Data Science Report:** `REPORT.md` (includes fine-tuning setup and evaluation)
- **Dataset:** `genetics.txt`
- **LLM Interaction Logs:** `INTERACTION_LOGS.md`
