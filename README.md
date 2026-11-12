You can use the same common code for all six experiments. Just replace the `print()`, `input()` and `prompt` sections with the following.

These prompts follow your lab manual.

## 1. E-commerce Chatbot

```
print("WELCOME TO ONLINE SHOPPING")data = input("Enter customer question: ")prompt = f"""You are an e-commerce chatbot.Answer customer questions using the product information.Do not invent products, prices or features.If information is not available, say so.Customer question: {data}"""
```

## 2. AI Blog Generator

```
print("AI BLOG CONTENT GENERATOR")topic = input("Enter blog topic: ")style = input("Enter writing style: ")data = topic + " Style: " + styleprompt = f"""Write a blog on the topic: {topic}.Use this writing style: {style}.Include:1. Attractive title2. Introduction3. Main content with headings4. Conclusion"""
```

## 3. Intelligent Email Assistant

```
print("INTELLIGENT EMAIL ASSISTANT")email = input("Enter received email: ")tone = input("Enter tone: ")data = email + " Tone: " + toneprompt = f"""You are an intelligent email assistant.Read the received email and generate an appropriate reply.Received email: {email}Tone: {tone}Include:1. Suitable subject2. Greeting3. Email body4. ClosingDo not invent facts."""
```

## 4. Personalized Recommendation System

```
print("PERSONALIZED COURSE RECOMMENDATION")name = input("Enter student name: ")interest = input("Enter your interest: ")skill = input("Enter skill level: ")data = name + " " + interest + " " + skillprompt = f"""You are a course recommendation assistant.Student name: {name}Interest: {interest}Skill level: {skill}Recommend three suitable courses.Give a short reason for each recommendation."""
```

## 5. AI Document Analyzer

```
print("AI DOCUMENT ANALYZER")filename = input("Enter document name: ")with open(filename, "r", encoding="utf-8") as file:    document = file.read()question = input("Enter your question: ")data = documentprompt = f"""Summarize the following document in simple language.Document:{document}Answer the following question using only the document.If the answer is not available, say so.Question: {question}Include summary and answer."""
```

## 6. AI-Powered Medical Assistant

```
print("AI MEDICAL INFORMATION ASSISTANT")with open("health_info.txt", "r", encoding="utf-8") as file:    health_information = file.read()question = input("Enter your health question: ")data = health_informationprompt = f"""You are a general health information assistant.Use the following information to answer the question.Health information:{health_information}Question: {question}Do not diagnose diseases or prescribe medicines.If information is not available, say so."""
```

## Final revision – What to memorize

| Experiment | Inputs to remember           |
| ---------- | ---------------------------- |
| 1          | Customer question            |
| 2          | Topic, style                 |
| 3          | Email, tone                  |
| 4          | Name, interest, skill        |
| 5          | Filename, document, question |
| 6          | Health file, question        |

One important correction: In Experiments 1 and 4, the lab manual requires CSV datasets (`products.csv` and `courses.csv`). You must read those CSV files and include their contents in the prompt to fully satisfy the question. The short prompts above are templates, not complete replacements for that requirement.

My suggestion: Memorize the six prompt sections separately. They are much shorter than memorizing six complete programs.
You have to create TWO separate Python files in the SAME folder in VS Code. Both codes are needed. You should not paste them together.

Let me show you exactly where to write each one.

## 1. First code – Common helper code

Write only once

File name: `ollama_helper.py`

In VS Code:

1. Open your `GPT_Experiments` folder.
2. Click New File.
3. Type `ollama_helper.py`.
4. Paste this code.
5. Press `Ctrl + S`.

```
import requestsdef ask_ollama(prompt):    url = "http://localhost:11434/api/generate"    data = {        "model": "llama3.2",        "prompt": prompt,        "stream": False    }    response = requests.post(url, json=data, timeout=180)    response.raise_for_status()    return response.json()["response"]
```

Purpose: This code connects your Python program to Ollama and gets the AI response.

You don't need to rewrite this for every experiment.

## 2. Second code – Common application code

File name: `experiment.py`

1. Click New File again.
2. Type `experiment.py`.
3. Paste this code.
4. Press `Ctrl + S`.

```
from ollama_helper import ask_ollamaprint("AI APPLICATION")data = input("Enter your input: ")prompt = f"""You are an intelligent AI assistant.Analyze the following input:{data}Generate a suitable response based on the input.Give the answer in simple and clear language."""result = ask_ollama(prompt)print("\nGENERATED RESULT:\n")print(result)with open("output.txt", "w", encoding="utf-8") as file:    file.write(result)print("\nResult saved successfully.")
```

Purpose: This code accepts user input, sends the prompt to Ollama, displays the answer and saves it in a file.

## 3. Your VS Code folder should look like this

GPT_Experiments

ollama_helper.py

First code

experiment.py

Second code

output.txt

(created automatically)

## 4. How to run the program

Open VS Code Terminal → New Terminal.

First install requests (only once):

```
pip install requests
```

Make sure Ollama is running and the model is available:

```
ollama list
```

Now run:

```
python experiment.py
```

You will get:

```
AI APPLICATION

Enter your input:
```

Type your question and Ollama will generate the answer.

## 5. For the six experiments, what changes?

You keep `ollama_helper.py` unchanged.

You change only `experiment.py` according to the experiment. For example:

| Experiment        | What you type as input   |
| ----------------- | ------------------------ |
| 1. E-commerce     | Customer question        |
| 2. Blog           | Topic and writing style  |
| 3. Email          | Received email and tone  |
| 4. Recommendation | Name, interest and skill |
| 5. Document       | Document and question    |
| 6. Medical        | Health question          |

Important: The common application code is only a starting template. For full marks, add the CSV or text-file reading and other required features specified in the question.

Remember this for your exam:

- `ollama_helper.py` = Connects to AI.
- `experiment.py` = Performs the experiment.

Both files must be in the same folder.
