---
title: AI Development Techniques
---

# AI Development Techniques

Resource: [PAIR AI Explorables](https://pair.withgoogle.com/explorables/)

**Artificial intelligence** refers to computer programs that can complete cognitive tasks typically associated with human intelligence.

There are two main techniques used to design AI programs:

1. Rule-based techniques
2. Machine learning techniques

## Rule-based technique

In this technique we specify rules to make **dependent** decisions.

For example, a spam filter using a rule-based technique blocks email that contains specific words.

## Machine learning technique

Analyze and learn from the patterns in data to make **independent** decisions.

For example, a spam filter using this technique might flag potential spam for the recipient to review, preventing automatic blocking. If the recipient marks emails from trusted sources as safe, the spam filter learns and adapts its logic to include similar emails from that sender in the future.

An AI tool can also be a combination of both.

## Approaches to training ML programs

There are three common approaches:

1. Supervised learning
2. Unsupervised learning
3. Reinforcement learning

### Supervised learning

A labeled training set includes data that is labeled or tagged, which provides context and meaning to the data. For instance, an email spam filter trained with supervised learning would use a training set of emails labeled as "spam" or "not spam". Supervised learning is often used when there is a specific output in mind.

### Unsupervised learning

For instance, ML might be used to analyze a dataset of unsorted email messages and find patterns in topics, keywords, or contacts. Unsupervised learning is used to identify patterns in data without a specific output in mind.

### Reinforcement learning

The program learns by getting rewarded for making good choices that lead to the desired results. Reinforcement learning is commonly used by conversational AI tools.

## Practice Questions

??? question "1. What is the difference between rule-based and machine learning techniques?"

    Rule-based techniques follow rules you specify to make dependent decisions (block email with certain words). Machine learning analyzes patterns in data to make independent decisions, and can learn and adapt (a spam filter that learns from what you mark as safe).

??? question "2. Name the three approaches to training ML programs."

    Supervised learning, unsupervised learning, and reinforcement learning.

??? question "3. What is supervised learning, and when is it used?"

    Learning from a labeled training set (for example emails labeled spam or not spam). It is often used when there is a specific output in mind.

??? question "4. What is unsupervised learning?"

    Finding patterns in data without a specific output in mind, for example finding topics or contacts in a dataset of unsorted emails.

??? question "5. What is reinforcement learning?"

    The program learns by being rewarded for good choices that lead to the desired results. It is commonly used by conversational AI tools.
