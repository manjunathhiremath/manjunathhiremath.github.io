---
layout: default
title: Decoding Stratergies
parent: Basics of Prompt Engineering
nav_order: 4
---

# Decoding Stratergies

Decoding strategies are methods used to convert the output probabilities from a language model into text. They play a key role in determining the diversity, coherence, and creativity of the generated text. Here are the top 5 different decoding strategies used in LLMs:

### 1. **Greedy Decoding**
   - **How it works**: Selects the word with the highest probability at each step.
   - **Pros**: Simple and fast; often used when the goal is to produce deterministic and consistent output.
   - **Cons**: Can lead to repetitive or suboptimal results, as it does not explore alternative word choices.
   - **Use Cases**: Suitable for tasks requiring straightforward, fact-based responses or code generation.

### 2. **Beam Search**
   - **How it works**: Explores multiple possible sequences (beams) at each step, retaining the top `k` beams with the highest cumulative probabilities. At the end, the sequence with the highest score is selected.
   - **Pros**: Balances between exploring different possibilities and finding the most likely sequence. It improves coherence compared to greedy decoding.
   - **Cons**: Can be computationally expensive; may still lead to repetitive or generic text if `k` is too large.
   - **Use Cases**: Works well for structured text generation, such as translation or summarization.

### 3. **Top-k Sampling**
   - **How it works**: At each step, instead of choosing the most probable word, the model samples from the top `k` most likely words. This introduces some randomness while focusing on high-probability options.
   - **Pros**: Adds diversity and avoids repetitiveness by not always choosing the top word.
   - **Cons**: The value of `k` needs careful tuning; a too-high `k` can lead to incoherent output, while a too-low `k` may limit diversity.
   - **Use Cases**: Suitable for creative tasks like storytelling, dialogue generation, or casual conversation.

### 4. **Top-p Sampling (Nucleus Sampling)**
   - **How it works**: Selects words from a dynamic set where the cumulative probability is below a threshold `p` (e.g., 0.9). The model then samples from this subset, ensuring more controlled randomness.
   - **Pros**: Provides a balance between coherence and diversity by dynamically adjusting the size of the sampling pool based on probability.
   - **Cons**: Choosing an appropriate `p` value is crucial; a small `p` can be too restrictive, while a large `p` may reduce coherence.
   - **Use Cases**: Widely used for chatbots, storytelling, and any application where both diversity and coherence are needed.

### 5. **Temperature Sampling**
   - **How it works**: Adjusts the probability distribution using a temperature parameter (`T`). A lower `T` (e.g., 0.2) makes the output more deterministic by focusing on higher probabilities, while a higher `T` (e.g., 1.5) increases randomness.
   - **Pros**: Provides fine-grained control over the output’s creativity; flexible for various applications.
   - **Cons**: Extreme values can make output either too repetitive or too chaotic, so it requires tuning based on the task.
   - **Use Cases**: Ideal for exploring variations in creative writing, generating dialogue with different levels of spontaneity, or tailoring output consistency.

These strategies can also be combined or fine-tuned depending on the specific application and desired outcome. For example, top-p sampling with temperature adjustments is a popular combination to optimize both coherence and diversity.


### 1. Greedy Decoding
Greedy Decoding is a straightforward method where the model selects the word with the highest probability at each step to generate a sequence. It doesn’t consider alternative options, leading to the most likely sequence but often lacks diversity. Here's how it works with an example:

Suppose the model is generating the sentence: "The cat sat on the mat."

Assume we start with the prompt **"The"** and the model generates the following probabilities for the next word at each step:

### Step-by-step Process (5 Steps)

1. **Step 1: Generate the first word after the prompt**
   - **Prompt**: "The"
   - **Model's next word probabilities**:
     - **cat**: 0.6
     - dog: 0.2
     - car: 0.1
     - sun: 0.05
     - tree: 0.05
   - **Greedy choice**: The model selects **"cat"** because it has the highest probability (0.6).
   - **Current output**: "The cat"

2. **Step 2: Generate the next word**
   - **Current text**: "The cat"
   - **Model's next word probabilities**:
     - **sat**: 0.7
     - ran: 0.15
     - jumped: 0.1
     - sleeps: 0.05
   - **Greedy choice**: The model selects **"sat"** (0.7).
   - **Current output**: "The cat sat"

3. **Step 3: Generate the next word**
   - **Current text**: "The cat sat"
   - **Model's next word probabilities**:
     - **on**: 0.8
     - under: 0.1
     - beside: 0.05
     - near: 0.05
   - **Greedy choice**: The model selects **"on"** (0.8).
   - **Current output**: "The cat sat on"

4. **Step 4: Generate the next word**
   - **Current text**: "The cat sat on"
   - **Model's next word probabilities**:
     - **the**: 0.9
     - a: 0.05
     - that: 0.03
     - his: 0.02
   - **Greedy choice**: The model selects **"the"** (0.9).
   - **Current output**: "The cat sat on the"

5. **Step 5: Generate the next word**
   - **Current text**: "The cat sat on the"
   - **Model's next word probabilities**:
     - **mat**: 0.85
     - rug: 0.1
     - couch: 0.03
     - grass: 0.02
   - **Greedy choice**: The model selects **"mat"** (0.85).
   - **Final output**: "The cat sat on the mat"

### Summary
Greedy Decoding always picks the word with the highest probability at each step, leading to a deterministic output: "The cat sat on the mat." However, it might not always produce the most creative or diverse text, as it doesn’t explore lower-probability options that might be interesting or varied.


### 2.Beam Search
Beam Search is a decoding strategy that balances exploration and exploitation by considering multiple candidate sequences (beams) at each step. It keeps track of the top `k` sequences with the highest cumulative probabilities, called beams, and expands them iteratively. At the end, the sequence with the highest score is selected.

Here's how Beam Search works with an example, using `k = 2` (2 beams) over 5 steps:

Let's start with the prompt **"The"**, and we'll track the top 2 beams at each step. Assume the model generates the following probabilities for each step:

### Step-by-step Process (5 Steps)

1. **Step 1: Generate the first word after the prompt**
   - **Prompt**: "The"
   - **Model's next word probabilities**:
     - cat: 0.5
     - dog: 0.3
     - car: 0.1
     - tree: 0.1
   - **Top 2 beams**:
     - Beam 1: "The cat" (probability = 0.5)
     - Beam 2: "The dog" (probability = 0.3)
   - **Current beams**: ["The cat", "The dog"]

2. **Step 2: Expand each beam with the next word**
   - **For "The cat"**:
     - sits: 0.6
     - runs: 0.3
     - sleeps: 0.1
   - **For "The dog"**:
     - barks: 0.4
     - jumps: 0.35
     - runs: 0.25
   - **New expanded beams**:
     - "The cat sits" (0.5 * 0.6 = 0.30)
     - "The cat runs" (0.5 * 0.3 = 0.15)
     - "The dog barks" (0.3 * 0.4 = 0.12)
     - "The dog jumps" (0.3 * 0.35 = 0.105)
   - **Top 2 beams**:
     - Beam 1: "The cat sits" (0.30)
     - Beam 2: "The cat runs" (0.15)
   - **Current beams**: ["The cat sits", "The cat runs"]

3. **Step 3: Expand each beam again**
   - **For "The cat sits"**:
     - on: 0.7
     - under: 0.2
     - near: 0.1
   - **For "The cat runs"**:
     - fast: 0.5
     - away: 0.3
     - quickly: 0.2
   - **New expanded beams**:
     - "The cat sits on" (0.30 * 0.7 = 0.21)
     - "The cat sits under" (0.30 * 0.2 = 0.06)
     - "The cat runs fast" (0.15 * 0.5 = 0.075)
     - "The cat runs away" (0.15 * 0.3 = 0.045)
   - **Top 2 beams**:
     - Beam 1: "The cat sits on" (0.21)
     - Beam 2: "The cat runs fast" (0.075)
   - **Current beams**: ["The cat sits on", "The cat runs fast"]

4. **Step 4: Expand each beam further**
   - **For "The cat sits on"**:
     - the: 0.8
     - a: 0.15
     - his: 0.05
   - **For "The cat runs fast"**:
     - towards: 0.4
     - past: 0.35
     - around: 0.25
   - **New expanded beams**:
     - "The cat sits on the" (0.21 * 0.8 = 0.168)
     - "The cat sits on a" (0.21 * 0.15 = 0.0315)
     - "The cat runs fast towards" (0.075 * 0.4 = 0.03)
     - "The cat runs fast past" (0.075 * 0.35 = 0.02625)
   - **Top 2 beams**:
     - Beam 1: "The cat sits on the" (0.168)
     - Beam 2: "The cat sits on a" (0.0315)
   - **Current beams**: ["The cat sits on the", "The cat sits on a"]

5. **Step 5: Expand the final set of beams**
   - **For "The cat sits on the"**:
     - mat: 0.6
     - rug: 0.3
     - floor: 0.1
   - **For "The cat sits on a"**:
     - chair: 0.5
     - cushion: 0.3
     - bench: 0.2
   - **New expanded beams**:
     - "The cat sits on the mat" (0.168 * 0.6 = 0.1008)
     - "The cat sits on the rug" (0.168 * 0.3 = 0.0504)
     - "The cat sits on a chair" (0.0315 * 0.5 = 0.01575)
     - "The cat sits on a cushion" (0.0315 * 0.3 = 0.00945)
   - **Top 2 beams**:
     - Beam 1: "The cat sits on the mat" (0.1008)
     - Beam 2: "The cat sits on the rug" (0.0504)

### Final Output
- The model selects the beam with the highest score: **"The cat sits on the mat"**.

### Summary
Beam Search considers multiple possible sequences at each step, expanding them based on their probabilities. By keeping the top `k` beams, it explores a wider space of options compared to greedy decoding, often leading to more coherent and contextually appropriate outputs. However, it is more computationally intensive and may still converge to repetitive or generic sequences if `k` is too high.

### 3.Top-K Sampling
Top-k sampling is a decoding strategy where, instead of always choosing the most likely next word (as in greedy decoding), the model considers the top `k` most probable words at each step and randomly samples from them. This introduces controlled randomness, increasing diversity in the output while still focusing on likely options. 

Here's how Top-k sampling works with an example over 5 steps:

Let's start with the prompt **"The"**, and we'll use `k = 3` (the model will consider the top 3 most probable words at each step). Assume the model generates the following probabilities:

### Step-by-step Process (5 Steps)

1. **Step 1: Generate the first word after the prompt**
   - **Prompt**: "The"
   - **Model's next word probabilities**:
     - cat: 0.5
     - dog: 0.3
     - car: 0.15
     - tree: 0.05
   - **Top 3 words** (k = 3): ["cat", "dog", "car"]
   - The model randomly selects one of these three options. Suppose it picks **"dog"**.
   - **Current output**: "The dog"

2. **Step 2: Generate the next word**
   - **Current text**: "The dog"
   - **Model's next word probabilities**:
     - barks: 0.4
     - runs: 0.35
     - jumps: 0.2
     - sleeps: 0.05
   - **Top 3 words** (k = 3): ["barks", "runs", "jumps"]
   - The model randomly selects one of these. Suppose it chooses **"runs"**.
   - **Current output**: "The dog runs"

3. **Step 3: Generate the next word**
   - **Current text**: "The dog runs"
   - **Model's next word probabilities**:
     - fast: 0.6
     - quickly: 0.2
     - away: 0.15
     - towards: 0.05
   - **Top 3 words** (k = 3): ["fast", "quickly", "away"]
   - The model randomly picks one. Suppose it selects **"fast"**.
   - **Current output**: "The dog runs fast"

4. **Step 4: Generate the next word**
   - **Current text**: "The dog runs fast"
   - **Model's next word probabilities**:
     - towards: 0.5
     - past: 0.3
     - away: 0.2
   - **Top 3 words** (k = 3): ["towards", "past", "away"]
   - The model randomly selects one of these. Suppose it chooses **"past"**.
   - **Current output**: "The dog runs fast past"

5. **Step 5: Generate the next word**
   - **Current text**: "The dog runs fast past"
   - **Model's next word probabilities**:
     - the: 0.6
     - a: 0.3
     - his: 0.1
   - **Top 3 words** (k = 3): ["the", "a", "his"]
   - The model randomly selects one. Suppose it picks **"the"**.
   - **Current output**: "The dog runs fast past the"

### Summary
Top-k sampling introduces randomness by allowing the model to choose from the top `k` words at each step, rather than always selecting the single most probable word. This increases diversity and creativity in the output while still maintaining a focus on likely word choices.

- **Pros**: More varied and creative outputs compared to greedy decoding.
- **Cons**: The value of `k` must be chosen carefully. If `k` is too high, the output may become incoherent. If `k` is too low, the output may lack diversity.
- **Use Cases**: Suitable for storytelling, dialogue generation, and creative writing, where diverse responses are desired.

### 4.Top-p Sampling
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

### 5. Temperature
  Temperature sampling is a decoding strategy that adjusts the probability distribution of the model’s next-word predictions to control randomness and creativity in the output. By modifying the temperature parameter (`T`), you can make the model's predictions either more deterministic (lower temperature) or more diverse (higher temperature).

- **Low temperature (`T < 1`)**: Makes the model more confident, sharpening the probability distribution. This reduces randomness, making the output more predictable.
- **High temperature (`T > 1`)**: Flattens the probability distribution, increasing randomness and diversity, which can lead to more creative and varied outputs.

In language models, the temperature parameter (`T`) is used to adjust the probabilities of predicted tokens. The formula for temperature scaling is as follows:
Here's the formatted content for a .md file:

In language models, the temperature parameter (`T`) is used to adjust the probabilities of predicted tokens. The formula for temperature scaling is as follows:

Here's the formatted content for a .md file:

# Temperature Adjustment in Language Model Text Generation

## Example Setup

**Prompt**: "The"  
**Temperature (`T`)**: 1.2

Initial probabilities for the next token:

| Token | Original Probability (p(w)) |
|-------|----------------------------|
| cat   | 0.5                        |
| dog   | 0.3                        |
| car   | 0.15                       |
| tree  | 0.05                       |

## Step-by-Step Process

### Adjust Probabilities with Temperature

1. **Original Probabilities**:
   - cat: 0.5
   - dog: 0.3
   - car: 0.15
   - tree: 0.05

2. **Adjust the probabilities** using temperature T = 1.2:
   - Compute $\frac{1}{T} = \frac{1}{1.2} \approx 0.8333$
   - Raise each probability to the power of $\frac{1}{T}$:
     - $p_{\text{new}}(\text{cat}) = 0.5^{0.8333} \approx 0.4192$
     - $p_{\text{new}}(\text{dog}) = 0.3^{0.8333} \approx 0.2462$
     - $p_{\text{new}}(\text{car}) = 0.15^{0.8333} \approx 0.1122$
     - $p_{\text{new}}(\text{tree}) = 0.05^{0.8333} \approx 0.0262$

3. **Normalization**:
   - Calculate the normalization factor Z:
     $Z = 0.4192 + 0.2462 + 0.1122 + 0.0262 \approx 0.8038$

   - Normalize the adjusted probabilities:
     - $p_{\text{new}}(\text{cat}) = \frac{0.4192}{0.8038} \approx 0.5207$
     - $p_{\text{new}}(\text{dog}) = \frac{0.2462}{0.8038} \approx 0.3053$
     - $p_{\text{new}}(\text{car}) = \frac{0.1122}{0.8038} \approx 0.1391$
     - $p_{\text{new}}(\text{tree}) = \frac{0.0262}{0.8038} \approx 0.0326$

4. **Random Selection**:
   - Model samples from adjusted distribution → selects "cat"
   - **Current output**: "The cat"
