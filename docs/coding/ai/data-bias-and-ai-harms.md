---
title: Data Bias and AI Harms
---

# Recognize Data Bias and AI Harms

## Bias, drift, and knowledge cutoff

A thorough understanding of concepts in responsible AI, such as bias, drift, and knowledge cutoff, can help you use AI more ethically and with greater accountability.

## Harms and biases

Engaging with AI responsibly requires knowledge of its inherent biases. **Data biases** are circumstances in which systemic errors or prejudices lead to unfair or inaccurate information, resulting in biased outputs.

Biased output can cause many types of harm to people and society, including:

- **Allocative harm:** wrongdoing that occurs when an AI system's use or behavior withholds opportunities, resources, or information in domains that affect a person's well-being.
    - **Example:** a property manager uses an AI tool for background checks to screen tenants. The tool misidentifies an applicant and deems them a risk because of a low credit score. They are denied an apartment and lose the application fee.
    - **How to mitigate:** evaluate all AI-generated content before you incorporate it into your work or share it. Double-check AI output against other sources.
- **Quality-of-service harm:** AI tools do not perform as well for certain groups of people based on their identity.
    - **Example:** when speech-recognition technology was first developed, the training data didn't have many examples of speech patterns of people with disabilities, so the devices often struggled to parse this type of speech.
    - **How to mitigate:** specify diversity by adding inclusive language to your prompt. If a generative AI tool fails to consider certain groups or identities, address that when you iterate on the prompt.
- **Representational harm:** an AI tool reinforces the subordination of social groups based on their identities.
    - **Example:** when translation technology was first developed, certain outputs skewed masculine or feminine. Words like "nurse" and "beautiful" skewed feminine, and "doctor" and "strong" skewed masculine.
    - **How to mitigate:** challenge assumptions. If a tool gives a biased response, identify and address the issue when you iterate on your prompt, and ask the tool to correct the bias.
- **Social system harm:** macro-level societal effects that amplify existing class, power, or privilege disparities, or cause physical harm, as a result of the development or use of AI tools.
    - **Example:** unwanted **deepfakes**, AI-generated fake photos or videos of real people saying or doing things they did not.
    - **How to mitigate:** fact-check and cross-reference output. Some tools provide sources. You can also use a search engine or ask an expert. Running a prompt through two or more resources helps you identify possible inaccurate output.
- **Interpersonal harm:** the use of technology to create a disadvantage to certain people that negatively affects their relationships with others or causes a loss of their sense of self and agency.
    - **Example:** someone takes control of an in-home device at their previous apartment to play an unwanted prank on a former roommate, causing a loss of sense of self and agency.
    - **How to mitigate:** consider the effects of using AI and use your best judgment and critical thinking. Ask yourself whether AI is right for the task. Like any technology, AI can be beneficial or harmful depending on how it is used, and it is the user's responsibility to avoid causing harm.

## Drift versus knowledge cutoff

Another phenomenon that can cause unfair or inaccurate outputs is **drift**: the decline in an AI model's accuracy in predictions due to changes over time that aren't reflected in the training data. It is commonly caused by **knowledge cutoff**: a model is trained at a specific point in time, so it has no knowledge of events or information after that date.

For instance, a fashion designer might want to track trends in spending before creating a new collection. If they use a model last trained on fashion trends and consumer habits from 2015, it may not produce useful outputs, because consumer preferences in 2015 are very likely different from today's. The model's predictions have drifted from accurate at the time of training to less accurate now, in part because of its knowledge cutoff.

Several other factors can cause drift. Biases in new data can contribute. Changes in how people behave and use technology, or even major events in the world, can make a model less reliable. To keep an AI model working well, regularly monitor its performance and address its knowledge cutoffs using a **human-in-the-loop** approach.

Explore biases, drift, and knowledge cutoffs with Google PAIR Explorables: [What Have Language Models Learned?](https://pair.withgoogle.com/explorables/fill-in-the-blank/) and the other [PAIR AI Explorables](https://pair.withgoogle.com/explorables/).

## Practice Questions

??? question "1. What is data bias?"

    Circumstances in which systemic errors or prejudices lead to unfair or inaccurate information, resulting in biased outputs.

??? question "2. Name the five types of AI harm and one mitigation for each."

    Allocative (double-check AI output against other sources), quality-of-service (add inclusive language to your prompt), representational (challenge assumptions and ask the tool to correct the bias), social system (fact-check and cross-reference output), and interpersonal (consider the effects and use critical thinking about whether AI is right for the task).

??? question "3. What is a deepfake?"

    An AI-generated fake photo or video of a real person saying or doing something they did not. It is an example of social system harm.

??? question "4. What are drift and knowledge cutoff, and how are they related?"

    Drift is the decline in a model's accuracy over time as the world changes in ways not reflected in its training data. Knowledge cutoff is the fact that a model is trained at a specific point in time and knows nothing after that date, which commonly causes drift.

??? question "5. How do you keep an AI model working well?"

    Regularly monitor its performance and address its knowledge cutoffs using a human-in-the-loop approach.
