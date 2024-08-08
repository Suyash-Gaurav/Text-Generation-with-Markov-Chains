# Text-Generation-with-Markov-Chains




```markdown
# Markov Chain Text Generator

This project implements a simple text generation algorithm using Markov chains. The algorithm creates a statistical model that predicts the probability of a word based on the preceding word(s), and uses this model to generate text that mimics the style of the input corpus.

## Table of Contents

- [Introduction](#introduction)
- [Requirements](#requirements)
- [Usage](#usage)
- [Code Explanation](#code-explanation)
- [License](#license)

## Introduction

The Markov Chain Text Generator is a Python script that builds a Markov chain model from a given text corpus and generates new text based on this model. This project serves as an example of how Markov chains can be used for text generation and can be a starting point for more advanced text generation projects.

## Requirements

- Python 3.x
- No additional libraries are required beyond the Python standard library.

## Usage

1. Clone this repository or download the script file.

2. Prepare a text corpus that you want to use for training the Markov chain model. You can replace the sample corpus in the script with your own text.

3. Run the script:
    ```bash
    python markov_chain_text_generator.py
    ```

4. The script will output generated text based on the input corpus.

## Code Explanation

The code consists of several key sections:

### Importing Necessary Libraries

```python
import re
import random
from collections import defaultdict
```

- `re`: Provides support for regular expressions.
- `random`: Implements pseudo-random number generators.
- `defaultdict` from `collections`: Extends the built-in `dict` class to provide default values for non-existent keys.

### Sample Corpus

A sample text used to train the Markov chain model. Replace this with your own text.

```python
corpus = """
In a village of La Mancha, the name of which I have no desire to call to mind, there lived not long since one of those gentlemen that keep a lance in the lance-rack, an old buckler, a lean hack, and a greyhound for coursing.
An olla of rather more beef than mutton, a salad on most nights, scraps on Saturdays, lentils on Fridays, and a pigeon or so extra on Sundays, made away with three-quarters of his income.
"""
```

### Tokenize the Text

Tokenizes the text into words.

```python
def tokenize(text):
    text = text.lower()
    words = re.findall(r'\b\w+\b', text)
    return words

tokens = tokenize(corpus)
```

### Build the Markov Chain Model

Constructs the Markov chain model.

```python
def build_markov_chain(tokens, n=1):
    markov_chain = defaultdict(list)
    for i in range(len(tokens) - n):
        key = tuple(tokens[i:i+n])
        next_word = tokens[i+n]
        markov_chain[key].append(next_word)
    return markov_chain

markov_chain = build_markov_chain(tokens, n=1)
```

### Generate Text

Generates text based on the Markov chain model.

```python
def generate_text(markov_chain, length=50, n=1):
    start = random.choice(list(markov_chain.keys()))
    current_words = list(start)
    text = current_words[:]

    for _ in range(length - n):
        key = tuple(current_words[-n:])
        next_word = random.choice(markov_chain[key])
        text.append(next_word)
        current_words.append(next_word)

    return ' '.join(text)

generated_text = generate_text(markov_chain, length=50, n=1)
print(generated_text)
```

### Full Implementation

Combining all the sections:

```python
import re
import random
from collections import defaultdict

# Sample corpus
corpus = """
In a village of La Mancha, the name of which I have no desire to call to mind, there lived not long since one of those gentlemen that keep a lance in the lance-rack, an old buckler, a lean hack, and a greyhound for coursing.
An olla of rather more beef than mutton, a salad on most nights, scraps on Saturdays, lentils on Fridays, and a pigeon or so extra on Sundays, made away with three-quarters of his income.
"""

# Tokenize the text
def tokenize(text):
    text = text.lower()
    words = re.findall(r'\b\w+\b', text)
    return words

tokens = tokenize(corpus)

# Build the Markov chain model
def build_markov_chain(tokens, n=1):
    markov_chain = defaultdict(list)
    for i in range(len(tokens) - n):
        key = tuple(tokens[i:i+n])
        next_word = tokens[i+n]
        markov_chain[key].append(next_word)
    return markov_chain

markov_chain = build_markov_chain(tokens, n=1)

# Generate text
def generate_text(markov_chain, length=50, n=1):
    start = random.choice(list(markov_chain.keys()))
    current_words = list(start)
    text = current_words[:]

    for _ in range(length - n):
        key = tuple(current_words[-n:])
        next_word = random.choice(markov_chain[key])
        text.append(next_word)
        current_words.append(next_word)

    return ' '.join(text)

# Generate and print the text
generated_text = generate_text(markov_chain, length=50, n=1)
print(generated_text)
```

## License

This project is licensed under the MIT License. See the [LICENSE](LICENSE) file for details.
```

This `README.md` provides an overview of the project, instructions for usage, and explanations for each section of the code. It is intended to help users understand and run the Markov Chain Text Generator script.
