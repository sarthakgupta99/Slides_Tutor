LLM Interaction Logs
This file contains a history of interactions with an AI assistant (Google Gemini) during the development of the "Genetics Tutor" AI Agent, as encouraged by the assignment guidelines.

Session 1: Initial Setup & GPU Debugging
My Prompt:

I have to build an AI agent for my internship assignment that automates a task from my university work. It needs to use a fine-tuned model. My course is on Genetic Engineering. I have the lecture notes as a .txt file. What's a good approach?

AI Response:

That's a great project idea. You can build an agent that acts as a specialized Q&A tutor for your course. The manual task you're automating is "searching through notes to find answers."

A good approach would be:

Choose a powerful base model: A model like meta-llama/Llama-2-7b-chat-hf is a strong, open-source choice.

Use PEFT with LoRA: Fine-tuning the full model is computationally expensive. Use the PEFT library with LoRA to efficiently fine-tune it on your genetics.txt data.

Quantize the model: Use the bitsandbytes library to load the model in 4-bit precision. This will be crucial to avoid running out of GPU memory.

I can help you with the initial code to load the model this way.

My Prompt:

I'm trying to run the training script, but I'm getting a CUDA out of memory error. How can I fix this? My GPU is a T4.

AI Response:

The "CUDA out of memory" error is very common with large models. Here are the most effective ways to solve it on a T4 GPU:

Batch Size: Your per_device_train_batch_size is the most likely culprit. Try reducing it. If it's at 4, try 2 or even 1.

Gradient Accumulation: To compensate for a smaller batch size, you can use gradient_accumulation_steps. For example, if you reduce your batch size from 4 to 2, you can set gradient_accumulation_steps=2 to achieve the same effective batch size of 4.

Check Quantization: Double-check that your BitsAndBytesConfig is correctly configured for 4-bit loading (load_in_4bit=True). This dramatically reduces the memory footprint.

Here's an example of the arguments you might use in transformers.TrainingArguments:

args=transformers.TrainingArguments(
    per_device_train_batch_size=2,
    gradient_accumulation_steps=2,
    ...
)

Session 2: Data Loading & LoRA Configuration
My Prompt:

I'm trying to load my genetics.txt file using load_dataset("text", data_files="genetics.txt") but it's giving me a UnicodeDecodeError. What's wrong?

AI Response:

A UnicodeDecodeError usually means the file was saved with a specific encoding that the function isn't expecting. The default is often 'utf-8'. Your file might be encoded differently.

Try specifying the encoding directly in the function call. A common one that works for many text files is latin-1.

train_dataset = load_dataset(
    "text",
    data_files={"train": ["/content/genetics.txt"]},
    split="train",
    encoding="latin-1" # Add this parameter
)

This should resolve the decoding error.

My Prompt:

For the LoRA config, how do I know which target_modules to use for the Llama-2 model?

AI Response:

That's an excellent question. The target_modules are the specific layers of the transformer you want to adapt with LoRA. For the Llama-2 architecture, the most common and effective modules to target are the attention projection layers and sometimes the feed-forward network layers.

For a comprehensive setup with Llama-2, you should target all linear layers involved in attention and the feed-forward network. A good default configuration is:

config = LoraConfig(
    ...
    target_modules=["q_proj", "k_proj", "v_proj", "o_proj", "gate_proj", "up_proj", "down_proj"],
    ...
)

This targets the query, key, value, and output projections in the attention mechanism, as well as the gate, up, and down projections in the MLP block.

Session 3: Evaluation and Final Submission
My Prompt:

My model is trained. Now the assignment says I need to "design and implement evaluation metrics." What's a good way to do this for a Q&A agent?

AI Response:

A great way to evaluate your agent is to perform a qualitative comparison. You can create a small test set of questions from your lecture notes and compare the answers from your fine-tuned model against the original, base Llama-2 model.

You should judge the answers based on criteria like:

Accuracy: Is the answer factually correct based on your genetics.txt file?

Specificity: Does it use the specific terminology from the course? The fine-tuned model should be much better at this.

Conciseness: Is the answer direct and not overly verbose?

Presenting this in a table in your report would be very effective.

My Prompt:

Okay, the evaluation is done. The assignment asks for several documents: a source code file, an architecture document, a data science report, and interaction logs. Can you help me structure these?

AI Response:

Of course. Let's structure them:

Source Code: Your primary source code is your Jupyter Notebook. Just make sure it's cleaned up with comments.

Architecture Document: This should be a brief .md file. Describe the agent's task, its components (Input -> Model -> Output), and most importantly, the reason you chose to fine-tune the model.

Data Science Report: This is your main document. It should have two parts: Fine-Tuning Setup and Evaluation.

Interaction Logs: This file itself! Just document the help you've received.

I can generate templates for the architecture and report documents for you to fill in.

My Prompt:

I've created all the files. How do I put them on GitHub and what should I write in the submission email?

AI Response:

To submit:

Create a new public repository on GitHub.

Use the "Add file" -> "Create new file" option on the GitHub website to create each .md file and paste the content in.

Use the "Add file" -> "Upload files" option to upload your .ipynb notebook and your .txt dataset.

Make sure you create a README.md with your name, university, and department as requested.

Finally, send a professional email with the link to your repository to the provided email addresses. Keep it short and clear.
