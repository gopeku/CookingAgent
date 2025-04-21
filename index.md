---
title: AI Cooking Agent
---
# &#127859;Cooking Agent with Prompt and GoogleSearch Grounding
---

**AI Cooking Agent** that provides cooking advice and solves endless questions on what to eat
- Recommend based on the available ingredients
    - either, user typed input
    - or, the image of grocery receipt (**image understanding**)
- Take additional input on cooking time, the number of people to feed and the cuisine style
- Use **one-shot prompt** to summarize cooking ingredients from the receipt image in **structured output** and also the recommended recipes 
- Provide the sources based on **google search grounding**
---

## Questions - might be simple for someone but not for everyone
- What should I cook?
- What have I bought from the grocery store?
- Can I have some cooking recipes that are customized (taking advantage of LLM) but also grounded by online resouces like websites and youtube videos (so I don't risk cook something too creative)?

## Capability
- answer open questions about cooking
- not just take text input but also directly read the image of receipt to tell the ingredients available for cooking
- provide cooking instructions based on the ingredients and associate the recipes with the search results

## Gen AI Support
- `langgraph`: agent framework to enable cyclic chatbot interaction with human
- `gemini-2.0-flash`: Google Generative AI model to not just comprehend human language but also other formats like images
- `GenAITool(google_search={})`:  enable google search grounding
- *prompt engineering*: both system level to define the flow of interactions and *one/few-shot* prompt to output structured format

## Future work
- add capability to directly take human voice as input
- add tools for the chatbot to interact with online shopping service to place order for missing ingredients




