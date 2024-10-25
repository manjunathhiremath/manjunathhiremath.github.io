---
layout: default
title: System Prompt vs User Prompt
parent: Basics of Prompt Engineering
nav_order: 1
---

# System Prompt vs User Prompt

In the context of AI models like GPT, **system prompts** and **user prompts** serve distinct roles in shaping the conversation and guiding the AI's responses. Here’s a breakdown of their characteristics:

### 1. **System Prompt:**
- **Role**: Provides a set of guidelines or instructions for the AI model before any user input is processed. It defines the behavior, tone, and style of the AI throughout the conversation.
- **Characteristics**:
  - **Instructional**: Directs the model on how to behave, such as being polite, concise, or professional.
  - **Context-setting**: May include information about the conversation's purpose (e.g., as a technical assistant, a tutor, or a friendly chatbot).
  - **Static**: Remains consistent throughout the session unless explicitly modified by an API call or setup.
  - **Foundation**: Acts as a base layer, ensuring the AI maintains certain standards regardless of user inputs.
- **Examples**:
  - "You are a helpful assistant."
  - "You are an expert in providing legal advice and must answer questions accurately and professionally."

### 2. **User Prompt:**
- **Role**: The input provided by the user, which the AI responds to. It typically carries the user's query, command, or request for information.
- **Characteristics**:
  - **Dynamic**: Varies based on user input, changing with each interaction.
  - **Direct**: Usually straightforward, expressing the user's intent, question, or requirement.
  - **Guiding the Response**: Determines the specific focus of the AI's response and may override certain behaviors based on the request (e.g., asking for detailed explanations or brief summaries).
  - **Personalized**: Tailored to the user’s needs and context.
- **Examples**:
  - "Can you explain the difference between supervised and unsupervised learning?"
  - "What is the weather like today?"

Together, the system and user prompts create a structured and interactive environment where the AI’s behavior (set by the system prompt) adapts dynamically to user inputs (user prompts).
