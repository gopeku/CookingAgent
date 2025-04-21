---
title: AI Cooking Agent
subtitle: "Ask anything about cooking"
---
# &#127859;Cooking Agent with Prompt and GoogleSearch Grounding

**AI Cooking Agent** that provides cooking advice and solves endless questions on what to eat
* Recommend based on the available ingredients
    * either, user typed input
    * or, the image of grocery receipt based on **image understanding**
* Take additional input on cooking time, the number of people to feed and the cuisine style
* Use **one-shot prompt** to summarize cooking ingredients from the receipt image in **structured output** and also the recommended recipes 
* Provide the sources based on **google search grounding**
  
---

## Questions - might be simple for someone but not for everyone
* What should I cook?
* What have I bought from the grocery store?
* Can I have some cooking recipes that are customized (taking advantage of LLM) but also grounded by online resouces like websites and youtube videos (so I don't risk cooking something too creative)?

## Capability
* answer open questions about cooking
* not just take text input but also directly read the image of receipt to tell the ingredients available for cooking
* provide cooking instructions based on the ingredients and associate the recipes with the search results

## Code w/ Gen AI
* `langgraph`: agent framework to enable cyclic chatbot interaction with human
```
from langgraph.graph.message import add_messages
from langgraph.graph import StateGraph, START, END
from langchain_google_genai import ChatGoogleGenerativeAI
from langchain_core.messages.ai import AIMessage
```
* `gemini-2.0-flash`: Google Generative AI model to not just comprehend human language but also other formats like images
```
llm = ChatGoogleGenerativeAI(model="gemini-2.0-flash")
```
* `GenAITool(google_search={})`:  enable google search grounding
```
new_output = llm.invoke([CookingBOT_SYSINT] + messages,
                   tools=[GenAITool(google_search={})])
```
* *prompt engineering*: both system level to define the flow of interactions and *one/few-shot* prompt to output structured format
```
# one shot prompt
prompt = '''
output the items in the image that are related to the food in Markdown table format . See example below
Example:
'|Item|Price|Quantity (Units)|
|rice|30|10 lb|'
'''
```
* `image_prompt`: read image from either local or online and construct the prompt for LLM to comprehend
```
from PIL import Image as IMAGE
def image_prompt(img_url):
    """
    Convert the image and define the prompt for model processing
    Use one-shot prompt to help define the output format
    """
    try:
        img = IMAGE.open(img_url)
    except OSError:
        response = requests.get(img_url)
        if response.status_code == 200:
            # Open the image using PIL from the response content
            img = IMAGE.open(io.BytesIO(response.content))
        else:
            print(f"Failed to retrieve {img_url}. HTTP Status code: {response.status_code}")
```

## Future work
* add capability to directly take human voice as input
* add tools for the chatbot to interact with online shopping service to place order for missing ingredients




