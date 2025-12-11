# Week 1: Introduction to Coding LLMs and AI Development

## Lecture 1 slide notes

More excitement than ever before in AI

Bad News

- High unemployment for CS grads
- 20% drop in enrollment for Stanford CS this year

Good News
- A competent engineer can be orders of magnitude more productive with AI

Course won't teach "vibe coding" but how to truly become a 10x engineer.

Alternative to vibe coding: human-agent engineering. 
- Focus on skills not replaced by AI
- Become the tech lead.
- Help give code context to LLMs
- The key is to know good code from bad code. Being a competent code reviewer is now essential.

LLMs
- Autoregressive models for next-token prediction.
- Causal self-attention mechanism
- Output is probability distribution of the most likely next word

Training process
- Stage 1: self-supervised learning
  - Train on language/code from public sources, trillions of tokens
- Stage 2: supervised finetuning
  - Train to follow instructions, give high quality question response answers
- Stage 3: preferencing tuning
  - Align outputs with human preferences, reward model for preferred output
- Reasoning models (thinking)

## Lecture 2 slide notes

### LLM Power Prompting

- Prompting is the *lingua franca* for programming with LLMs, "Software 3.0"
- Some magic to "LLM-whispering" to make the most of LLM black box. But some established techniques have empirically improved LLM performance
- Helps understand what's going on under the hood with Claude Code / Cursor.

### Zero-shot prompting

Write one prompt to do something with no additional context/support/examples.

### K-shot prompting

Provide *k* examples (shots).

- 1, 3, 5 - empirically justified numbers of shots
- Good for domain specific APIs the LLM hasn't been trained on
- Avoid over-constraining with too many examples (I can imagine the LLM will over-analyse and find incidental patterns between examples that you did not intend)
- Provide examples in the prompt using `<example>...</example>` tags

### Chain-of-Thought (CoT) Prompting

Prompt LLM to demonstrate its reasoning

- Multi-shot CoT: give examples (shots) of how the LLM should output it's CoT reasoning for e.g. coding tasks, than ask it to reason on a specific problem.
- Zero-shot CoT: give pointers but not specific examples ("think step-by-step")
- Best for multiple logical steps in programming or math
- How reasoning models work

### Self-Consistency Prompting

- Sample multiple outputs from the same prompt and aggregate most common results
- LLMs are probabilistic in nature (predict next word) but this technique works because there are several reasoning paths the model can go down and we want to filter out paths that are wrong (while levaraging exploration within the correct reasoning path)

### Tool use/agency/autonomy

- Allow LLMs to use external systems, e.g. run unit tests
- One of the best ways to reduce hallucinations and produce verifiable results

### Retrieval Augmented Generation

- Provide LLM with contextual data
- Keep them up to date without retraining
- Adds citations to LLM output

### Reflection

- Make LLM reflect on its own output
- Can add verbal feedback from environment (e.g. the unit tests have passed/failed)
- Multi-turn prompting: have a first try, reflect on result and give a second try if needed.
- This is why we get fully agentic behaviour in coding agents.

### Additional terms
- System prompt: LLMs will have a system prompt that their creators use that provides the context and rules of the LLM's output, before it ever reads the user's prompt
- User prompt: everything discussed above in general
- Assistant prompt: additions to the user prompt, giving a final prompt that the LLM will actually use to generate content

Best practices - Anthropic provide a Claude prompt improver to provide better structure to prompts. Prompts should be clear, and consider role prompting.

> You are a helpful assistant that loves programming at the level of a senior software developer and is very detailed and pedantic in your answers.

Key takeaway: prompts should be formatted with structure, xml-style tags seem to work well.

Be explicit, decompose tasks.

## Video: Deep Dive into LLMs like ChatGPT by Andrej Karpathy

- [Tiktokenizer](https://tiktokenizer.vercel.app/) visually demonstrates how well known LLMs will tokenzie strings.
- This [LLM Visualization website](https://bbycroft.net/llm) can help to visualize the mathematical function behind how the GPT LLMs generate output.
- The [DeepSeek-R1 paper](https://arxiv.org/abs/2501.12948) was really one of the first papers to publicly shed light on the process of reinforcement learning for an LLM.

## Article: [Prompt Engineering Overview](https://cloud.google.com/discover/what-is-prompt-engineering) by Google

Reiterating a lot of what was on the slides - prompt engineering techniques and common sense examples of concise prompting.

## Site: [Prompt Engineering Guide](https://www.promptingguide.ai/techniques) by promptingguide.ai

Good guide of prompting techniques with citations showing how techniques are proven to work empirically.
- Few-shot worked well for e.g. categorising sentiment of a movie, but not for number calculations where CoT reasoning allows more thinking time to computer the answer.
- Zero-shot CoT is CoT without specific examples given, just a trigger phrase like "think step-by-step" is enough to get the model to ruminate on a problem for longer.
- Auto-CoT - sort of like self-generated few-shot prompting, the model gives itself reasoning examples to follow, and then uses this examples on a new question without further examples.
- Meta Prompting: specifying the structure and syntax that the answer should be given in, provide an abstract framework for the model to follow. For example, the relationship between how models are trained on maths problem and how LaTeX is one of the better and more well-supported formats for precisely specifying maths is interesting. I'm not sure if "thinking in LaTeX" specifically would help or hinder the model, it probably depends.
- Tree of Thoughts (ToT), like Chain of Thought but model traverses a tree of intermediate thoughts, can process alternative thoughts at a particular step, and can backtrack to reach a desired outcome.
- Automatic Prompt Engineer (APE) is a way to use LLMs to generate instructions/prompts. It finds the prompt "Let's work this out in a step by step way to be sure we have the right answer" is better than the human-designed "Let's think step by step".

## Video: [AI prompt engineering: A deep dive](https://www.youtube.com/watch?v=T9aRN5JkmL8) by Anthropic

Informal discussion about prompt engineering, interesting to hear the perspective of some of the important people in this novel discipline - the people working on Claude at Anthropic.

## Document: [How OpenAI uses Codex](https://cdn.openai.com/pdf/6a2631dc-783e-479b-b1a4-af0cfbd38630/how-openai-uses-codex.pdf)

Suggestions on how to use the Codex coding tool in practice, a lot of the suggestions mirror what I've been using GitHub Copilot and Claude Sonnet to do every day at work, however some ideas I've not tried, e.g. "Generate a plan to refactor this service 
and split it into smaller modules."