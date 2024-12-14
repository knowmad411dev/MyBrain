---
tags:
- agents
- web
url: https://github.com/InternLM/MindSearch
---

## **MindSearch

“Mimicking human mind for deeper AI search”

Google’s search engine can give you the best search results in the form of web-page links. But not direct answers to your queries. If you combine the search engine with a powerful modern LLM like GPT4o, you can get very accurate responses to your complex queries.

However even the Search Engine + [[LLM]] combo has limitations.

1) The web search results include too much information and a lot of noise. This can easily exceed the context length of LLM.

2) Search Engine cannot efficiently do the search if the query is complex

The process of finding information is very different in humans. We do not try to find the answer to our complex question directly. We modularize the question to smaller, manageable chunks.

Imagine you want to buy a car. You will not be directly trying to answer your question of “I wish to buy a car under Rs. 12 lakhs budget for the purpose of daily use. I want XYZ features, mileage and CC”.

Rather you look at different parts of this question. Your brand preference, feature list, resale value, number of seats, expected years/kms of total use, maximum budget etc. Then you find a list of cars. Some of them will fit some of your requirements. You will weight your options and then take a call. It is a fairly iterative process.

How do you incorporate this complex, iterative decision making into AI assisted internet search?

This paper titled “MindSearch”, published on arXiv 3 has a fascinating idea: Modularize the search query and represent this as a [[Graphs]] Neural Network with nodes and edges. Deploy LLM agents for planning the web search via Search Engine API. Conduct parallel search queries to answer different parts of the query. This is called fine-grain search.

The Graph will be dynamic. Based on the findings from the initial web search by LLM agent, the nodes and edges are updated. The number of nodes in the Graph will depend on the complexity of the search query.

Based on the research conducted by the authors of the paper, MindSearch hands down beats the existing solutions for AI assisted search on open ended and close ended questions. Their GitHub repo already has 3.7k stars: https://github.com/InternLM/MindSearch

Here is the link to the paper: https://arxiv.org/abs/2407.20183

For LLM search to replace traditional Google search there is a long way to go. The commercial use of MindSearch will boil down to cost, accuracy, rate of hallucination, speed and the actual utility of the responses from the LLM agent.

[[LLM]]   [[AI Agents]]
