---
title: AI Models and the Training Process
---

# AI Models and the Training Process

Terms like AI tools and AI models can be confusing because they sound similar but refer to different things.

- An **AI tool** is AI-powered software that can automate or assist users with a variety of tasks.
- An **AI model** is a computer program trained on sets of data to recognize patterns and perform specific tasks.

!!! tip
    Some AI tools leverage multiple AI models.

## The process of training AI models

AI designers and engineers develop AI models through a process called **training**. Here is an example of the typical steps, for building a model that predicts rainfall:

1. **Define the problem to be solved.** AI designers and engineers want to predict rain to help people stay dry when commuting to and from work. They start by considering AI's capabilities and limitations before identifying an AI solution.
2. **Collect relevant data to train the model.** They gather historical data of days when it rained and days when it didn't rain over the past 50 years.
3. **Prepare the data for training.** They label important features, such as outdoor temperature, humidity, and air pressure, and then note whether it rained. It is also common to separate the data into two distinct sets: a **training set** and a **validation set** to test with later.
4. **Train the model.** They apply machine learning (ML) programs to the prepared training data. As the ML programs analyze the data, they begin learning how to recognize patterns that indicate the likelihood of rainfall, such as the combination of high temperatures, low air pressure, and high humidity.
5. **Evaluate the model.** They use the validation set they prepared earlier to assess the model's ability to predict rainfall accurately and reliably. Analyzing performance can uncover potential issues, such as insufficient or biased training data. If any issues exist, they may revisit an earlier step to try a different approach. Once the model performs well with its validation set, the process continues.
6. **Deploy the model.** When they are satisfied with the model's performance, they deploy it in an AI tool, helping people in their city stay dry on their way to work.

Model training is an iterative process. AI designers and engineers can repeat each step as many times as necessary and make adjustments until they create the best model possible.

## Practice Questions

??? question "1. What is the difference between an AI tool and an AI model?"

    An AI tool is AI-powered software that automates or assists users with tasks. An AI model is a program trained on data to recognize patterns and perform specific tasks. Some tools use multiple models.

??? question "2. List the six steps of training an AI model."

    Define the problem, collect relevant data, prepare the data (label it and split it into training and validation sets), train the model, evaluate it with the validation set, and deploy it.

??? question "3. Why is a validation set kept separate from the training set?"

    To test how accurately and reliably the model performs on data it wasn't trained on, which can uncover issues like insufficient or biased training data.

??? question "4. Is model training linear?"

    No. It is iterative: designers can repeat each step as many times as needed and revisit earlier steps until they create the best model possible.
