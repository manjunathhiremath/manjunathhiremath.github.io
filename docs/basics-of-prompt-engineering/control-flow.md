---
layout: default
title: Best Practices to Design System Prompt
parent: Basics of Prompt Engineering
nav_order: 2
---

# Best Practices to Design System Prompt

Here's a comparison of **wrong** versus **correct** system prompts, illustrating how to structure them properly for optimal AI behavior.

### 1. **Context Clarity**
   - **Wrong System Prompt**: "You are a chatbot. Answer questions."
     - **Issue**: This is too vague and lacks context. It doesn’t specify how the chatbot should respond (e.g., tone, detail, role).
   
   - **Correct System Prompt**: "You are a friendly and knowledgeable assistant specializing in machine learning. Answer questions with clear explanations, and provide examples where possible."
     - **Fix**: This provides a specific role, tone (friendly and knowledgeable), and instructions (use clear explanations and examples). It ensures the AI understands its context and behavior.

### 2. **Tone and Style Specification**
   - **Wrong System Prompt**: "Be helpful."
     - **Issue**: This is overly general and does not define the tone or style (e.g., professional, casual, or educational) the AI should adopt.
   
   - **Correct System Prompt**: "You are a professional assistant. Respond to queries in a concise and formal manner, providing information in a respectful and informative style."
     - **Fix**: This sets a specific style (formal) and tone (respectful and informative), ensuring the AI maintains a consistent approach in its responses.

### 3. **Overly Restrictive Instructions**
   - **Wrong System Prompt**: "Always respond in less than 20 words."
     - **Issue**: This is too limiting and doesn’t allow for flexibility. Not all questions can be adequately addressed in such a brief response.
   
   - **Correct System Prompt**: "Respond concisely, but provide enough detail to fully address the user’s query. Use longer explanations when needed for clarity."
     - **Fix**: This still emphasizes conciseness but allows the AI to adapt when longer explanations are necessary, balancing detail and brevity.

### 4. **Ambiguous Role Definition**
   - **Wrong System Prompt**: "You are a teacher."
     - **Issue**: This is not specific enough. It doesn’t clarify what subject the AI should teach, what kind of teacher it is, or how it should teach (e.g., patient, detailed).
   
   - **Correct System Prompt**: "You are an experienced math teacher for high school students. Explain concepts clearly, use simple language, and provide step-by-step solutions."
     - **Fix**: This specifies the subject (math), the audience (high school students), and the teaching style (clear, simple language, step-by-step), ensuring the AI knows exactly how to respond.

### 5. **Contradictory Instructions**
   - **Wrong System Prompt**: "Be concise but give a lot of detail in your answers."
     - **Issue**: This is contradictory—being concise and giving a lot of detail can’t be done simultaneously without clarity on which is more important.
   
   - **Correct System Prompt**: "Provide detailed explanations where necessary, but keep the response as concise as possible. Prioritize clarity over brevity when explaining complex topics."
     - **Fix**: This clarifies that while the AI should aim for conciseness, clarity and detail should be prioritized when the topic requires it.

### 6. **Lack of Role Specification for Special Use Cases**
   - **Wrong System Prompt**: "Answer questions."
     - **Issue**: This lacks any context about the kind of questions the AI should expect or how it should handle specific scenarios, like sensitive topics or technical queries.
   
   - **Correct System Prompt**: "You are a customer support agent for a technology company. Address customer queries politely, explain technical details in simple terms, and ensure that any issues are resolved or escalated properly."
     - **Fix**: This defines the AI’s role (customer support agent), the nature of questions (technology-related), and the approach (polite, simple explanations, resolving/escalating issues), ensuring clarity and consistency.

Here are additional examples comparing **wrong** versus **correct** system prompts to further illustrate effective design:

### 7. **Incomplete Instructions for Specialized Tasks**
   - **Wrong System Prompt**: "Translate text."
     - **Issue**: This is too generic and doesn’t specify the languages or style of translation (e.g., formal, casual).
   
   - **Correct System Prompt**: "You are a professional translator. Translate the given text from English to French, maintaining a formal tone and ensuring accuracy in technical terms."
     - **Fix**: This specifies the language pair (English to French), the tone (formal), and the importance of accuracy, ensuring the AI delivers translations that align with the intended purpose.

### 8. **Unclear Guidance for Creative Tasks**
   - **Wrong System Prompt**: "Write a story."
     - **Issue**: This doesn’t provide enough context or guidelines on the theme, audience, or length, resulting in inconsistent output.
   
   - **Correct System Prompt**: "Write a short, imaginative story for children aged 5-8. Use simple language, animal characters, and end with a positive moral lesson."
     - **Fix**: This defines the story’s length (short), audience (children aged 5-8), style (simple language, animal characters), and goal (a moral lesson), guiding the AI to create appropriate content.

### 9. **Lack of Clarity on Formality Levels**
   - **Wrong System Prompt**: "Help the user."
     - **Issue**: It doesn’t clarify how the AI should interact (e.g., casually, formally, professionally), leading to unpredictable behavior.
   
   - **Correct System Prompt**: "You are a polite and professional virtual assistant. Always address users respectfully and provide answers in a formal and well-structured manner."
     - **Fix**: This specifies the style (polite, professional), tone (formal), and approach (structured responses), ensuring consistent interactions.

### 10. **Non-Specific Role Instruction for Technical Guidance**
   - **Wrong System Prompt**: "Answer coding questions."
     - **Issue**: It’s not clear what programming languages the AI should be knowledgeable about, the expected level of detail, or the target audience’s skill level.
   
   - **Correct System Prompt**: "You are a coding assistant specializing in Python and JavaScript. Provide detailed explanations with code snippets suitable for beginners and focus on best practices."
     - **Fix**: This defines the programming languages (Python and JavaScript), the target audience (beginners), and the depth of explanations (detailed, with code snippets), ensuring the AI responds appropriately.

### 11. **Inadequate Instructions for Ethical or Sensitive Topics**
   - **Wrong System Prompt**: "Discuss controversial issues."
     - **Issue**: This lacks specificity and doesn’t provide guidance on handling sensitivity, leading to potential misuse or harmful responses.
   
   - **Correct System Prompt**: "You are a neutral and thoughtful assistant. When discussing controversial topics, present balanced viewpoints, avoid taking sides, and provide information based on reliable sources without promoting bias."
     - **Fix**: This sets clear expectations for neutrality, balance, and reliance on credible information, ensuring that the AI handles sensitive subjects responsibly.

### 12. **Ambiguous Guidance for Summarization**
   - **Wrong System Prompt**: "Summarize text."
     - **Issue**: It doesn’t specify the length of the summary, the level of detail, or the target audience, leading to inconsistent results.
   
   - **Correct System Prompt**: "Provide a concise summary of the given text, focusing on the main points. Limit the summary to three sentences and ensure it is suitable for a general audience with no technical background."
     - **Fix**: This clarifies the length (three sentences), the focus (main points), and the intended audience (general, non-technical), resulting in more precise outputs.

### 13. **Vague Instruction for Interactive Tasks**
   - **Wrong System Prompt**: "Play a game."
     - **Issue**: It doesn’t define the type of game, the rules, or the user’s role, resulting in unclear or ineffective interactions.
   
   - **Correct System Prompt**: "You are a trivia game host. Ask the user multiple-choice questions about world history, provide three options for each, and give feedback on whether their answer is correct or not. Offer the option to play again after each question."
     - **Fix**: This establishes the role (game host), the game type (trivia), and the structure (multiple-choice with feedback), creating a clear and engaging experience.

### 14. **Inconsistent Tone for Customer Support Scenarios**
   - **Wrong System Prompt**: "Help customers with issues."
     - **Issue**: This lacks specificity, failing to set the tone (e.g., empathy, professionalism) or the approach for problem-solving.
   
   - **Correct System Prompt**: "You are a customer support assistant. Address customer concerns with empathy and professionalism, guiding them through troubleshooting steps clearly and ensuring they feel supported throughout the process."
     - **Fix**: This defines the tone (empathetic, professional) and approach (step-by-step guidance), ensuring consistent and helpful support.

### 15. **Unclear Instruction for Teaching Scenarios**
   - **Wrong System Prompt**: "Teach about science."
     - **Issue**: This is too general and doesn’t specify the subject area, depth of content, or target audience (e.g., children, college students).
   
   - **Correct System Prompt**: "You are a science tutor for middle school students. Explain concepts related to basic physics, such as gravity and motion, using simple analogies and visuals when appropriate."
     - **Fix**: This specifies the target audience (middle school students), the subject area (basic physics), and the teaching method (simple analogies and visuals), allowing the AI to provide appropriate educational content.

These examples demonstrate the importance of clarity, specificity, and consistency in system prompts to ensure the AI delivers useful, accurate, and context-appropriate responses.
