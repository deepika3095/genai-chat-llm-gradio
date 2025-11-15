## Development and Deployment of a 'Chat with LLM' Application Using the Gradio Blocks Framework
## NAME: DEEPIKA R
## REG: 212223230038
### AIM:
To design and deploy a "Chat with LLM" application by leveraging the Gradio Blocks UI framework to create an interactive interface for seamless user interaction with a large language model.

### PROBLEM STATEMENT:
Develop a user-friendly chatbot application using a large language model (LLM) to assist users with queries and generate conversational responses. The application should feature a responsive design, real-time text exchange, and customizable settings for response quality.

DESIGN STEPS:
STEP 1:Set Up the Environment
Install the necessary libraries (openai, gradio) and verify API access to the LLM.

STEP 2: Create the Chat Functionality
Write a function to interact with the LLM using OpenAI's API (or another preferred LLM provider).

STEP 3: Design the Gradio Blocks Interface
Use Gradio Blocks to build a structured, multi-component UI with features like: A text box for user input. A chat history display. A clear button to reset the conversation.

Step 4: Deploy and Test Host the Gradio app locally or on a server. Test with diverse inputs to ensure robust performance.

### PROGRAM:
```
import os
import gradio as gr
from dotenv import load_dotenv
from text_generation import Client

# Load API key
load_dotenv()
client = Client(
    os.environ["HF_API_FALCOM_BASE"],
    headers={"Authorization": f"Basic {os.environ['HF_API_KEY']}"},
    timeout=120
)

# Format prompt with chat history
def format_prompt(message, history):
    prompt = ""
    for user, bot in history:
        prompt += f"User: {user}\nAssistant: {bot}\n"
    prompt += f"User: {message}\nAssistant:"
    return prompt

# Respond function
def respond(message, history):
    prompt = format_prompt(message, history)
    bot = client.generate(
        prompt,
        max_new_tokens=200,
        stop_sequences=["User:"]
    ).generated_text
    history.append((message, bot))
    return "", history

# Gradio UI
with gr.Blocks() as demo:
    chatbot = gr.Chatbot()
    msg = gr.Textbox(label="Say something")
    btn = gr.Button("Submit")
    btn.click(respond, inputs=[msg, chatbot], outputs=[msg, chatbot])
    msg.submit(respond, inputs=[msg, chatbot], outputs=[msg, chatbot])

demo.launch(share=True)

```

### OUTPUT:
<img width="1179" height="628" alt="image" src="https://github.com/user-attachments/assets/73ab337f-e9bb-4093-943d-05a8c2ac05ff" />
<img width="1180" height="632" alt="image" src="https://github.com/user-attachments/assets/b9c14e3b-8429-45ed-bacf-38886e66b06e" />


### RESULT:
The "Chat with LLM" application successfully enables interactive text-based communication with a large language model, offering a streamlined and visually appealing interface for users.
