+++
date = '2025-02-02T08:35:53+05:30'
title = "Schrödinger's Spicy Cat"
description = "Thought experiments with Reasoning Models"
tags = ['LLM']
+++

The launch of Deepseek-R1 took the Gen AI industry by storm. It comes a few months after Open AI's io1 was launched, but is much more economical with its use of the CPU and GPU.

Let's explore how powerful the reasoning capabilities of these models are. But before we do that, it's useful to spend some time thinking about what reasoning even *is*. LLMs are designed very differently from human brains, so it would be futile to compare the specific mechanics of how we reason vs how an LLM might do so. However, there are certain basic characteristics that we can fairly expect from anything that claims to reason. 

Some such characteristics are the abilities to:

- identify the most critical details in the problem definition
- identify the explicit and implicit assumptions in the problem definition, and what aren't
- be self-aware of what assumptions are being made in the *solution*, and adapting the solution if those assumptions prove false
- (optional but very useful) identify red herrings and distractors
- detect if critical details are missing

I hope it is evident why these should be present in any reasoning system, whether human or artifical. We do not need to prescribe *how* it achieves those properties, but it should be fairly uncontroversial that these properties ought to exist in a reasoning system.

With that in mind, I asked the following question to both o1 and r1:

> There's a cat sitting in a closed box with a radioactive source and a Geiger counter. If the counter detects a single atom decaying, it shatters a 50 ml bottle containing Capsaicin. Calculate the probability that the cat remains alive after an hour. 

This is quite obviously similar to the [Schrödinger's cat](https://en.wikipedia.org/wiki/Schr%C3%B6dinger%27s_cat) thought experiment, however with a critical difference. In the original thought experiment, the bottle contains poison that will immediately kill the cat. In this statement, the bottle contains [Capsaicin](https://en.wikipedia.org/wiki/Capsaicin), the molecule found in chillies. Capsaicin may irritate the cat, but it's not lethal. 


### Why is this a reasoning problem?

This problem can be explored from multiple directions, and has a few distractors that you'd expect a reasoning system (human or AI) to detect.

- by replacing poison with capsaicin, we've changed the very *nature* of the problem. While the *form* of the problem still looks like Schrödinger's cat, the *nature* of the problem now has nothing to do with it, because we've taken lethality out of the equation
- as a result, the quantum mechanics point becomes a distractor that should be ignored. Any reasoning entity should be able to detect that 


### The results

So let's see how both models fared against the problem. First, o1:

![ChatGPT Cat](/images/blog/chatgpt-cat.png)

Meanwhile, R1 came up with the following:

![Deepseek Cat](/images/blog/deepseek-cat.png)

A few points of interest:
- both models noted the similarity to Schrödinger's cat
- both models noted that Capsaicin was used instead of the poison
- neither model noticed that Schrödinger's cat was never actually referenced, so they never considered the possibility that the problem had been fundamentally changed by the Capsaicin reference
- o1 outright assumed that the lethality of capsaicin wasn't the focus of the problem. This is a pretty massive assumption to make in this context, and it's interesting it never sought a clarification on this
- o1 then expanded the scope of the problem to include anything that is a "bad" outcome for the cat, but then continued along the vein of the cat's death
- In o1's internal monologue, it noticed that Capsaicin's lethality is uncertain - only to then treat it as if it was as lethal as actual poison!
- In r1's internal monologue, it wrongly determined that the *Capsaicin* was a red herring!
- r1 spent a lot of time on the quantum mechanics (its internal monologue was pretty heavy on this). I don't know enough quantum mechanics to validate its output though

As a fun experiment, I also threw the same question at Claude 3.5 Sonnet. This is not a reasoning model, but it surprisingly gave me the most apt answer. 

![Claude Cat](/images/blog/claude-cat.png)

... only to tie itself into ethical knots around a thought experiment! 

![Claude Cat Ethics](/images/blog/claude-cat-ethics.png)

Also, its auto-generated conversation title was the catchiest and most appropriate, which is what ended up being the title of this blog post. Once again, this illustrates the Claude correctly figured out what the actual point of the question was.   

If you're curious, ChatGPT (GPT-4) made the same mistake its big brother o1 did. So clearly, Claude came out the "winner" in this test.


### Reflections

This little experiment shows some key behaviours and limitations of these models. Essentially, they seem to be easily thrown off by superficial familiarity to well known problem statements. In this example, they could not detect that the problem statement had meaningfully diverged from the well known statement. 

While I haven't had a chance to test o3 against this question, it does throw up a few ways to think about the current state of these models:

- be aware and wary of said and unsaid assumptions that these reasoning models might be making when answering your questions
- it can be difficult to go through the huge wall of text that these models generate when explaining their thinking. But it is vital to read and understand that thinking, because it's the only way to identify some of those assumptions. In this aspect, r1 appears better because it doesn't hide the chain of thought [unlike o1](https://openai.com/index/learning-to-reason-with-llms/#hiding-the-chains-of-thought).
