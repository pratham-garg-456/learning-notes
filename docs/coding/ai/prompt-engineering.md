---
title: Prompt Engineering
---

# Prompt Engineering

## LLM output configuration

Effective prompt engineering requires setting these configurations optimally for a task.

### 1. Output length

- **What is it?** How many words or pieces (tokens) the model is allowed to generate in its answer.
- **Why care?**
    - More tokens means longer answers, more compute cost, and potentially more fluff.
    - Limiting tokens just makes the model stop at the limit. It doesn't make the answer fancier or more concise.
- **How to control?**
    - Set a max token number in settings.
    - Or ask for a short answer in your prompt, for example "Explain in 1 sentence."

### 2. Sampling controls: how the model picks words

LLMs don't just pick the next word. They assign a probability to every possible next word, then pick one based on your settings.

**A. Temperature**

- **What is it?** Controls how random or creative the word selection is.
- **How does it work?**
    - **Low temperature (0):** always picks the most likely word. Very predictable, like a robot reciting facts.
    - **High temperature (1+):** makes choices more randomly. Good for brainstorming, poetry, and creative tasks.
- **When to use what?**
    - **0:** math, logic, or fact-based answers (deterministic, always the same answer).
    - **0.2 to 0.5:** mostly factual with a bit of variety.
    - **0.7+:** creative, varied outputs.

**B. Top-K**

- **What is it?** Only consider the top K most likely next words and ignore the rest.
- **Example:** K=1 picks only the most likely word (like temperature 0). K=10 picks randomly among the top 10 candidates.

**C. Top-P (nucleus sampling)**

- **What is it?** Instead of a fixed number of words (K), consider the smallest set of words whose total probability adds up to P.
- **Example:** P=0.9 considers words whose combined chance is 90%, ignoring the rare, weird words.

## Prompting techniques

1. **General (zero-shot) prompting**
    - What: just ask the model to do something, with no examples.
    - Example: "Classify this movie review as positive, neutral, or negative."
    - Config: low temperature (for example 0.1) for factual, predictable results.
    - When: the task is straightforward and doesn't need creativity.
2. **One-shot and few-shot prompting**
    - What: give the model 1 (one-shot) or a few (few-shot) example prompts and responses.
    - Example:

        ```text
        User: Order: Large pepperoni pizza
        Model: {"size": "large", "type": "pepperoni"}
        ```

    - Config: low temperature (for example 0.1), but increase the token limit for longer outputs.
    - When: you want the model to mimic a pattern or format.
3. **System, contextual, and role prompting**
    - **System:** tell the model what its job is and how to format its output. Example: "You are a JSON formatter. Output only JSON."
    - **Contextual:** give background details to help the model tailor answers. Example: "You're writing for a retro gaming blog."
    - **Role:** tell the model to act as a particular character or profession. Example: "Act as a travel guide."
    - Config: often higher temperature (for example 1), with Top-K/Top-P for creativity.
    - When: you need a specific style, structure, or persona.
4. **Step-back prompting**
    - What: prompt the model to answer a related general question first, then use that info for the main task.
    - Example: first "What makes a good video game story?", then "Write a story using those elements."
    - Why: activates broader knowledge and reduces bias.
5. **Chain of Thought (CoT) prompting**
    - What: ask the model to "think step by step" and show its reasoning.
    - Example: "Let's think step by step..." for math problems.
    - Config: temperature 0 (deterministic) for reliable reasoning.
    - When: you want logical, transparent answers for complex problems.
6. **Self-consistency**
    - What: run the same prompt several times at a high temperature, collect multiple answers, and pick the majority answer.
    - Why: increases accuracy by aggregating diverse reasoning paths.
7. **Tree of Thoughts (ToT)**
    - What: like CoT, but explores multiple reasoning paths at once in a tree structure.
    - When: tasks needing exploration of many possible solutions.
8. **ReAct (Reason and Act)**
    - What: the model alternates between thinking and performing actions (like searching), then updates its plan.
    - Example: "How many kids do Metallica members have?" The model looks up each member's info and aggregates it.
    - When: tasks that need research or external tool use.
9. **Automatic Prompt Engineering (APE)**
    - What: the model creates multiple prompt versions, tests them, and picks the best one automatically.
    - When: to optimize prompts without manual trial and error.
10. **Code prompting**
    - What: prompts for generating, explaining, translating, or debugging code.
    - Config: use correct formatting (like Markdown) for best results.
    - Warning: always review and test generated code.

## How output configurations relate

- **Temperature:** controls randomness and creativity. Lower for accuracy, higher for creativity.
- **Top-K:** limits choices to the top K likely words. Lower is safer, higher gives more variety.
- **Top-P:** limits to the smallest set of words whose probabilities add up to P. Lower is safer, higher gives more variety.

**Best practices:**

- Give clear, concise prompts.
- Be specific about the output.
- Use positive instructions ("do this") rather than negative constraints ("don't do this").
- Document what works.

### Summary table

| Technique | Main use | Example config | When to use |
| --- | --- | --- | --- |
| Zero-shot | No examples | temp=0.1 | Simple, factual tasks |
| Few-shot | 1+ examples | temp=0.1, more tokens | When format or pattern is important |
| System/Role/Context | Set style and structure | temp=1, Top-K=40 | Specific persona or output format |
| Step-back | Prep background info | Any | When broader knowledge is needed |
| Chain of Thought | Show reasoning | temp=0 | Logic-heavy, reasoning tasks |
| Self-consistency | Aggregate outputs | temp=high | When a single run isn't reliable |
| Tree of Thoughts | Explore options | Any | Complex, exploratory tasks |
| ReAct | Reason + take actions | Any | Needs research or tool use |
| Auto Prompt Eng. | Automate prompt design | Any | Optimize prompts automatically |
| Code prompting | Code tasks | Proper formatting | Coding, debugging, code explanations |

## Best practices

1. **Provide examples.** Examples teach the model what a good answer looks like (structure, style, tone). Use one-shot or few-shot. Make sure examples are clear and high quality.
2. **Design with simplicity.** Simple, clear prompts are easier for you and the model to understand. Use direct verbs ("Classify", "Summarize", "Generate") and avoid unnecessary info.
3. **Be specific about the output.** Vague prompts give vague outputs. Clearly state what you want (format, length, style). Example: "Return the answer as a JSON object."
4. **Use instructions over constraints.** Telling the model what to do ("Generate a summary...") works better than listing what not to do. Only use constraints for strict safety or format needs.
5. **Control the max token length.** More tokens means higher cost and slower responses. Set a max token limit in your config, or specify the output length in your prompt ("in one sentence").
6. **Use variables in prompts.** Makes prompts reusable and dynamic. Insert placeholders for changing info (like `{user_input}`, `{date}`).
7. **Experiment with input formats and writing styles.** Changing how you ask can change the answer. Try different wordings, styles, and types (question vs instruction).
8. **Mix up classes for few-shot classification.** Prevents the model from just copying order and structure. Shuffle example order and include all possible classes in your few-shot examples.
9. **Adapt to model updates.** Models change, and newer ones may behave differently. Test and tweak prompts as new models or versions are released.
10. **Experiment with output formats.** Structured formats (like JSON) reduce hallucinations and improve consistency. Ask for JSON, XML, tables, etc. Use schemas to guide the model.
    - Use tools like `json-repair` to fix incomplete outputs.
    - Give the model a JSON schema for complex tasks. It acts as a blueprint.
11. **Experiment together with others.** More people means more ideas and better prompts. Collaborate, compare, and select the best results.
12. **Chain of Thought best practices.**
    - **Answer after reasoning:** ask the model to show its steps, then give the answer at the end.
    - **Extract the final answer:** make it easy to pull out just the answer from the output.
    - **Set temperature to 0** for reasoning tasks (like math) for consistent results.
13. **Documentation.** Keep records for future use, debugging, and improvement. Log the prompt name, goal, model, settings (temperature, top-k, top-p, token limit), prompt text, and output. Prompting is trial and error, so keep refining based on what works.

### Summary table

| Best practice | Key point |
| --- | --- |
| Provide examples | Use few-shot or one-shot for teaching and guiding the model |
| Simplicity | Be clear and straightforward |
| Specificity | State exactly what you want |
| Instructions over constraints | Tell what to do, not just what not to do |
| Max token length | Limit for cost and clarity |
| Variables | Make prompts reusable and dynamic |
| Input/style experimentation | Try different phrasings and styles |
| Mix classes | Prevent overfitting in classification |
| Model adaptation | Update prompts as models evolve |
| Output formats and schemas | Use JSON/XML for structure and clarity |
| Collaborate | Work with others for better ideas |
| CoT tips | Reason step by step, answer last, temp=0 |
| Document everything | Track prompts, settings, outputs, and lessons |
| Iterate | Refine based on results |

## Practice Questions

??? question "1. What does temperature control, and what values suit what tasks?"

    How random or creative the word selection is. 0 always picks the most likely word (math, logic, facts). 0.2 to 0.5 is mostly factual with a bit of variety. 0.7 and above is for creative, varied outputs.

??? question "2. What is the difference between Top-K and Top-P?"

    Top-K considers only the K most likely next words. Top-P considers the smallest set of words whose combined probability adds up to P (for example 90%), ignoring rare words.

??? question "3. What is the difference between zero-shot and few-shot prompting?"

    Zero-shot gives just the task with no examples. Few-shot gives one or a few example prompts and responses so the model mimics a pattern or format.

??? question "4. What are system, contextual, and role prompting?"

    System: tells the model its job and output format. Contextual: gives background details. Role: tells the model to act as a particular character or profession.

??? question "5. What is chain-of-thought prompting, and what temperature is recommended?"

    Asking the model to think step by step and show its reasoning, which helps on multi-step problems. Use temperature 0 for consistent reasoning.

??? question "6. What is self-consistency?"

    Running the same prompt several times at a high temperature, collecting multiple answers, and picking the majority answer.

??? question "7. What is ReAct?"

    The model alternates between reasoning and taking actions (like searching), then updates its plan. Useful for tasks that need research or external tools.

??? question "8. Why give instructions instead of constraints?"

    Telling the model what to do works better than listing what not to do. Use constraints only for strict safety or format needs.

??? question "9. What should you record when documenting prompts?"

    The prompt name, goal, model, settings (temperature, top-k, top-p, token limit), prompt text, and output.
