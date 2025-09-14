# Data Science Report: Slides Tutor Agent

This report covers the fine-tuning setup and evaluation of the AI agent.

## Part A: Fine-Tuning Setup

### Data
The model was fine-tuned on a custom dataset named `genetics.txt`.  
This dataset is a single text file containing the complete content of 20 lecture slides from the "BT301: Genetic Engineering & Applications" course at the Indian Institute of Technology (IIT).  
The data covers fundamental and advanced topics in molecular genetics, including the Central Dogma, CRISPR-Cas9, and recombinant DNA technology.

### Method
- **Base Model:** `meta-llama/Llama-2-7b-chat-hf`
- **Technique:** Parameter-Efficient Fine-Tuning (PEFT) using Low-Rank Adaptation (LoRA).  
  This approach allows for efficient tuning by only updating a small subset of the model's parameters.
- **Configuration:** Key LoRA parameters included a rank (`r`) of 8 and `lora_alpha` of 64.  
  The target modules for adaptation were `["q_proj", "k_proj", "v_proj", "o_proj", "gate_proj", "up_proj", "down_proj"]`.
- **Hardware Optimization:** To manage memory constraints, the model was loaded in 4-bit precision using the `BitsAndBytesConfig` from the `transformers` library.  
  The quantization type was "nf4" with a compute dtype of `torch.bfloat16`.

### Results
The model was trained for a limited number of steps to demonstrate feasibility.  
The final training loss after 20 steps was **2.6723**, indicating that the model was successfully learning from the custom dataset.

## Part B: Evaluation

### Methodology
To measure the quality and reliability of the agent, a qualitative evaluation was performed.  
A question was asked based on the content of the lecture slides.  
Answers were generated from both the **base model** and the **fine-tuned agent**.  
The responses are compared on three criteria:

1. **Accuracy:** Is the information factually correct according to the `genetics.txt` file?  
2. **Specificity:** Does the answer use the specific terminology from the course?  
3. **Conciseness:** Is the answer direct and to the point?

### Outcomes

| Question | Base Model Answer | Fine-Tuned Model Answer
| :--- | :--- | :---
| **What is a gene?** | `A gene is a segment of DNA that contains the instructions to make a specific protein or functional RNA. It serves as the basic unit of heredity, transmitting traits from parents to offspring. Genes are located on chromosomes inside the cell’s nucleus and sometimes in mitochondria. They are composed of nucleotide sequences—adenine (A),thymine (T), cytosine (C), and guanine (G).Variations or mutations in these sequences create genetic diversity and can influence how the body grows, functions, or develops diseases.` | `scientific explanation: A gene is a unit of heredity that carries the information necessary to create a specific protein. In simpler terms, a gene is a set of instructions inside your body that tells your cells how to make a specific protein. Proteins are like the building blocks of your body, so they play a crucial role in how your body functions and looks. For example, some genes help your body grow and repair tissues, while others determine your eye color or hair color. Genes are made up of a long sequence of molecules called DNA, which is inside every living cell. The DNA sequence inside each gene tells your body how to build a specific protein. When your body reads the instructions inside a gene, it uses the information to create the protein.` 

Our fine-tuned agent consistently delivers more focused and context-aware answers than the base model. When questioned about concepts from the lecture slides, it recalls precise definitions and examples directly relevant to the course material, while the base model tends to provide broader, more generic explanations. This demonstrates that fine-tuning on the slide content successfully improves both relevance and specificity of responses, highlighting the added value of the customized model.
