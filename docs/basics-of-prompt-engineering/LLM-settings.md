---
layout: default
title: LLM Settings
parent: Basics of Prompt Engineering
nav_order: 3
---

# LLM Settings

When designing and testing prompts, you typically interact with the LLM via an API. You can configure a few parameters to get different results for your prompts. Tweaking these settings are important to improve reliability and desirability of responses and it takes a bit of experimentation to figure out the proper settings for your use cases. Below are the common settings you will come across when using different LLM providers:

## 1.Temperature
In short, the lower the temperature, the more deterministic the results in the sense that the highest probable next token is always picked. Increasing temperature could lead to more randomness, which encourages more diverse or creative outputs. You are essentially increasing the weights of the other possible tokens. In terms of application, you might want to use a lower temperature value for tasks like fact-based QA to encourage more factual and concise responses. For poem generation or other creative tasks, it might be beneficial to increase the temperature value.


### Low Temperature (e.g., 0.1 - 0.4)
- **Deterministic and Fact-Based Tasks**: When you want the model to provide consistent, precise answers, such as for:
  - Code generation or debugging
  - Answering factual questions (e.g., scientific information, mathematical calculations)
  - Summarizing text with minimal variability
- **Formal and Structured Outputs**: For tasks requiring structure, like generating legal or technical documents where precision and consistency are crucial.

### High Temperature (e.g., 0.7 - 1.2)
- **Creative Writing or Brainstorming**: When you want diverse or imaginative output, such as:
  - Writing stories, poems, or creative pieces
  - Generating multiple ideas or variations for brainstorming
- **Conversational Chatbots**: For chatbots that need to sound natural, engaging, and varied in conversation.
- **Exploratory Outputs**: When experimenting with different responses, such as generating variations in marketing slogans or ad copies.

### Medium Temperature (e.g., 0.5 - 0.7)
- This range strikes a balance, making it suitable for cases where you want some creativity but still need reasonable consistency, like casual conversation or generating informative but engaging text.

<img width="708" alt="image (2)" src="https://github.com/user-attachments/assets/46bf03e8-5b59-4c4c-9c61-643d47d10196">

Here's a table that outlines the recommended **temperature settings** for each of the listed NLP tasks, along with an explanation for why the temperature setting is appropriate for that specific task.

| **NLP Task**                          | **Recommended Temperature** | **Explanation**                                                                                                                                                 |
|---------------------------------------|-----------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------|
| **Sentiment Analysis**                | Low (0.2 - 0.4)             | Sentiment analysis requires **accuracy** and **predictability** to correctly classify the emotional tone of the text. A low temperature ensures clear, consistent classifications. |
| **Named Entity Recognition (NER)**   | Low (0.2 - 0.3)             | NER needs **precise identification** of named entities (people, places, organizations). A low temperature avoids generating irrelevant or ambiguous entities.  |
| **Part-of-Speech (POS) Tagging**      | Low (0.2 - 0.3)             | POS tagging requires accurate **classification** of words based on their syntactic role. A low temperature ensures the output is deterministic and consistent.    |
| **Dependency Parsing**                | Low (0.2 - 0.3)             | Dependency parsing involves **accurate syntactic structure** analysis. A low temperature ensures the model doesn’t deviate from expected grammatical structures.    |
| **Text Classification**               | Low (0.3 - 0.5)             | Text classification requires **clear and deterministic classification** into predefined categories. A low temperature keeps the results stable and predictable.    |
| **Question Answering**                | Low (0.3 - 0.5)             | Question answering demands **factual accuracy** and **reliable extraction** of information. A low temperature prevents hallucinations or off-topic answers.         |
| **Part-of-Speech Tagging with Dependency Parsing** | Low (0.2 - 0.3) | This task combines **POS tagging** and **dependency parsing** and requires **accuracy** and **reliable grammar structure**. A low temperature maintains consistency. |
| **Text Summarization**                | Low (0.3 - 0.5)             | Summarization requires **clarity and relevance**. A low temperature ensures that the model focuses on extracting the most important information without introducing too much creativity. |
| **Language Translation**              | Low (0.2 - 0.4)             | For translation, **accuracy** in mapping one language to another is essential. A low temperature ensures proper translations without unnecessary changes or mistakes. |
| **Coreference Resolution**            | Low (0.3 - 0.4)             | Coreference resolution needs to maintain **consistent references** between words (e.g., "he" vs. "John"). A low temperature ensures clear and accurate linking of pronouns to entities. |

### High Temperature Tasks: Examples & Explanations

| **NLP Task**                          | **Recommended Temperature** | **Explanation**                                                                                                                                                 |
|---------------------------------------|-----------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------|
| **Text Generation (Creative Writing)** | High (0.7 - 1.0)             | For tasks like creative writing or story generation, you want the model to produce **diverse, unexpected**, and **imaginative** content. A high temperature encourages creativity and exploration of ideas. |
| **Dialogue Generation**               | High (0.7 - 1.0)             | In dialogue systems (e.g., chatbots, interactive fiction), a high temperature can generate more **natural, varied**, and **engaging responses** that mimic human-like conversation and creativity. |
| **Poetry Generation**                 | High (0.7 - 1.0)             | Poetry generation requires **imaginative, unique phrasing** and artistic expression. A high temperature leads to more **creative** and less predictable outputs. |
| **Storytelling/Creative Narrative Generation** | High (0.7 - 1.0) | Generating creative stories demands **originality** and **diversity** in plot, character development, and dialogue. High temperature allows the model to take **risks** and explore unconventional ideas. |
| **Brainstorming/Idea Generation**     | High (0.7 - 1.0)             | When brainstorming new ideas (e.g., for projects, products, or solutions), a high temperature encourages the model to generate **novel, unconventional** ideas, without sticking to conventional or safe choices. |
| **Text Completion (Creative)**        | High (0.7 - 1.0)             | In tasks like completing a partially written story or paragraph, a high temperature encourages the model to fill in the gaps with **varied and creative endings**, leading to unexpected twists or novel continuations. |
| **Open-Domain Question Answering**    | High (0.7 - 1.0)             | For open-ended question answering, where there may be multiple valid responses or interpretations, a high temperature allows the model to generate more **exploratory, diverse**, and **context-sensitive** answers. |
| **Joke or Humor Generation**          | High (0.7 - 1.0)             | Humor often requires **creative** and **unexpected twists**. High temperature helps generate **funny**, **witty**, and **original** punchlines or jokes. |
| **Text-based Game (Interactive Fiction)** | High (0.7 - 1.0)        | In interactive fiction or text-based games, a high temperature enables the model to produce **interactive, dynamic narratives** that respond to user inputs in a **flexible, engaging** manner. |

---

### Summary of High Temperature Recommendations:
- **High Temperature (0.7 - 1.0)** is ideal for tasks that benefit from **creativity**, **diversity**, and **exploration**, such as:
  - **Creative writing** (e.g., story generation, poetry),
  - **Dialogue generation** (e.g., chatbots, interactive fiction),
  - **Idea generation** (e.g., brainstorming),
  - **Open-domain question answering**, and
  - **Humor generation** (e.g., jokes).

The **high temperature** setting encourages the model to explore a **wide range of possibilities** and generate more **unpredictable, creative** outputs. This is perfect for tasks where the goal is to **stimulate imagination** or produce **varied responses**, but less suitable for tasks requiring strict accuracy or consistency.

![image](https://github.com/user-attachments/assets/139311d1-2ddc-48a8-a236-7deb32a361ca)

## 2.Top-p Sampling
Top-p sampling, also known as **nucleus sampling**, is a decoding strategy that dynamically selects a subset of words at each step based on their cumulative probability. Instead of a fixed number (`k`) of the most likely words, it considers the smallest group of words whose cumulative probability exceeds a threshold `p` (e.g., 0.9). This introduces controlled randomness while allowing for a flexible set of choices based on the model's confidence.

Here's how Top-p sampling works with an example over 5 steps:


Let's start with the prompt **"The"**, and we'll use `p = 0.9` (the model will select words whose cumulative probability is just above 0.9). Assume the model generates the following probabilities for each step:

### Step-by-step Process (5 Steps)

1. **Step 1: Generate the first word after the prompt**
   - **Prompt**: "The"
   - **Model's next word probabilities**:
     - cat: 0.5
     - dog: 0.2
     - car: 0.15
     - tree: 0.1
     - sun: 0.05
   - **Top-p subset (p = 0.9)**:
     - ["cat" (0.5), "dog" (0.2), "car" (0.15), "tree" (0.1)] — Cumulative probability = 0.95
   - The model randomly selects one of these options. Suppose it picks **"cat"**.
   - **Current output**: "The cat"

2. **Step 2: Generate the next word**
   - **Current text**: "The cat"
   - **Model's next word probabilities**:
     - sits: 0.4
     - jumps: 0.3
     - runs: 0.15
     - sleeps: 0.1
     - looks: 0.05
   - **Top-p subset (p = 0.9)**:
     - ["sits" (0.4), "jumps" (0.3), "runs" (0.15), "sleeps" (0.1)] — Cumulative probability = 0.95
   - The model randomly picks one. Suppose it chooses **"sits"**.
   - **Current output**: "The cat sits"

3. **Step 3: Generate the next word**
   - **Current text**: "The cat sits"
   - **Model's next word probabilities**:
     - on: 0.5
     - under: 0.2
     - beside: 0.15
     - near: 0.1
     - with: 0.05
   - **Top-p subset (p = 0.9)**:
     - ["on" (0.5), "under" (0.2), "beside" (0.15), "near" (0.1)] — Cumulative probability = 0.95
   - The model randomly selects one. Suppose it selects **"on"**.
   - **Current output**: "The cat sits on"

4. **Step 4: Generate the next word**
   - **Current text**: "The cat sits on"
   - **Model's next word probabilities**:
     - the: 0.6
     - a: 0.2
     - his: 0.1
     - its: 0.05
     - that: 0.05
   - **Top-p subset (p = 0.9)**:
     - ["the" (0.6), "a" (0.2), "his" (0.1)] — Cumulative probability = 0.9
   - The model randomly selects one. Suppose it chooses **"the"**.
   - **Current output**: "The cat sits on the"

5. **Step 5: Generate the next word**
   - **Current text**: "The cat sits on the"
   - **Model's next word probabilities**:
     - mat: 0.4
     - rug: 0.3
     - floor: 0.2
     - couch: 0.1
   - **Top-p subset (p = 0.9)**:
     - ["mat" (0.4), "rug" (0.3), "floor" (0.2)] — Cumulative probability = 0.9
   - The model randomly picks one. Suppose it selects **"mat"**.
   - **Final output**: "The cat sits on the mat"

### Summary
Top-p sampling dynamically adjusts the set of words to sample from based on their cumulative probability, ensuring that the most likely options are always included but still allowing for diversity:

- **Pros**: Balances between coherence and randomness by dynamically adjusting the sampling pool based on probabilities. It often produces varied yet reasonable text.
- **Cons**: The threshold `p` needs to be chosen carefully. A too-small `p` may limit diversity, while a too-large `p` may reduce coherence.
- **Use Cases**: Ideal for chatbots, storytelling, and other applications where a mix of diversity and coherence is needed.

<img width="999" alt="image" src="https://github.com/user-attachments/assets/996e441b-72a5-49f6-a84b-d7c4de95a8cf">


**The general recommendation is to alter temperature or Top P but not both.**

## 3.Max Length
You can manage the number of tokens the model generates by adjusting the max length. Specifying a max length helps you prevent long or irrelevant responses and control costs.
Yes, the token limit **does** include the system prompt. In LLMs, all components of the input—such as the system prompt, user input, and any other context—count towards the total token limit. Here's how it breaks down:

### Components Included in the Token Limit
1. **System Prompt**: This is the initial instruction or configuration set by the system to guide the behavior of the model. It defines how the model should respond (e.g., "You are a helpful assistant").
   
2. **User Input**: The actual prompt or question provided by the user. This is the main content that the model processes in conjunction with the system prompt.

3. **Model's Response**: The output generated by the model also contributes to the token count.

4. **Special Tokens**: Any start, end, or separator tokens that the model might use to structure the input and output.

### Example
If the system prompt uses 50 tokens, and the user input takes 100 tokens, that adds up to 150 tokens. If the model's max length is 4,096 tokens, this leaves 3,946 tokens for the model’s response.

### Summary
The entire sequence—**system prompt, user prompt, and generated response**—must stay within the model's token limit.

## 4.Stop Sequences 
A stop sequence is a string that stops the model from generating tokens. Specifying stop sequences is another way to control the length and structure of the model's response. For example, you can tell the model to generate lists that have no more than 10 items by adding "11" as a stop sequence.

## 5.Frequency Penalty
The frequency penalty applies a penalty on the next token proportional to how many times that token already appeared in the response and prompt. The higher the frequency penalty, the less likely a word will appear again. This setting reduces the repetition of words in the model's response by giving tokens that appear more a higher penalty.

## 6.Presence Penalty
The presence penalty also applies a penalty on repeated tokens but, unlike the frequency penalty, the penalty is the same for all repeated tokens. A token that appears twice and a token that appears 10 times are penalized the same. This setting prevents the model from repeating phrases too often in its response. If you want the model to generate diverse or creative text, you might want to use a higher presence penalty. Or, if you need the model to stay focused, try using a lower presence penalty.

**Similar to temperature and top_p, the general recommendation is to alter the frequency or presence penalty but not both.**

**Before starting with some basic examples, keep in mind that your results may vary depending on the version of LLM you use.**
