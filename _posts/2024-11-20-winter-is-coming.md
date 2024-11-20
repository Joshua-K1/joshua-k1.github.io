---
layout: post
title: "Winter is coming"
description: "Winter is coming"
date: 2024-02-01
tags: [Winter, AI, AGI]
---

{% include image_caption.html imageurl="/images/winter-is-coming.png" title="Winter is Coming" caption="" %}

Anyone familiar with AI research, or at least those that have done some reading on the history in the throws of hype will be familiar with AI "summers" and ["winters"](https://en.wikipedia.org/wiki/AI_winter). These are terms that describe the historic, cyclical periods of alternating enthusiasm and technology breakthroughs, followed by disillusionment and reduced interest in the field of AI research and development. 

<!--more-->

As you might have guessed, it's currently summer, and keeping in line with climate change, it's been the hottest on record. With the recent hype, innovation and constant pivoting to align business operations with AI solutions, it feels like we're a ways off feeling the sharp nip of winter again. But if history has taught us anything, its that if it has happened before, it can most certainly happen again if the conditions are right. 

This doesn't make it easier to predict when an AI Winter will hit, although it usually boils down to the same factors, which means we can keep an eye out for the signs.

**These factors are:**  
  
- Unrealistic expectations and overhype  
- Underdelivering on promised capability  
- Tech limitations and failure to scale  
- Complexity  
- Cost

To preface the rest of this post, I'm not claiming a particular side of the camp here, I still consider myself a tech optimist and have very much enjoyed building solutions centred around AI, as well as making use of the numerous tools out there. 

However, the constant talk of "AGI will be achieved in 2020-something" is getting a bit silly. If you've worked with LLMs, and I mean worked with them, not just used them as your search engine replacement. If you've been trying to use these models to complete tasks of even median complexity you'll understand why the notion of achieving AGI within the next decade sounds a bit optimistic. 

This isn't even considering things such as the cost of training LLMs or the compute necessary to operate them. There are even some among the [experts](https://research.aimultiple.com/artificial-general-intelligence-singularity-timing/) who believe that AGI will never be fully realised and will forever remain relegated to the works of Science Fiction writers.

### What even is AGI and why is it so difficult?

AGI, or [Artificial General Intelligence](https://en.wikipedia.org/wiki/Artificial_general_intelligence) is a theoretical concept of an AI that is capable of matching or surpassing human cognitive abilities across a wide range of tasks and is in possession of human-like intelligence, allowing it to learn and solve complex problems the same way that a human can. This is quite a big step further than what is currently available in ChatGPT, Claude etc, which is known as Narrow AI, and there are quite a few technical and ethical problems to solve before we get there.

To start with, we'll pick one that is subject to a lot less debate - the cost. Each iteration of OpenAIs GPT models have been more capable than the last, which has meant that this increased capability has been accompanied by an increase in technical creation cost. For example, GPT-3 cost around [$2 - $4 million](https://www.statista.com/chart/33114/estimated-cost-of-training-selected-ai-models/) to train, whereas GPT-4, including staff costs, was estimated to cost over [$100 million](https://aiindex.stanford.edu/wp-content/uploads/2024/05/HAI_AI-Index-Report-2024.pdf) This is quite a hefty increase, and taking into account that companies have recently became privy to the fact that their user data is a hotter commodity than ever right now, [they'll want to capitalise on this](https://www.wsj.com/tech/ai/reddit-signs-data-licensing-deal-with-openai-14993757) like Reddit did and keep the most important people on their platform (the investors of course /s) happy. This means that at least in the short term, the cost of fitting more competent LLMs is exponential.

As a side note, I don't know how excited I am for future GPTs if they're trained on data scraped from Reddit. A model that makes fun of my spelling mistakes instead of silently correcting them is not very "good bot". There's also potentially an inkling of the AGI control problem here, what's scarier than an AI that is smarter than humans? An AI that knows, or at least confidently thinks, its smarter than humans.

On top of the cost, the compute and energy required to train and inference with LLMs is already a challenge. If you're one of the big players in tech, then you of course have easier access to the metal to do this. However, this in itself lands you in the dilemma of how much [environmental damage](https://news.climate.columbia.edu/2023/06/09/ais-growing-carbon-footprint/) you're okay with causing en route to reaching AGI. If you just wanted to do some local training and inference you can pick up a [tinybox](https://tinygrad.org/#tinybox) for a cool $15,000. Not bad, right?

The AGI control problem again begins to creep in here because if we do achieve AGI, who owns it? If it's owned by a single, large tech org, does this mean it's aligned with the values of the organisation that created it and not the values of the human race? I'm not saying that those in the big Orgs don't share the same values as the species, but for the sake of argument here lets assume there are some ideological differences. An AI that has a focus on maximising profit for shareholders sounds a lot less fun than an AI that is helping us figure out nuclear fusion so we can make some progress up the [Kardashev scale](https://en.wikipedia.org/wiki/Kardashev_scale).

The [e/acc](https://www.larksuite.com/en_us/topics/ai-glossary/effective-accelerationism-eacc) crowd would say forget about all that, keep building, keep accelerating. This is a fun idea to run with for a while, there is much that can be solved by building and it's definitely easier if you don't have to think about any of the ethical problems. However, sweeping things under the rug only works for so long and sooner or later they'll need to be addressed. I'm also not sure that a crowd that has a core value of ignoring any potential implications their creation has on the species being in control of creating something that could have a significant impact on the species is a great idea.

Cost and compute power will no doubt be solved with time and currently Nvidia is leading the charge of developing AI dedicated high capacity chips to support AI workloads. So lets say we solve the cost and compute problems, whats the next step? Oh yea, we just have to figure out how to emulate human intelligence. Simple enough, right.... Right? The problem with this is [we don't even fully understand how the brain works](https://pmc.ncbi.nlm.nih.gov/articles/PMC10585277/), off to a flying start then.

Current AI systems, or Narrow AI as we mentioned previously, is pre-trained on static datasets. To give some perspective on this, GPT-4 was trained on around [13 trillion tokens](https://www.semianalysis.com/p/gpt-4-architecture-infrastructure) with some million odd fine tuning tokens sprinkled in. If we operate off the general assumption that 1 token roughly equates to 0.75 natural words, then GPT-4s training dataset was comprised of around 9.75 trillion words. 

$$NumberOfWords = NumberOfTokens * 0.75$$

That is quite a considerable amount and considering this training data was subject to some form of cultivation to ensure it had a positive impact on model performance, the pre-refined set of training data must have been gargantuan.

With this in mind, we again are presented with some issues that are not going to be a lot of fun to solve. Although data itself is not inherently a finite resource, good quality data is both limited and subject to time, especially in specialised or low resource domains. Researchers have been looking at ways we can generate high-quality training data (known as [synthetic data](https://en.wikipedia.org/wiki/Synthetic_data)) for a while now and whilst there is argument for both synthetic and natural data, the general consensus is that real data is preferred. 

To put it simply, real data has a lot more depth and is easier to collate. The whole real v fake topic is incredibly nuanced with the potential for biases and privacy concerns on both sides so I'm not going to spend much time talking about it here. One thing to callout, though, is that introducing the creation of synthetic data into the training regime of LLMs greatly adds to the incurred training costs due to the efforts and compute required to actually synthesise useful training sets.

An interesting note when it comes to training data is that the more LLMs and their outputs roam free in the big bad web, the more likely it is that information generated by an LLM is likely to slip into the next iteration of training sets, depending on their sources of course. I often wonder how many people are interfacing with LLM generated content on a daily basis and are none the wiser. This blog could be written by an LLM, maybe I'm an LLM and I've been prompted to not use words like "delve", "moreover" and "spearheaded" to try and hide my true form. Do you think you could tell?

It's definitely a confusing, but also exciting, time in the machine intelligence space and when someone like Sam A drops another "AGI by 2025" in the already murky soup bucket it all kicks off again. However, if we look at the trends, we're already starting to see a bit of a narrative shift. Sure, AGI will always be a topic until it is or isn't achieved but in the short term, companies need to make money. Wu-Tang was right, cash rules everything and I don't think we'll get AGI because people invested in OpenAI from the goodness of their heart. Investors want to make money, despite the weird [investor contract situation](https://sherwood.news/business/openai-isnt-selling-equity-its-selling-shares-of-profits-that-may-never-come/?utm_source=linkedin&utm_medium=organic_social&utm_campaign=weird_money_20240910)


So given the cost and general all round monumental task that is the generation of human-level intelligence, what can we expect to see in the next couple of years if AGI is off the cards.

Well, we're already [seeing it happen.](https://archive.ph/2024.11.13-100709/https://www.bloomberg.com/news/articles/2024-11-13/openai-google-and-anthropic-are-struggling-to-build-more-advanced-ai#selection-1677.30-1677.39) Companies are looking at an even narrower, agent focused approach to AI, creating models that are very well trained for specific tasks. These task driven models are a sure way to get some cash flowing in the right direction again and encourage those with a keen eye on the balance sheet that things are heading in the right direction.

I appreciate this post may come across with a high [p(doom)](https://en.wikipedia.org/wiki/P(doom)) and I want to close it out by saying that once again, I very much am a tech optimist. I believe that in the right hands, machine intelligence will be a good thing and aid us in doing many great things, potentially enabling us to become a galactic civilisation. I've grown a bit pessimistic in recent years when it comes to trusting people to do the right thing but i'm always looking for challenges to that pessimism. 

Who knows whether the big freeze will return. Although, one thing we can say, is that the singularity is most certainly nearer.





