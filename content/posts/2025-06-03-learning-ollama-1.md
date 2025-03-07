---
title: "Learning Ollama #1"
date: 2025-03-06
---

I recently explored [Ollama](https://ollama.com/) to build a simple AI-powered grocery list categorizer. This was my first time using Ollama, and I wanted to experiment with how it could process and organize text data locally.

## The Goal 🎯

The idea was straightforward:

- Read a list of grocery items from a file.
    
- Use Ollama to categorize the items into groups like Produce, Dairy, Meat, etc.
    
- Sort them alphabetically within each category.
    
- Save the organized list to a new file.
    

## The Implementation 🛠️

I wrote a small Python script that loads a grocery list from `grocery_list.txt`, feeds it into Ollama, and writes the structured output to `outputed_list.txt`. Here’s a breakdown of the steps:

1. **Check if the input file exists** to avoid errors.
    
2. **Read grocery items** from the file.
    
3. **Generate a structured response** using the Ollama API.
    
4. **Save the AI-generated output** to a new file.
    

Here’s a snippet of the core logic:

```
import ollama
import os

MODEL = "llama3.2"
INPUT_FILE = "./data/grocery_list.txt"
OUTPUT_FILE = "./data/outputed_list.txt"

if not os.path.exists(INPUT_FILE):
    print("Error: Input file does not exist.")
    exit(1)

with open(INPUT_FILE, "r") as f:
    items = f.read().strip()

prompt = f"""
You are an assistant that categorizes and sorts grocery items.
Here is a list of grocery items:
{items}

Please:
1. Categorize these items into appropriate categories (e.g., Produce, Dairy, Meat, etc.).
2. Sort the items alphabetically within each category.
3. Present the categorized list in a clear format.
"""

try:
    response = ollama.generate(model=MODEL, prompt=prompt)
    categorized_list = response.get("response", "")
    
    with open(OUTPUT_FILE, "w") as f:
        f.write(categorized_list.strip())
    
    print("Categorization completed successfully!")
except Exception as e:
    print(f"Error: {e}")
```

## Input file

```md
Eggs
Bread
Apples
Chicken breast
Rice
Carrots
Milk 
Cheese
Olive oil
Coffee
```
## Output file
```md
Here is the categorized and sorted list of grocery items:

**Bakery**
� Bread
� Cheese

**Beverages**
� Coffee
� Milk

**Dairy**
� Cheese
� Eggs
� Milk

**Meat**
� Chicken breast

**Oils and Condiments**
� Olive oil

**Produce**
� Apples
� Carrots

Note: I've categorized the items into general categories, but some items (like olive oil) could fit into multiple categories. If you'd like me to re-categorize or add more specific subcategories, please let me know!
```

## The Experience 🚀

Using Ollama for the first time was surprisingly easy! It runs locally, so there’s no need for an external API key, and responses are generated quickly. The model handled the task well, neatly categorizing the list with minimal effort on my part.

## What’s Next? 🔥

Now that I have a working script, I’m thinking of:

- Extending it to handle larger datasets.
    
- Experimenting with different AI models for better categorization.
    
- Building a small web UI to make it user-friendly.
    

This was a fun and simple way to get started with Ollama, and I’m excited to explore more! Have you tried Ollama yet? Let me know what you think. 😊