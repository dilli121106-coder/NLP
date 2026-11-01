# 24AIPW501 - Natural Language Processing Theory with Laboratory

**Sri Sairam Engineering College**  
An Autonomous Institution | Affiliated to Anna University and approved by AICTE, New Delhi  
Accredited by NBA and NAAC A+ | BIS/EOMS ISO 21001:2018 certified and NIRF-ranked institution  
Sri Leo Nagar, West Tambaram, Chennai - 600 044  
Website: https://www.sairam.edu.in  
Record Note Book  
Name: ______________________________  
Register Number: ______________________________  
Department of Artificial Intelligence and Data Science  
Batch: 2024-2028  
III Year / V Semester  
Academic Year: 2026-2027

---

## Bonafide Certificate

**Department of Artificial Intelligence and Data Science**

**Bonafide Certificate**

Register Number: ______________________________

This is to certify that this is the Bonafide record of the work done by **________________________________**, of B.Tech Artificial Intelligence and Data Science in the **24AIPW501 - Natural Language Processing Theory with Laboratory** during the academic year **2026-2027**.

- Station: Chennai - 600 044
- Date: ______________________________
- Staff In-Charge: ______________________________
- Head of the Department: ______________________________

Submitted for End Semester Practical Examination held on __________________ at Sri Sairam Engineering College, Chennai - 600 044.

Internal Examiner: ______________________________

---

## Index

| S. No. | Date | Experiment | Page No. | Marks | Signature | PDF page range (navigation) |
|---:|---|---|---|---|---|:---:|
| 1 |  | Text Processing - Sentence Tokenization, Word Tokenization, Stop Words Removal, Stemming and Lemmatization |  |  |  | 4-10 |
| 2 |  | Term Frequency, Inverse Term Frequency (the experiment body uses Inverse Document Frequency) |  |  |  | 11-16 |
| 3 |  | Language Models - Unigram, Bigram and Trigram |  |  |  | 17-21 |
| 4 |  | CKY Parsing for Sentence Analysis |  |  |  | 22-25 |
| 5 |  | Semantic Relationship Using Word2Vec Models - CBOW, Skip-gram |  |  |  | 26-31 |
| 6 |  | Language Translation Using SMT |  |  |  | 32-36 |
| 7 |  | Language Translation Using NMT/NLP Libraries |  |  |  | 37-39 |
| 8 |  | Next Word Prediction Using LSTM |  |  |  | 40-45 |
| 9 |  | Spam Filtering System Using NLP Techniques |  |  |  | 46-51 |
| 10 |  | Implementation of Chatbot Using NLP Techniques |  |  |  | 52-58 |

> **Source-layout note:** The manual's index and individual page headers contain a few naming/numbering inconsistencies. The sequence above follows the index. The original experiment headings and wording are retained within the relevant sections below. In Experiment 6, the printed output says there are 12 sentence pairs, while the visible source list contains 11 pairs; both are preserved as printed. Page 31 contains the original side-by-side PCA plots for the Word2Vec experiment; this single-file Markdown edition records the figure's purpose and surrounding results in text.

---

# Experiment 1 - Text Processing: Sentence Tokenization, Word Tokenization, Stop Words Removal, Stemming and Lemmatization

## Aim

To develop a Python program using the NLTK library to perform text preprocessing on a given text corpus by applying regular expressions for extracting words, numbers, email addresses, and special characters, followed by sentence tokenization, word tokenization, Part-of-Speech (POS) tagging, stop-word removal, stemming, and lemmatization.

## Theory

Natural Language Processing (NLP) enables computers to process, analyze, and understand human language. Text preprocessing is an important initial step that converts raw text into a structured form suitable for further NLP tasks.

### Regular Expression

A Regular Expression (RegEx) is a sequence of characters used to search, match, validate, and extract specific patterns from text. Python provides the built-in `re` module for regular-expression operations.

**Common Regular Expression symbols**

| Symbol | Description | Example |
|---|---|---|
| `.` | Matches any character except newline by default | `a.c` |
| `^` | Matches the beginning of a string | `^Hello` |
| `$` | Matches the end of a string | `world$` |
| `*` | Matches zero or more repetitions | `ab*c` |
| `+` | Matches one or more repetitions | `ab+c` |
| `?` | Matches zero or one occurrence | `colou?r` |
| `\d` | Matches a digit | `\d+` |
| `\D` | Matches a non-digit | `\D+` |
| `\w` | Matches a word character | `\w+` |
| `\W` | Matches a non-word character | `\W+` |
| `\s` | Matches whitespace | `\s+` |
| `\S` | Matches non-whitespace | `\S+` |
| `[A-Z]` | Matches uppercase letters | `[A-Z]+` |
| `[a-z]` | Matches lowercase letters | `[a-z]+` |
| `[0-9]` | Matches digits | `[0-9]+` |
| `\b` | Matches a word boundary | `\bcat\b` |
| `{n}` | Matches exactly n repetitions | `\d{4}` |
| `{n,m}` | Matches between n and m repetitions | `\d{2,4}` |
| `()` | Groups patterns | `(ab)+` |
| `|` | Alternation between patterns | `cat|dog` |

### Sentence Tokenization

Sentence tokenization divides a paragraph into individual sentences. The NLTK function `sent_tokenize()` identifies sentence boundaries.

### Word Tokenization

Word tokenization divides text into individual words and punctuation marks using `word_tokenize()`.

### Part-of-Speech Tagging

Part-of-Speech (POS) tagging assigns grammatical categories, such as nouns, verbs, adjectives, and adverbs, to words. The `nltk.pos_tag()` function performs this operation.

### Stop-Word Removal

Stop-word removal eliminates common words such as *the*, *is*, *are*, and *and* using NLTK's English stop-word list. These words may be less informative for certain NLP tasks.

### Stemming

Stemming reduces words to root-like forms by removing suffixes according to predefined rules. The `PorterStemmer()` class performs stemming.

Example: `playing` -> `play`  
A stem is not always a valid dictionary word.

### Lemmatization

Lemmatization converts words into their dictionary base forms, called lemmas, using the `WordNetLemmatizer()` class.

Example: `cats` -> `cat`  
In this program, the lemmatizer uses noun-based lemmatization by default, so some verbs such as *running* and *playing* remain unchanged.

## Algorithm

1. Start the program.
2. Import the `re` module and required NLTK modules.
3. Download the required NLTK datasets.
4. Read the text corpus from the user.
5. Apply regular expressions to extract alphabetic words, numbers, and email addresses.
6. Perform sentence tokenization using `sent_tokenize()`.
7. Perform word tokenization using `word_tokenize()`.
8. Select alphabetic tokens and perform POS tagging using `nltk.pos_tag()`.
9. Remove English stop words and non-alphabetic tokens.
10. Apply Porter stemming to the filtered words.
11. Apply WordNet lemmatization to the filtered words.
12. Display the results of every preprocessing operation.
13. Stop the program.

## Setup

**Software requirements**

- Python 3.x
- Python IDLE
- NLTK library

**Installation**

```bash
pip install nltk
```

**Required NLTK datasets**

- `punkt` - sentence tokenization.
- `punkt_tab` - supporting tokenizer data.
- `stopwords` - English stop-word list.
- `wordnet` - lexical database for lemmatization.
- `omw-1.4` - additional WordNet language data.
- `averaged_perceptron_tagger_eng` - English POS tagging.

## Program

```python
import re
import nltk
from nltk.tokenize import sent_tokenize, word_tokenize
from nltk.corpus import stopwords
from nltk.stem import PorterStemmer, WordNetLemmatizer

# Step 1: Download the required NLTK data
nltk.download('punkt')
nltk.download('punkt_tab')
nltk.download('stopwords')
nltk.download('wordnet')
nltk.download('omw-1.4')
nltk.download('averaged_perceptron_tagger_eng')

# Step 2: Get text input from the user
print("===== TEXT PREPROCESSING USING NLTK =====")
text = input("\nEnter the text corpus: ")

# Step 3: Regular Expression
print("\n===== Regular Expression =====")

email_pattern = r'\b[\w.+-]+@[\w.-]+\.[A-Za-z]{2,}\b'
number_pattern = r'\b\d+(?:\.\d+)?\b'
word_pattern = r'\b[A-Za-z]+\b'
special_pattern = r'[^A-Za-z0-9\s]'

emails = re.findall(email_pattern, text)
numbers = re.findall(number_pattern, text)
alpha_words = re.findall(word_pattern, text)
special_chars = re.findall(special_pattern, text)

print("Alphabetic Words:", alpha_words)
print("Numbers:", numbers)
print("Email Addresses:", emails)
print("Special Characters:", special_chars)

# Step 4: Sentence Tokenization
sentences = sent_tokenize(text)

print("\n===== Sentence Tokenization =====")
for i, sentence in enumerate(sentences, start=1):
    print("Sentence", i, ":", sentence)

# Step 5: Word Tokenization
words = word_tokenize(text)

print("\n===== Word Tokenization =====")
print(words)

# Step 6: POS Tagging
pos_words = [word for word in words if word.isalpha()]
pos_tags = nltk.pos_tag(pos_words)

print("\n===== POS Tagging =====")
for word, tag in pos_tags:
    print(word, "->", tag)

# Step 7: Stop-Word Removal
stop_words = set(stopwords.words('english'))

filtered_words = [
    word for word in words
    if word.isalpha() and word.lower() not in stop_words
]

print("\n===== Stop Word Removal =====")
print(filtered_words)

# Step 8: Stemming
stemmer = PorterStemmer()
stemmed_words = [
    stemmer.stem(word) for word in filtered_words
]

print("\n===== Stemming =====")
for original, stemmed in zip(filtered_words, stemmed_words):
    print(original, "->", stemmed)

# Step 9: Lemmatization
lemmatizer = WordNetLemmatizer()

lemmatized_words = [
    lemmatizer.lemmatize(word) for word in filtered_words
]

print("\n===== Lemmatization =====")
for original, lemma in zip(filtered_words, lemmatized_words):
    print(original, "->", lemma)

# Step 10: Final Results
print("\n===== Final Results =====")
print("Stemmed Words:", stemmed_words)
print("Lemmatized Words:", lemmatized_words)

print("\nText preprocessing completed successfully.")
```

## Input

```text
Hello NLP123! My email is student123@gmail.com and my marks are 95.
```

## Output

```text
===== TEXT PREPROCESSING USING NLTK =====

===== Regular Expression =====
Alphabetic Words: ['Hello', 'NLP', 'My', 'email', 'is', 'and', 'my', 'marks', 'are']
Numbers: ['123', '95']
Email Addresses: ['student123@gmail.com']
Special Characters: ['!', '@', '.']

===== Sentence Tokenization =====
Sentence 1 : Hello NLP123!
Sentence 2 : My email is student123@gmail.com and my marks are 95.

===== Word Tokenization =====
['Hello', 'NLP123', '!', 'My', 'email', 'is', 'student123', '@', 'gmail.com', 'and', 'my', 'marks', 'are', '95', '.']

===== POS Tagging =====
Hello -> NNP
NLP -> NNP
My -> PRP$
email -> NN
is -> VBZ
and -> CC
my -> PRP$
marks -> NNS
are -> VBP

===== Stop Word Removal =====
['Hello', 'NLP', 'marks', '95']

===== Stemming =====
Hello -> hello
NLP -> nlp
marks -> mark

===== Lemmatization =====
Hello -> Hello
NLP -> NLP
marks -> mark

===== Final Results =====
Stemmed Words: ['hello', 'nlp', 'mark']
Lemmatized Words: ['Hello', 'NLP', 'mark']

Text preprocessing completed successfully.
```

## Result

Thus, the Python program for text preprocessing using Regular Expressions and NLTK was developed and executed. Alphabetic words, numbers, email addresses, and special characters were extracted, and sentence tokenization, word tokenization, POS tagging, stop-word removal, stemming, and lemmatization were performed to analyze the input text successfully.

---

# Experiment 2 - Term Frequency, Inverse Document Frequency (TF-IDF)

## Aim

To develop a Python program to calculate Term Frequency (TF), Inverse Document Frequency (IDF), and TF-IDF values separately for a given set of documents, and analyze the importance of words using TF-IDF scores and cosine similarity.

## Theory

TF-IDF stands for Term Frequency-Inverse Document Frequency. It is a technique used in Natural Language Processing (NLP) to identify important words in a document compared with a collection of documents. It is commonly used in search engines, document classification, and text analysis.

### Term Frequency (TF)

TF measures how often a word appears in a document.

`TF(t, d) = (Number of occurrences of t in d) / (Total words in document d)`

Example: In D1, “the cat sat on the mat”, the word *cat* occurs once in six words.

`TF(cat, D1) = 1/6 = 0.167`

### Inverse Document Frequency (IDF)

IDF measures how rare a word is across all documents.

`IDF(t) = log10(N / DF(t))`

Where:

- `N` = Total number of documents.
- `DF(t)` = Number of documents containing the word.
- `log10` = Logarithm to base 10.

Example: If *mat* appears in only one of four documents:

`IDF(mat) = log10(4/1) = 0.602`

### TF-IDF

TF-IDF combines TF and IDF to measure a word’s importance in a document.

`TF-IDF(t, d) = TF(t, d) x IDF(t)`

Example:

`TF-IDF(mat, D1) = 0.167 x 0.602 = 0.100`

A higher TF-IDF value generally indicates a more useful word for distinguishing a document from the others.

### Cosine Similarity

Cosine similarity compares two documents using their TF-IDF vectors A and B:

`cos(A, B) = (A . B) / (||A|| ||B||)`

Its value lies between 0 and 1 for TF-IDF vectors, and a higher value means the documents are more similar.

## Algorithm

1. Define the set of documents.
2. Convert each document to lowercase and split it into words using a regular expression.
3. Build the sorted list of unique terms from all documents.
4. Calculate TF for every term in every document by dividing its count by the document length.
5. Count the number of documents containing each term (DF) and calculate `IDF = log10(N / DF)`.
6. Calculate TF-IDF by multiplying TF and IDF.
7. Display the TF, IDF and TF-IDF tables.
8. Find the top three keywords of each document and list the common and unique terms.
9. Calculate the cosine similarity between every pair of documents.

## Setup

**Software requirements:** Python 3.x.

**Modules and functions used**

| Library | Purpose |
|---|---|
| `re` | Splits text into words and removes punctuation |
| `math` | Calculates logarithms and square roots |
| `collections.Counter` | Counts word occurrences and document frequency |

All three are part of the Python standard library; no external installation is required.

## Program

```python
import re
import math
from collections import Counter

# 1. Documents
docs = {
    "D1": "the cat sat on the mat",
    "D2": "the dog sat on the log",
    "D3": "the cat chased the dog",
    "D4": "dogs and cats are pets"
}

words = {d: re.findall(r"\b\w+\b", s.lower())
         for d, s in docs.items()}
N = len(docs)
terms = sorted(set(w for t in words.values() for w in t))

# 2. TF and DF
tf, df = {}, Counter()

for d, tokens in words.items():
    count = Counter(tokens)
    tf[d] = {w: count[w] / len(tokens) for w in terms}
    df.update(set(tokens))

# 3. IDF and TF-IDF
idf = {w: math.log10(N / df[w]) for w in terms}
score = {d: {w: tf[d][w] * idf[w] for w in terms}
         for d in docs}

def heading(title):
    print("\n" + "=" * 60)
    print(title)
    print("=" * 60)

def table(data):
    print(f"{'Term':<12}" + "".join(f"{d:>9}" for d in docs))
    for w, values in data.items():
        print(f"{w:<12}" + "".join(f"{values[d]:>9.3f}" for d in docs))

# 4. Display TF
heading("TERM FREQUENCY (TF)")
table({w: {d: tf[d][w] for d in docs} for w in terms})

# 5. Display IDF
heading("INVERSE DOCUMENT FREQUENCY (IDF)")
print(f"{'Term':<12}{'DF':>8}{'IDF':>10}")
for w in terms:
    print(f"{w:<12}{df[w]:>8}{idf[w]:>10.3f}")

# 6. Display TF-IDF
heading("TF-IDF SCORES")
table({w: {d: score[d][w] for d in docs} for w in terms})

# 7. Analysis
heading("ANALYSIS")
for d in docs:
    top = sorted(terms, key=lambda w: -score[d][w])
    top = [w for w in top if score[d][w] > 0][:3]
    print(f"{d} top keywords: {', '.join(top)}")

print("Common terms:", [w for w in terms if df[w] == N] or "None")
print("Unique terms:", [w for w in terms if df[w] == 1])

# 8. Cosine similarity between documents
def cosine(a, b):
    dot = sum(score[a][w] * score[b][w] for w in terms)
    na = math.sqrt(sum(v * v for v in score[a].values()))
    nb = math.sqrt(sum(v * v for v in score[b].values()))
    return dot / (na * nb) if na and nb else 0.0

heading("COSINE SIMILARITY")
names = list(docs)
for i, a in enumerate(names):
    for b in names[i + 1:]:
        print(f"{a} - {b}: {cosine(a, b):.3f}")
```

## Output

### Term Frequency (TF)

| Term | D1 | D2 | D3 | D4 |
|---|---:|---:|---:|---:|
| and | 0.000 | 0.000 | 0.000 | 0.200 |
| are | 0.000 | 0.000 | 0.000 | 0.200 |
| cat | 0.167 | 0.000 | 0.200 | 0.000 |
| cats | 0.000 | 0.000 | 0.000 | 0.200 |
| chased | 0.000 | 0.000 | 0.200 | 0.000 |
| dog | 0.000 | 0.167 | 0.200 | 0.000 |
| dogs | 0.000 | 0.000 | 0.000 | 0.200 |
| log | 0.000 | 0.167 | 0.000 | 0.000 |
| mat | 0.167 | 0.000 | 0.000 | 0.000 |
| on | 0.167 | 0.167 | 0.000 | 0.000 |
| pets | 0.000 | 0.000 | 0.000 | 0.200 |
| sat | 0.167 | 0.167 | 0.000 | 0.000 |
| the | 0.333 | 0.333 | 0.400 | 0.000 |

### Inverse Document Frequency (IDF)

| Term | DF | IDF |
|---|---:|---:|
| and | 1 | 0.602 |
| are | 1 | 0.602 |
| cat | 2 | 0.301 |
| cats | 1 | 0.602 |
| chased | 1 | 0.602 |
| dog | 2 | 0.301 |
| dogs | 1 | 0.602 |
| log | 1 | 0.602 |
| mat | 1 | 0.602 |
| on | 2 | 0.301 |
| pets | 1 | 0.602 |
| sat | 2 | 0.301 |
| the | 3 | 0.125 |

### TF-IDF Scores

| Term | D1 | D2 | D3 | D4 |
|---|---:|---:|---:|---:|
| and | 0.000 | 0.000 | 0.000 | 0.120 |
| are | 0.000 | 0.000 | 0.000 | 0.120 |
| cat | 0.050 | 0.000 | 0.060 | 0.000 |
| cats | 0.000 | 0.000 | 0.000 | 0.120 |
| chased | 0.000 | 0.000 | 0.120 | 0.000 |
| dog | 0.000 | 0.050 | 0.060 | 0.000 |
| dogs | 0.000 | 0.000 | 0.000 | 0.120 |
| log | 0.000 | 0.100 | 0.000 | 0.000 |
| mat | 0.100 | 0.000 | 0.000 | 0.000 |
| on | 0.050 | 0.050 | 0.000 | 0.000 |
| pets | 0.000 | 0.000 | 0.000 | 0.120 |
| sat | 0.050 | 0.050 | 0.000 | 0.000 |
| the | 0.042 | 0.042 | 0.050 | 0.000 |

### Analysis

```text
D1 top keywords: mat, cat, on
D2 top keywords: log, dog, on
D3 top keywords: chased, cat, dog
D4 top keywords: and, are, cats
Common terms: None
Unique terms: ['and', 'are', 'cats', 'chased', 'dogs', 'log', 'mat', 'pets']
```

### Cosine Similarity

| Document pair | Similarity |
|---|---:|
| D1 - D2 | 0.350 |
| D1 - D3 | 0.236 |
| D1 - D4 | 0.000 |
| D2 - D3 | 0.236 |
| D2 - D4 | 0.000 |
| D3 - D4 | 0.000 |

## Result

Thus, the TF-IDF technique was successfully implemented in Python. Term frequency, inverse document frequency, TF-IDF scores, important keywords, and cosine similarity between documents were calculated and analyzed.

---

# Experiment 3 - Language Models: Unigram, Bigram and Trigram

## Aim

To develop a Python program to extract and display all unigrams, bigrams, and trigrams from a given text corpus and compute the probability and perplexity of a test sentence using unigram, bigram, and trigram language models.

## Theory

An n-gram is a sequence of n consecutive words in a text corpus. A unigram contains one word, a bigram contains two consecutive words, and a trigram contains three consecutive words. N-gram language models estimate word probabilities using frequencies in a training corpus.

### Unigram

A unigram is a single word. Its probability is:

`P(w) = C(w) / T`

where `C(w)` is the count of the word and `T` is the total number of words in the corpus.

### Bigram

A bigram is a sequence of two consecutive words. Its conditional probability is:

`P(w2 | w1) = C(w1, w2) / C(w1)`

where `C(w1, w2)` is the count of the word pair and `C(w1)` is the count of the first word.

### Trigram

A trigram is a sequence of three consecutive words. Its conditional probability is:

`P(w3 | w1, w2) = C(w1, w2, w3) / C(w1, w2)`

where `C(w1, w2, w3)` is the count of the three-word sequence and `C(w1, w2)` is the count of the first two words.

### Sentence Probability

The sentence probability is the product of the probabilities evaluated for the sentence:

`P(W) = product(Pi), i = 1 to N`

### Perplexity

Perplexity measures how well a language model predicts a sequence. Lower perplexity generally indicates a better fit.

`PP(W) = exp[-(1/N) x sum(ln(Pi)), i = 1 to N]`

Here, `N` is the number of probabilities evaluated. If any probability is zero, the sentence probability is zero and perplexity is infinite without smoothing.

## Algorithm

1. Read the training corpus and the test sentence.
2. Convert the text to lowercase and tokenize it, retaining only alphanumeric words.
3. Count all unigrams, bigrams, and trigrams in the training corpus.
4. Calculate unigram probabilities by dividing word counts by the total number of words.
5. Calculate bigram probabilities by dividing bigram counts by the count of the first word.
6. Calculate trigram probabilities by dividing trigram counts by the count of the first two words.
7. Extract n-grams from the test sentence and calculate their probabilities.
8. Multiply the probabilities to obtain the sentence probability for each model.
9. Calculate perplexity using the logarithm of the probabilities.
10. Display the probability tables, sentence probabilities, and perplexities.

## Setup

Software: Python 3.x.  
Modules used: `re`, `math`, and `collections` (standard Python library). No external installation is required.

Save the program as `Code.py` and run it using:

```bash
python Code.py
```

## Program

```python
import re
import math
from collections import Counter

documents = [
    "I am Sam.",
    "Sam I am.",
    "Sam am I.",
    "I do not like green eggs and Sam."
]
test_sentence = "Sam am I"

def tokenize(text):
    return re.findall(r"[a-z0-9]+", text.lower())

def ngrams(words, n):
    return [tuple(words[i:i+n])
            for i in range(len(words)-n+1)]

corpus = [tokenize(d) for d in documents]
test = tokenize(test_sentence)

C = {n: Counter(g for s in corpus for g in ngrams(s, n))
     for n in (1, 2, 3)}
total = sum(C[1].values())

print("INPUT CORPUS")
for i, d in enumerate(documents, 1):
    print(f"Sentence {i}: {d}")
print("\nTest Sentence:", test_sentence)

results = []

for n in (1, 2, 3):
    print(f"\nTEST SENTENCE - {n}-GRAM PROBABILITIES")

    if n == 1:
        print(f"{'Word':<15}{'Count':>10}"
              f"{'Total Words':>15}{'Probability':>15}")
    elif n == 2:
        print(f"{'Bigram':<18}{'Count':>10}"
              f"{'Previous Count':>18}{'Probability':>15}")
    else:
        print(f"{'Trigram':<18}{'Count':>10}"
              f"{'Bigram Count':>18}{'Probability':>15}")

    p = 1.0
    k = 0

    for gram in ngrams(test, n):
        count = C[n][gram]
        denominator = total if n == 1 else C[n-1][gram[:-1]]
        probability = count / denominator if denominator else 0.0

        print(f"{' '.join(gram):<18}{count:>10}"
              f"{denominator:>18}{probability:>15.4f}")

        p *= probability
        k += 1

    perplexity = (
        math.exp(-math.log(p) / k)
        if p > 0 and k > 0 else float("inf")
    )
    results.append((n, p, perplexity))

print("\nPROBABILITY & PERPLEXITY OF TEST SENTENCE")
print(f"{'Model':<15}{'Probability':>20}{'Perplexity':>18}")
print("-" * 53)

for n, p, pp in results:
    print(f"{'Unigram' if n == 1 else 'Bigram' if n == 2 else 'Trigram':<15}"
          f"{p:>20.6f}{pp:>18.4f}")
```

## Output

```text
INPUT CORPUS
Sentence 1: I am Sam.
Sentence 2: Sam I am.
Sentence 3: Sam am I.
Sentence 4: I do not like green eggs and Sam.

Test Sentence: Sam am I

TEST SENTENCE - 1-GRAM PROBABILITIES
Word Count Total Words Probability
sam 4 17 0.2353
am 3 17 0.1765
i 4 17 0.2353

TEST SENTENCE - 2-GRAM PROBABILITIES
Bigram Count Previous Count Probability
sam am 1 4 0.2500
am i 1 3 0.3333

TEST SENTENCE - 3-GRAM PROBABILITIES
Trigram Count Bigram Count Probability
sam am i 1 1 1.0000

PROBABILITY & PERPLEXITY OF TEST SENTENCE
Model Probability Perplexity
-----------------------------------------------------
Unigram 0.009770 4.6777
Bigram 0.083333 3.4641
Trigram 1.000000 1.0000
```

## Result

Thus, the Python program was executed successfully to extract unigrams, bigrams, and trigrams from the given text corpus and calculate the probability and perplexity of the test sentence “Sam am I”. The sentence probabilities were 0.009770, 0.083333, and 1.000000, with perplexities of 4.6777, 3.4641, and 1.0000, respectively.

---

# Experiment 4 - CKY Parsing for Sentence Analysis

## Aim

To develop a Python program to implement the Cocke-Younger-Kasami (CYK) parsing algorithm and analyze a sentence by displaying its parsing table and parse trees, including structural ambiguity.

## Theory

CYK is a bottom-up dynamic programming algorithm used in NLP to determine whether a sentence can be generated by a Context-Free Grammar (CFG). The grammar is represented in Chomsky Normal Form (CNF), with rules `A -> BC` or `A -> a`.

The algorithm initializes diagonal cells using terminal rules and fills larger spans by combining smaller spans. If the start symbol `S` appears in the cell for the complete sentence, the sentence is accepted. Structural ambiguity occurs when a sentence has more than one valid parse tree.

### Grammar Used

```text
S    -> Pron VP
NP   -> Det N | NP PP
VP   -> V NP | VP PP
PP   -> P N
Pron -> i
Det  -> the
N    -> man | telescope
V    -> saw
P    -> with
```

## Setup

No external libraries are required. Save the code as `cyk_parsing.py` and run:

```bash
python cyk_parsing.py
```

## Program

```python
# CYK Parsing with Parse Trees and Ambiguity Detection
G = {
    'S': [('Pron', 'VP')],
    'NP': [('Det', 'N'), ('NP', 'PP')],
    'VP': [('V', 'NP'), ('VP', 'PP')],
    'PP': [('P', 'N')],
    'Pron': ['i'],
    'Det': ['the'],
    'N': ['man', 'telescope'],
    'V': ['saw'],
    'P': ['with']
}

words = input("Enter sentence: ").lower().split()
n = len(words)
if n == 0:
    print("Empty sentence")
    raise SystemExit

# Store every parse tree for each non-terminal in each cell.
table = [[{} for _ in range(n)] for _ in range(n)]

# Initialize cells with terminal productions.
for i, word in enumerate(words):
    for lhs, rules in G.items():
        if word in rules:
            table[i][i].setdefault(lhs, []).append((lhs, word))

# Fill the CYK table using binary productions.
for length in range(2, n + 1):
    for i in range(n - length + 1):
        j = i + length - 1
        for k in range(i, j):
            for lhs, rules in G.items():
                for rule in rules:
                    if isinstance(rule, tuple):
                        left, right = rule
                        for lt in table[i][k].get(left, []):
                            for rt in table[k + 1][j].get(right, []):
                                tree = (lhs, lt, rt)
                                table[i][j].setdefault(lhs, []).append(tree)

print("\nCYK Parsing Table:")
for length in range(1, n + 1):
    cells = [sorted(table[i][i + length - 1].keys())
             for i in range(n - length + 1)]
    print("Length", length, ":", cells)

def show_tree(tree, prefix="", last=True):
    branch = "└── " if last else "├── "
    print(prefix + branch + tree[0], end="")
    if len(tree) == 2 and isinstance(tree[1], str):
        print(" -> " + tree[1])
        return
    print()
    for index, child in enumerate(tree[1:]):
        new_prefix = prefix + (" " if last else "│ ")
        show_tree(child, new_prefix, index == len(tree[1:]) - 1)

parses = table[0][n - 1].get('S', [])
if not parses:
    print("\nSentence is REJECTED")
else:
    print("\nSentence is ACCEPTED")
    print("Number of parse trees:", len(parses))
    for index, tree in enumerate(parses, 1):
        print("\nParse Tree", index)
        show_tree(tree)
    if len(parses) > 1:
        print("\nAMBIGUITY DETECTED: multiple parse trees found.")
    else:
        print("\nNo ambiguity detected.")
```

## Input

```text
i saw the man with telescope
```

## Output

```text
Enter sentence: i saw the man with telescope

CYK Parsing Table:
Length 1 : [['Pron'], ['V'], ['Det'], ['N'], ['P'], ['N']]
Length 2 : [[], [], ['NP'], [], ['PP']]
Length 3 : [[], ['VP'], [], []]
Length 4 : [['S'], [], ['NP']]
Length 5 : [[], ['VP']]
Length 6 : [['S']]

Sentence is ACCEPTED
Number of parse trees: 2

Parse Tree 1
└── S
  ├── Pron -> i
  └── VP
     ├── V -> saw
     └── NP
       ├── NP
       │ ├── Det -> the
       │ └── N -> man
       └── PP
         ├── P -> with
         └── N -> telescope

Parse Tree 2
└── S
  ├── Pron -> i
  └── VP
     ├── VP
     │ ├── V -> saw
     │ ├── NP
     │   ├── Det -> the
     │   └── N -> man
     └── PP
       ├── P -> with
       └── N -> telescope

AMBIGUITY DETECTED: multiple parse trees found.
```

## Result

The CYK parsing program builds a parsing table, checks sentence acceptance, and displays the parse trees. The sample sentence has two parse trees, demonstrating structural ambiguity.

**Note:** This small teaching grammar demonstrates prepositional-phrase attachment ambiguity and recognizes only the vocabulary and structures specified in the grammar.

---

# Experiment 5 - Semantic Relationship Using Word2Vec Models: CBOW, Skip-gram

> The experiment index lists this as Experiment 5. The source page header/program comment contains a different experiment number; the index sequence is retained here.

## Aim

To develop a Python program that trains CBOW and Skip-gram Word2Vec models on a text corpus, identifies semantically similar words, and visualizes the word embeddings in 2-D.

## Theory

Word embeddings represent each word as a dense, low-dimensional vector of real numbers. Words that appear in similar contexts get similar vectors, so semantic similarity becomes geometric closeness. This follows the distributional hypothesis: “a word is characterized by the company it keeps.”

Word2Vec (Mikolov et al., 2013) is a shallow neural network with an input layer, one hidden (projection) layer and an output layer. It has two architectures: CBOW and Skip-gram.

### CBOW (Continuous Bag of Words)

- Predicts the target word from its surrounding context words.
- The context word vectors are averaged in the hidden layer, and the output layer predicts the centre word.
- It trains faster and works well for frequent words.
- Objective: maximize `P(wt | wt-c, ..., wt+c)`.

### Skip-gram

- Predicts the context words from the target word.
- It trains slower but represents rare words and small datasets better.
- Objective: maximize `sum(log(P(wt+j | wt)))` for `-c <= j <= c`, `j != 0`.

### Training

The output layer uses softmax, made cheaper with Hierarchical Softmax or Negative Sampling. Weights are updated using stochastic gradient descent.

### Cosine Similarity

Cosine similarity is used to find similar words:

`cos(A, B) = (A . B) / (||A|| ||B||)`

Its value lies between -1 and 1, and a higher value means the words are more similar.

### Principal Component Analysis (PCA)

PCA (Principal Component Analysis) reduces the 50-dimensional vectors to 2 dimensions for plotting, preserving as much variance as possible.

## Algorithm

1. Import the required modules: `re`, `numpy`, `matplotlib`, gensim Word2Vec and sklearn PCA.
2. Define the text corpus and split it into sentences.
3. Convert each sentence to lowercase and tokenize it using a regular expression.
4. Train the CBOW model (`sg=0`) and the Skip-gram model (`sg=1`) with `vector_size=50`, `window=2`, `min_count=1` and 100 epochs.
5. Display the vocabulary of the trained model.
6. Find the three words most similar to `cat` in each model using cosine similarity.
7. Display the 50-dimensional vector of `cat` for both models.
8. Reduce the word vectors of each model to two dimensions using PCA.
9. Plot the CBOW and Skip-gram embeddings side by side and display the figure.

## Setup

**Software requirements:** Python 3.11.3 (IDLE).

**Installation**

```bash
pip install gensim numpy scikit-learn matplotlib
```

**Modules and functions used**

| Module / Function | Purpose |
|---|---|
| `re` | Cleans and tokenizes the text |
| `numpy` | Stores word vectors as arrays |
| `gensim.models.Word2Vec` | Trains CBOW (`sg=0`) and Skip-gram (`sg=1`) models |
| `sklearn.decomposition.PCA` | Reduces vectors to 2-D |
| `matplotlib.pyplot` | Plots the embeddings |

**Model parameters**

| Parameter | Value | Meaning |
|---|---:|---|
| `vector_size` | 50 | Embedding dimension |
| `window` | 2 | Context window size |
| `min_count` | 1 | Keeps every word (small corpus) |
| `sg` | 0/1 | 0 = CBOW, 1 = Skip-gram |
| `epochs` | 100 | Training iterations |
| `seed` | 42 | Reproducible results |

## Program

```python
# Experiment 6: CBOW and Skip-gram Word2Vec
import re
import numpy as np
import matplotlib.pyplot as plt
from gensim.models import Word2Vec
from sklearn.decomposition import PCA

corpus = ("Cat chases mouse. Dog chases cat. Cat eats food. Mouse eats cheese. "
          "Dog likes food. Cat likes fast mouse. Mouse runs away fast. "
          "Dog sees cat. Cat catches mouse. Mouse sees cheese. Dog runs fast.")
print("Input Corpus:", corpus)

sentences = [re.findall(r"[a-z]+", s.lower())
             for s in corpus.split(".") if s.strip()]
params = dict(sentences=sentences, vector_size=50, window=2,
              min_count=1, epochs=100, workers=1, seed=42)
cbow_model = Word2Vec(sg=0, **params)
skipgram_model = Word2Vec(sg=1, **params)

print("\nVocabulary:")
print(list(cbow_model.wv.index_to_key))

def show_similar(model, name, word="cat", topn=3):
    print(f"\n{name} - Words similar to '{word}':")
    for w, score in model.wv.most_similar(word, topn=topn):
        print(f"{w} : {round(float(score), 4)}")

show_similar(cbow_model, "CBOW")
show_similar(skipgram_model, "Skip-gram")

print("\nCBOW Vector for 'cat':")
print(cbow_model.wv['cat'])

print("\nSkip-gram Vector for 'cat':")
print(skipgram_model.wv['cat'])

def plot_embeddings(model, ax, title):
    words = list(model.wv.index_to_key)
    vectors = np.array([model.wv[w] for w in words])
    pts = PCA(n_components=2).fit_transform(vectors)
    colors = plt.cm.tab10(np.arange(len(words)) % 10)
    for i, w in enumerate(words):
        ax.scatter(pts[i, 0], pts[i, 1], color=colors[i], s=15)
        ax.annotate(w, (pts[i, 0], pts[i, 1]), textcoords="offset points",
                    xytext=(5, 5), fontsize=8)
    ax.set_title(title, fontsize=10)
    ax.set_xlabel("PCA Component 1")
    ax.set_ylabel("PCA Component 2")
    ax.grid(True)

fig, axes = plt.subplots(1, 2, figsize=(12, 5.5))
plot_embeddings(cbow_model, axes[0], "CBOW Word Embeddings")
plot_embeddings(skipgram_model, axes[1], "Skip-gram Word Embeddings")
fig.suptitle("Comparison of CBOW and Skip-gram", fontsize=10)
plt.tight_layout()
plt.show()
```

## Output

```text
Input Corpus: Cat chases mouse. Dog chases cat. Cat eats food. Mouse eats cheese. Dog likes food. Cat likes fast mouse. Mouse runs away fast. Dog sees cat. Cat catches mouse. Mouse sees cheese. Dog runs fast.

Vocabulary:
['mouse', 'cat', 'dog', 'fast', 'sees', 'runs', 'likes', 'cheese', 'food', 'eats', 'chases', 'catches', 'away']

CBOW - Words similar to 'cat':
away : 0.3376
fast : 0.2139
chases : 0.1121

Skip-gram - Words similar to 'cat':
away : 0.3386
fast : 0.2158
likes : 0.1118

CBOW Vector for 'cat':
[ 1.0486514e-02 -1.2210890e-02 -5.3366399e-03 -1.4814921e-03
  3.6201065e-05 -1.8222753e-02  1.7428596e-03 -1.3817335e-02
  9.7055119e-03  7.3709297e-03  1.7157245e-02  1.0028817e-02
 -5.2939146e-03  1.8882053e-02 -3.5236576e-03 -6.8570599e-03
  1.6162792e-02 -5.5672717e-03 -1.7153412e-02 -1.3123377e-03
  1.1755271e-02 -1.2613110e-02 -1.5555378e-03 -1.4711404e-02
  7.7367658e-03 -1.0675213e-03 -6.8027172e-03 -1.0930081e-02
  2.6176586e-03  6.7546084e-03  1.7704504e-02 -2.5735390e-03
 -1.3841429e-02  1.3411613e-02  5.2656406e-03  7.9208445e-03
 -1.6239224e-02 -7.5955559e-03  1.0683928e-02  1.3363403e-02
 -2.4162759e-03  1.2238638e-02  1.3770238e-02 -4.6154493e-03
  1.6205814e-02 -8.4798625e-03 -1.0604118e-02  7.3218164e-03
  5.6321328e-03 -1.4545176e-02]

Skip-gram Vector for 'cat':
[ 1.04900207e-02 -1.22335311e-02 -5.44941146e-03 -1.52819336e-03
  5.49842916e-05 -1.83281749e-02  1.74556370e-03 -1.39044747e-02
  9.70258564e-03  7.36442348e-03  1.71914678e-02  1.00290971e-02
 -5.36356214e-03  1.89959761e-02 -3.50536173e-03 -6.80559641e-03
  1.62063166e-02 -5.59674529e-03 -1.71482414e-02 -1.30798889e-03
  1.18102347e-02 -1.27065899e-02 -1.59330294e-03 -1.46907279e-02
  7.79230380e-03 -1.03014125e-03 -6.88598631e-03 -1.08652310e-02
  2.51395372e-03  6.69009099e-03  1.77240837e-02 -2.57595256e-03
 -1.38866315e-02  1.34983892e-02  5.33055514e-03  8.00628308e-03
 -1.62861310e-02 -7.53935752e-03  1.06790364e-02  1.34788305e-02
 -2.43633171e-03  1.23180635e-02  1.39276525e-02 -4.63991892e-03
  1.61888953e-02 -8.41944851e-03 -1.05841458e-02  7.39898579e-03
  5.63563826e-03 -1.46840969e-02]
```

The original manual includes side-by-side PCA scatter plots titled **CBOW Word Embeddings** and **Skip-gram Word Embeddings**, under the overall title **Comparison of CBOW and Skip-gram** (manual page 31).

## Result

CBOW and Skip-gram Word2Vec models were successfully trained on the text corpus. Similar words and word vectors for `cat` were displayed, and the PCA plots were used to compare the word embeddings of the two models.

---

# Experiment 6 - Language Translation Using SMT / IBM Model 1

> The index identifies this experiment as Language Translation Using SMT. The section heading on the experiment pages reads “Language Translation Using NMT/NLP Libraries”; the theory and program in those pages describe and implement IBM Model 1 statistical machine translation. Both source labels are noted here.

## Aim

Develop a Python-based language translation system to translate text from English to French using NLP techniques and a library, and evaluate the translations.

## Theory

### Machine Translation

Machine translation (MT) automatically converts text from a source language to a target language. The main approaches are rule-based MT (hand-written dictionaries and grammar rules), statistical MT (learned from parallel corpora) and neural MT (deep networks). The manual states that this lab builds a transfer-based rule-based translator because each translation decision can be traced to one rule (see Step 3).

### IBM Model 1

IBM Model 1 is a word-alignment model that learns translation probabilities `t(f | e)`, where `e` is an English word and `f` is a French word. A NULL token is added to the English sentence to account for French words that do not align to a regular English word. The model assumes that alignment positions are selected uniformly.

The model is trained without manually labelled word alignments using the Expectation-Maximization (EM) algorithm.

### Expectation-Maximization (EM)

- **E-step:** Calculate expected fractional counts for each English-French word pair using the current translation probabilities.
- **M-step:** Normalize the expected counts to update the translation probabilities `t(f | e)`.

The EM algorithm iteratively improves the translation probabilities until they stabilize. IBM Model 1 learns word correspondences, but it does not model word order or target-language fluency.

### BLEU Score

BLEU (Bilingual Evaluation Understudy) evaluates machine translation by comparing n-gram overlap between the generated translation and a reference translation. A higher BLEU score generally indicates closer overlap with the reference.

## Algorithm

1. Define a parallel corpus containing English and French sentence pairs.
2. Tokenize each sentence using lowercase conversion and `split()`.
3. Add a NULL token to every English sentence.
4. Initialize translation probabilities for observed English-French word pairs.
5. Perform the E-step to calculate expected alignment counts.
6. Perform the M-step to update and normalize translation probabilities.
7. Display the log-likelihood after each training iteration.
8. Align each French word with the most probable English word.
9. Translate unseen English sentences using the learned word probabilities.
10. Compare the translations with reference sentences using BLEU and analyze the errors.

## Setup

**Software requirements**

- Python 3.x
- NLTK library

**Installation**

```bash
pip install nltk
```

## Program

```python
import math
from collections import defaultdict
from nltk.translate.bleu_score import sentence_bleu, SmoothingFunction

# Parallel corpus: English -> French
pairs = [
    ("the house", "la maison"),
    ("the book", "le livre"),
    ("a house", "une maison"),
    ("a book", "un livre"),
    ("the white house", "la maison blanche"),
    ("the white book", "le livre blanc"),
    ("a cat", "un chat"),
    ("the black cat", "le chat noir"),
    ("i see the house", "je vois la maison"),
    ("i see the cat", "je vois le chat"),
    ("i see a book", "je vois un livre")
]

def tokenize(text):
    return text.lower().split()

data = [(["NULL"] + tokenize(en), tokenize(fr)) for en, fr in pairs]

possible_f = defaultdict(set)
for en, fr in data:
    for e in en:
        possible_f[e].update(fr)

t = {}
for e, french_words in possible_f.items():
    for f in french_words:
        t[(f, e)] = 1.0 / len(french_words)

def log_likelihood():
    total = 0.0
    for en, fr in data:
        for f in fr:
            prob = sum(t.get((f, e), 0.0) for e in en) / len(en)
            total += math.log(max(prob, 1e-300))
    return total

print("STEP 1 - Training IBM Model 1 with EM")
print("Corpus size:", len(pairs), "sentence pairs")
for iteration in range(1, 13):
    count_fe = defaultdict(float)
    count_e = defaultdict(float)
    for en, fr in data:
        for f in fr:
            denom = sum(t.get((f, e), 0.0) for e in en)
            if denom:
                for e in en:
                    delta = t.get((f, e), 0.0) / denom
                    count_fe[(f, e)] += delta
                    count_e[e] += delta
    for (f, e), value in count_fe.items():
        t[(f, e)] = value / count_e[e]
    print(f"iter {iteration:2d}: log-likelihood = {log_likelihood():.4f}")

def best_translation(e):
    candidates = [(prob, f) for (f, source), prob in t.items()
                  if source == e]
    return max(candidates)[1] if candidates else e

def align(en, fr):
    src = ["NULL"] + tokenize(en)
    result = []
    for f in tokenize(fr):
        e = max(src, key=lambda word: t.get((f, word), 0.0))
        result.append((f, e, t.get((f, e), 0.0)))
    return result

print("\nSTEP 2 - Sample word alignments")
for en, fr in [pairs[4], pairs[5]]:
    print(f"EN: {en!r} | FR: {fr!r}")
    for f, e, prob in align(en, fr):
        print(f" {f:<8} <-- {e:<8} t={prob:.3f}")

tests = [
    ("the black house", "la maison noire"),
    ("i see a white cat", "je vois un chat blanc")
]
smooth = SmoothingFunction().method1
print("\nSTEP 3 - Translation and BLEU evaluation")
for source, reference in tests:
    output = " ".join(best_translation(w) for w in tokenize(source))
    score = sentence_bleu([tokenize(reference)], tokenize(output),
                          smoothing_function=smooth)
    print("Source :", source)
    print("SMT output:", output)
    print("Reference :", reference)
    print(f"BLEU score: {score:.3f}\n")

print("Note: IBM Model 1 learns word translations, but this simple decoder")
print("does not model French word order, agreement, or a language model.")
```

## Output

The sample output reports a corpus size of 12 sentence pairs and performs 12 EM iterations. (The visible `pairs` list in the source program contains 11 pairs.) The reported log-likelihood values and word alignments are:

```text
STEP 1 - Training IBM Model 1 with EM
Corpus size: 12 sentence pairs
iter  1: log-likelihood = -59.2122
iter  2: log-likelihood = -54.4281
iter  3: log-likelihood = -51.6992
iter  4: log-likelihood = -50.2495
iter  5: log-likelihood = -49.4767
iter  6: log-likelihood = -49.0509
iter  7: log-likelihood = -48.8058
iter  8: log-likelihood = -48.6582
iter  9: log-likelihood = -48.5656
iter 10: log-likelihood = -48.5053
iter 11: log-likelihood = -48.4649
iter 12: log-likelihood = -48.4371

STEP 2 - Sample word alignments
EN: 'the white house' | FR: 'la maison blanche'
la       <-- house    t=0.328
maison   <-- house    t=0.655
blanche  <-- white    t=0.498
EN: 'the white book' | FR: 'le livre blanc'
le       <-- the      t=0.746
livre    <-- book     t=0.997
blanc    <-- white    t=0.497

STEP 3 - Translation and BLEU evaluation
Source : the black house
SMT output: le noir maison
Reference : la maison noire
BLEU score: 0.114

Source : i see a white cat
SMT output: vois vois un blanche chat
Reference : je vois un chat blanc
BLEU score: 0.126
```

## Result

Thus, the Python program for Statistical Machine Translation using IBM Model 1 was developed. Translation probabilities were trained using the Expectation-Maximization algorithm, word alignments were displayed, unseen English sentences were translated, and the output was evaluated against French reference translations using BLEU.

---

# Experiment 7 - Language Translation Using NMT (LSTM)

## Aim

To develop a Python program that builds a small Neural Machine Translation (NMT) model using an LSTM encoder-decoder to translate English sentences into French.

## Theory

### Neural Machine Translation

NMT uses a single neural network to translate a sentence from a source language to a target language. The encoder-decoder architecture is the basic design used for this task.

### Encoder-Decoder with LSTM

- **Encoder:** an Embedding layer and an LSTM read the English sentence and produce the final hidden state `h` and cell state `c`.
- **Decoder:** a second LSTM starts from `(h, c)` and predicts the French words one by one through a Dense softmax layer.
- **Teacher forcing:** during training the decoder receives the correct previous French word; during testing it uses its own previous prediction (greedy decoding).
- The tokens `<s>` and `</s>` mark the start and end of a French sentence.

## Algorithm

1. Define a small set of English-French sentence pairs.
2. Add the `<s>` and `</s>` tokens to the French sentences and build word-to-index vocabularies.
3. Pad all sentences to a fixed length and prepare the encoder input, decoder input and decoder target.
4. Build the LSTM encoder-decoder model and train it for 300 epochs.
5. Translate sentences by repeatedly predicting the next French word until `</s>` appears.

## Setup

Software: Python 3.x with TensorFlow/Keras and NumPy.

```bash
pip install tensorflow numpy
```

Model setup: Embedding(32) + LSTM(64) in encoder and decoder; loss: sparse categorical cross-entropy; optimizer: Adam; 6 training pairs.

## Program

```python
import numpy as np
from tensorflow.keras.layers import Input, Embedding, LSTM, Dense
from tensorflow.keras.models import Model

pairs = [
    ("i see the cat", "je vois le chat"),
    ("i see a book", "je vois un livre"),
    ("the cat is black", "le chat est noir"),
    ("the house is white", "la maison est blanche"),
    ("i like the school", "j aime l ecole"),
    ("she has a dog", "elle a un chien")
]
src = [e.split() for e, _ in pairs]
tgt = [["<s>"] + f.split() + ["</s>"] for _, f in pairs]
sv = {w: i + 1 for i, w in enumerate(sorted({w for s in src for w in s}))}
tv = {w: i + 1 for i, w in enumerate(sorted({w for s in tgt for w in s}))}
inv = {i: w for w, i in tv.items()}
ls, lt = max(map(len, src)), max(map(len, tgt))
enc = lambda s, v, n: [v.get(w, 0) for w in s] + [0] * (n - len(s))

X = np.array([enc(s, sv, ls) for s in src])
D = np.array([enc(s[:-1], tv, lt) for s in tgt])
Y = np.array([enc(s[1:], tv, lt) for s in tgt])

ei = Input((ls,))
di = Input((lt,))
_, h, c = LSTM(64, return_state=True)(Embedding(len(sv) + 1, 32)(ei))
do = LSTM(64, return_sequences=True)(
    Embedding(len(tv) + 1, 32)(di), initial_state=[h, c]
)
model = Model([ei, di], Dense(len(tv) + 1, activation="softmax")(do))
model.compile("adam", "sparse_categorical_crossentropy", metrics=["accuracy"])
model.fit([X, D], Y, epochs=300, verbose=0)
print("Training accuracy:", round(model.evaluate([X, D], Y, verbose=0)[1], 3))

def translate(s):
    x = np.array([enc(s.lower().split(), sv, ls)])
    d, out = [tv["<s>"]], []
    for _ in range(lt - 1):
        dd = np.array([d + [0] * (lt - len(d))])
        w = inv.get(
            int(model.predict([x, dd], verbose=0)[0][len(d) - 1].argmax())
        )
        if w == "</s>":
            break
        out.append(w)
        d.append(tv[w])
    return " ".join(out)

for s in ["i see the cat", "the cat is black", "she has a dog", "i see a book"]:
    print(f"EN: {s:<20} FR: {translate(s)}")
```

## Output

```text
Training accuracy: 1.0
EN: i see the cat               FR: je vois le chat
EN: the cat is black            FR: le chat est noir
EN: she has a dog               FR: elle a un chien
EN: i see a book                FR: je vois un livre
```

## Result

Thus, a small encoder-decoder LSTM translation model was built and executed successfully. The model reached 100% training accuracy and translated the English sentences into French correctly. As only 6 sentence pairs were used, it memorizes the corpus and cannot translate unseen words.

---

# Experiment 8 - Next Word Prediction Using LSTM

## Aim

To develop a Python program to build a next-word prediction model using a given text corpus.

## Theory

### Language Modelling and Next-Word Prediction

A language model assigns a probability to the next word given the words that came before it. Next-word prediction is the task of choosing the most probable word `w_t` from the vocabulary after seeing the history `w_1 ... w_(t-1)`. Two broad approaches exist: statistical n-gram models (count how often a word follows the previous n-1 words) and neural models (learn dense word representations and a recurrent network that reads the history). This lab builds a neural model with an LSTM (Long Short-Term Memory) network, because it can use the whole sentence so far as context, not just a fixed window of one or two words.

### NLP Pipeline Used

- **Tokenization:** the Keras `Tokenizer` lowercases the corpus, removes punctuation and assigns every distinct word an integer index (1, 2, 3, ...). Index 0 is reserved for padding, so `vocab_size = number of distinct words + 1`.
- **N-gram sequence generation:** every sentence is expanded into growing prefixes. The sentence “rain falls heavily” gives `[rain, falls]` and `[rain, falls, heavily]`. In each prefix the last word is the label and the words before it are the input. This turns one sentence into many training examples.
- **Padding:** the neural network needs fixed-length input, so every prefix is padded with zeros on the left (pre-padding) up to `max_len`, the length of the longest prefix.
- **Input / label split:** `X` = all columns except the last, `y` = the last column. `y` is one-hot encoded to a vector of length `vocab_size`, because the output is a choice among all vocabulary words.
- **Embedding layer:** maps each word index to a dense 100-dimensional vector that is learned during training, so words used in similar contexts get similar vectors.
- **LSTM layer:** reads the embedded words one by one and keeps a memory (cell state) of the sentence. Its three gates decide what to forget, what to store and what to output at each step.
- **Dense + softmax layer:** converts the LSTM output into a probability for every word in the vocabulary; the word with the highest probability (`argmax`) is the predicted next word.

### LSTM Cell and Training Equations

```text
f_t = sigmoid(W_f[h_(t-1), x_t] + b_f)     (forget gate)
i_t = sigmoid(W_i[h_(t-1), x_t] + b_i)     (input gate)
g_t = tanh(W_g[h_(t-1), x_t] + b_g)        (candidate memory)
c_t = f_t * c_(t-1) + i_t * g_t            (cell state)
o_t = sigmoid(W_o[h_(t-1), x_t] + b_o)
h_t = o_t * tanh(c_t)
softmax(z_j) = exp(z_j) / sum_k exp(z_k)
loss = -sum_j y_j * log(p_j)               (categorical cross-entropy)
next word = word with index argmax_j p_j
```

### Model Summary and Corpus Statistics

The corpus has 10 sentences (73 word tokens). After tokenization the vocabulary size is 65 (64 distinct words + 1 padding index). N-gram expansion produces 63 training sequences with `max_len = 9`, so `X` has shape `(63, 8)` and `y` has shape `(63, 65)`.

| Layer | Output shape | Parameters |
|---|---|---:|
| Embedding (65 x 100) | `(None, 8, 100)` | 6,500 |
| LSTM (150 units) | `(None, 150)` | 150,600 |
| Dense (softmax, 65) | `(None, 65)` | 9,815 |
| **Total** |  | **166,915** |

The Embedding layer has `65 x 100 = 6,500` weights. The LSTM has `4 x ((100 + 150) x 150 + 150) = 150,600` weights (four gates, each with input weights, recurrent weights and a bias). The Dense layer has `150 x 65 + 65 = 9,815` weights.

Training setup: loss = categorical cross-entropy, optimizer = Adam, 100 epochs.

### Why an LSTM, and its Limitations

A plain n-gram model forgets everything beyond its window, and a simple RNN loses early words on long sentences. The LSTM's cell state carries information across the whole prefix, which is why “a doctor treats” can be completed with “patients”. The limitation is that the model only knows what is in the training corpus: with just 63 examples it memorizes the corpus sentences, and words it has never seen are ignored.

## Setup

```bash
pip install tensorflow numpy
python3 next_word.py
```

The command trains the model, then asks for sentences; type `exit` to stop. TensorFlow/Keras provides the tokenizer, padding utility and LSTM layers. NumPy is used for `argmax` over the predicted probabilities. Training a model this small takes only a few seconds on a CPU.

## Program

```python
# NEXT-WORD PREDICTION USING LSTM
# pip install tensorflow numpy

import numpy as np
import tensorflow as tf
from tensorflow.keras.preprocessing.text import Tokenizer
from tensorflow.keras.preprocessing.sequence import pad_sequences
from tensorflow.keras.models import Sequential
from tensorflow.keras.layers import Embedding, LSTM, Dense

# 1. TEXT CORPUS
corpus = """
The sun rises early in the morning.
Children walk to school carrying colorful bags.
A teacher explains mathematics using simple examples.
Birds build nests on tall green trees.
The farmer grows vegetables in the fertile soil.
Rain falls heavily during the monsoon season.
A doctor treats patients at the local hospital.
Engineers design bridges and modern buildings.
Students read books inside the quiet library.
The chef prepares delicious food for hungry customers.
"""

# 2. TOKENIZATION AND SEQUENCES
tokenizer = Tokenizer()
tokenizer.fit_on_texts([corpus])
vocab_size = len(tokenizer.word_index) + 1

sequences = []
for sentence in corpus.lower().split("\n"):
    if sentence.strip():
        words = tokenizer.texts_to_sequences([sentence])[0]
        for i in range(1, len(words)):
            sequences.append(words[:i + 1])

max_len = max(map(len, sequences))
sequences = pad_sequences(sequences, maxlen=max_len, padding="pre")

X = sequences[:, :-1]
y = tf.keras.utils.to_categorical(
    sequences[:, -1], num_classes=vocab_size
)

# 3. BUILD AND TRAIN LSTM MODEL
model = Sequential([
    Embedding(vocab_size, 100, input_length=max_len - 1),
    LSTM(150),
    Dense(vocab_size, activation="softmax")
])

model.compile(
    loss="categorical_crossentropy",
    optimizer="adam",
    metrics=["accuracy"]
)

model.fit(X, y, epochs=100, verbose=1)

# 4. NEXT-WORD PREDICTION
def predict_next_word(text):
    seq = tokenizer.texts_to_sequences([text])[0]
    seq = pad_sequences([seq], maxlen=max_len - 1, padding="pre")

    prediction = model.predict(seq, verbose=0)
    index = np.argmax(prediction)

    for word, i in tokenizer.word_index.items():
        if i == index:
            return word

# 5. TEST
seed = "natural language"
print("\nSeed Text:", seed)
print("Predicted Next Word:", predict_next_word(seed))

# 6. USER INPUT
while True:
    text = input("\nEnter a sentence (or 'exit'): ")

    if text.lower() == "exit":
        break

    print("Predicted Next Word:", predict_next_word(text))
```

## Output

```text
Seed Text: natural language
Predicted Next Word: falls

Enter a sentence (or 'exit'): rain falls
Predicted Next Word: heavily

Enter a sentence (or 'exit'): a doctor treats
Predicted Next Word: patients

Enter a sentence (or 'exit'): students
Predicted Next Word: read

Enter a sentence (or 'exit'): the chef prepares delicious
Predicted Next Word: food

Enter a sentence (or 'exit'): exit
```

## Result

A Python program to build a next-word prediction model using a given text corpus was developed and executed successfully. The corpus was tokenized (vocabulary size 65), expanded into 63 n-gram sequences, padded to length 9 and used to train an Embedding-LSTM-Dense model for 100 epochs. The trained model correctly predicted the next word for the inputs “rain falls” (heavily), “a doctor treats” (patients), “students” (read) and “the chef prepares delicious” (food). For the unseen seed “natural language” it could not give a meaningful prediction, showing that the model is limited to the vocabulary of its training corpus.

---

# Experiment 9 - Spam Filtering Using NLP and Naive Bayes

## Aim

Develop a Python program to design and implement a spam filtering system using NLP techniques.

## Theory

### Spam Filtering as Text Classification

Spam filtering decides whether a message is spam or ham (normal). The Naive Bayes classifier applies Bayes’ theorem and assumes the words of a message are independent given its class:

`P(spam | words) proportional to P(spam) x product(P(w | spam))`

`P(w | c) = (count(w, c) + 1) / (N_c + |V|)` (Laplace smoothing)

Smoothing prevents unseen words from giving zero probability. Log-probabilities are added instead of multiplying small numbers, avoiding numerical underflow.

### NLP Preprocessing

- **Cleaning:** links and numbers are replaced by the tokens `urltoken` and `numtoken`.
- **Tokenization and stop-word removal:** split into lowercase words and remove common words.
- **Stemming:** the Porter stemmer merges word forms such as *claim*, *claims* and *claimed*.
- **Bag of words:** the message is represented by word counts.

### Evaluation Metrics

`Precision = TP / (TP + FP)`  
`Recall = TP / (TP + FN)`  
`F1 = 2 x Precision x Recall / (Precision + Recall)`

A false positive means a normal message wrongly marked as spam.

## Setup

Installation commands:

```bash
pip install nltk
python3 spam_filter.py
```

NLTK is used only for the Porter stemmer, so no `nltk.download(...)` call is needed and the program runs offline. The Naive Bayes classifier is implemented from scratch.

## Program

```python
import math
import re
import sys
from collections import Counter
from nltk.stem import PorterStemmer

STEM = PorterStemmer()
STOP = {
    "a", "an", "the", "is", "are", "am", "to", "of", "in", "on", "at",
    "it", "i", "me", "my", "you", "your", "we", "and", "be", "for",
    "will", "can", "was", "so", "that", "this", "with"
}

SPAM = [
    "Congratulations! You have won a free prize. Click http://win.example to claim now",
    "URGENT! Your account is suspended. Verify your password at http://bank.example now",
    "Win cash now!!! Limited offer, reply YES to claim your 1000 reward",
    "Free entry in a weekly competition to win a brand new phone. Text WIN to 80085",
    "You are selected for a free gift card. Claim your prize today",
    "Get cheap loans approved instantly. No credit check, apply now",
    "Buy cheap medicines online. Special discount, order now",
    "Earn money fast from home! Guaranteed income, click here",
    "Final notice: you have won a lottery of 50000 dollars. Send your bank details to claim",
    "Exclusive offer! 50% off all products, limited time only, buy now",
    "Your free ringtone is waiting. Reply STOP to cancel. Claim free now",
    "Hot singles near you are waiting. Click the link to join free",
    "Act now to get a free vacation. Winner announced, call 0900123456 to claim",
    "Lowest price guaranteed on watches. Click to buy and win a bonus gift",
    "Dear customer your card is blocked. Update details immediately at www.secure-bank.example",
    "Make 5000 dollars weekly working from home. Apply today, free registration",
    "You are our lucky winner! Claim your cash prize now before it expires",
    "Cheap insurance quotes, save money today. Click here for a free quote",
    "Urgent: confirm your password to avoid account closure. Click the link now",
    "Free trial offer! Order today and get a second product free, limited stock"
]

HAM = [
    "Hi, are we still meeting for lunch tomorrow?",
    "Please send me the notes from today's lecture",
    "The project report is due on Friday, please review it",
    "Can you call me when you reach home?",
    "Happy birthday! Hope you have a wonderful day",
    "Don't forget to bring your laptop for the lab session",
    "Meeting rescheduled to 3 pm in the conference room",
    "I will be late for dinner, start without me",
    "Thanks for helping me with the assignment yesterday",
    "The exam timetable has been uploaded to the portal",
    "Mom said she will pick you up after class",
    "Let's go for a movie this weekend if you are free",
    "Can you share the code you wrote for the experiment?",
    "Reminder: submit your lab record before Monday",
    "Great game last night, we should play again soon",
    "I left my notebook in the library, did you see it?",
    "The bus will leave at 8 in the morning, please be on time",
    "Could you review my draft and send your feedback?",
    "Dinner at my place on Saturday, bring your friends",
    "Sorry I missed your call, I was in a meeting"
]

TEST = [
    ("Congratulations, you won a free gift! Click now to claim your prize", 1),
    ("Urgent: your account will be closed, verify your password at http://secure.example", 1),
    ("Limited offer! Buy cheap watches with 70% discount today", 1),
    ("Earn cash fast from home, guaranteed money, apply now", 1),
    ("Claim your free vacation, you are the lucky winner", 1),
    ("You have been selected for a cheap loan, no credit check, reply YES", 1),
    ("Final notice: claim your lottery cash prize before it expires", 1),
    ("Hot offer: free ringtone, click the link to get yours now", 1),
    ("Are you coming to the lab tomorrow morning?", 0),
    ("Please review the report and send me your feedback", 0),
    ("Happy birthday to you, have a great day", 0),
    ("Can we meet in the library after class?", 0),
    ("The lecture notes are uploaded on the portal", 0),
    ("I will call you when the meeting is over", 0),
    ("Thanks for the lunch, see you on Friday", 0),
    ("Don't forget to submit the assignment before the deadline", 0),
    ("Free lunch at the cafeteria on Friday, come and join us", 0),
    ("Win the match tomorrow, good luck to the team", 0)
]

def preprocess(text):
    text = re.sub(r"(https?://|www\.)\S+", " urltoken ", text.lower())
    text = re.sub(r"\d+", " numtoken ", text)
    return [STEM.stem(t) for t in re.findall(r"[a-z]+", text) if t not in STOP]

class NaiveBayes:
    def __init__(self, spam, ham):
        self.cnt = {
            1: Counter(w for m in spam for w in preprocess(m)),
            0: Counter(w for m in ham for w in preprocess(m))
        }
        self.prior = {
            1: len(spam) / (len(spam) + len(ham)),
            0: len(ham) / (len(spam) + len(ham))
        }
        self.vocab = set(self.cnt[1]) | set(self.cnt[0])
        self.tot = {c: sum(self.cnt[c].values()) for c in (0, 1)}

    def logp(self, w, c):
        return math.log((self.cnt[c][w] + 1) / (self.tot[c] + len(self.vocab)))

    def spam_prob(self, text):
        words = [w for w in preprocess(text) if w in self.vocab]
        s = {
            c: math.log(self.prior[c]) + sum(self.logp(w, c) for w in words)
            for c in (0, 1)
        }
        m = max(s.values())
        e = {c: math.exp(v - m) for c, v in s.items()}
        return e[1] / (e[0] + e[1])

def banner(t):
    print("=" * 72, t, "=" * 72, sep="\n")

def main():
    nb = NaiveBayes(SPAM, HAM)
    banner("STEP 1 - Training and evaluation on unseen messages")
    print(f"Training: {len(SPAM)} spam + {len(HAM)} ham | vocabulary: {len(nb.vocab)} stems")
    top = sorted(sorted(nb.vocab),
                 key=lambda w: nb.logp(w, 1) - nb.logp(w, 0), reverse=True)[:6]
    print("Strongest spam words: " + ", ".join(top) + "\n")
    tp = fp = tn = fn = 0
    for msg, gold in TEST:
        p = nb.spam_prob(msg)
        pred = int(p >= 0.5)
        tp += pred and gold
        fp += pred and not gold
        tn += (not pred) and (not gold)
        fn += (not pred) and gold
        print(f'{"OK " if pred == gold else "MISS"} {"spam" if pred else "ham ":<5} '
              f'P(spam)={p:.3f} "{msg[:48]}"')
    prec, rec = tp / (tp + fp), tp / (tp + fn)
    print(f"\nConfusion matrix: TP={tp} FP={fp} TN={tn} FN={fn}")
    print(f"Accuracy={(tp + tn) / len(TEST):.1%} Precision={prec:.1%} "
          f"Recall={rec:.1%} F1={2 * prec * rec / (prec + rec):.1%}")

    banner("STEP 2 - Live spam check (type a message, 'quit' to exit)")
    while True:
        try:
            msg = input("Message: ").strip()
        except EOFError:
            break
        if not sys.stdin.isatty():
            print(msg)
        if msg.lower() in {"quit", "exit", ""}:
            print()
            break
        p = nb.spam_prob(msg)
        print(f"Result: {'SPAM' if p >= 0.5 else 'NOT SPAM (ham)'} (P(spam)={p:.3f})\n")

    banner("STEP 3 - Analysis of the spam filter")
    print(f"1) LEARNED WORDS: {', '.join(top)}.")
    print(f"2) RESULTS: {tp + tn}/{len(TEST)} messages correct; recall {rec:.0%}, precision {prec:.0%}.")
    print("3) FALSE POSITIVES: messages containing 'free' and 'win' can be misclassified.")
    print("4) PREPROCESSING: links and numbers become urltoken and numtoken; stemming merges forms.")
    print("5) SMALL DATA: only 40 training messages were used; real filters learn from thousands.")

if __name__ == "__main__":
    main()
```

## Sample Output

```text
STEP 1 - Training and evaluation on unseen messages
Training: 20 spam + 20 ham | vocabulary: 198 stems
Strongest spam words: now, claim, click, free, win, buy

OK spam P(spam)=1.000  "Congratulations, you won a free gift! Click now"
OK spam P(spam)=0.987  "Urgent: your account will be closed, verify your"
OK spam P(spam)=0.999  "Limited offer! Buy cheap watches with 70% discount"
OK spam P(spam)=0.999  "Earn cash fast from home, guaranteed money, apply"
OK spam P(spam)=0.995  "Claim your free vacation, you are the lucky winner"
OK spam P(spam)=0.985  "You have been selected for a cheap loan, no credit"
OK spam P(spam)=0.996  "Final notice: claim your lottery cash prize before"
OK spam P(spam)=1.000  "Hot offer: free ringtone, click the link to get"
OK ham  P(spam)=0.042  "Are you coming to the lab tomorrow morning?"
OK ham  P(spam)=0.005  "Please review the report and send me your feedback"
OK ham  P(spam)=0.031  "Happy birthday to you, have a great day"
OK ham  P(spam)=0.013  "Can we meet in the library after class?"
OK ham  P(spam)=0.026  "The lecture notes are uploaded on the portal"
OK ham  P(spam)=0.042  "I will call you when the meeting is over"
OK ham  P(spam)=0.026  "Thanks for the lunch, see you on Friday"
OK ham  P(spam)=0.008  "Don't forget to submit the assignment before the"
MISS spam P(spam)=0.558  "Free lunch at the cafeteria on Friday, come and"
MISS spam P(spam)=0.618  "Win the match tomorrow, good luck to the team"

Confusion matrix: TP=8 FP=2 TN=8 FN=0
Accuracy=88.9% Precision=80.0% Recall=100.0% F1=88.9%

STEP 2 - Live spam check
Message: Congratulations! You won a free prize, click now
Result: SPAM (P(spam)=1.000)
Message: hi, are we meeting for lunch tomorrow?
Result: NOT SPAM (ham) (P(spam)=0.013)
Message: URGENT verify your password at http://bank.example
Result: SPAM (P(spam)=0.968)
Message: submit the lab record on monday
Result: NOT SPAM (ham) (P(spam)=0.017)
Message: free tickets, win cash today
Result: SPAM (P(spam)=0.990)
Message: quit

STEP 3 - Analysis of the spam filter
1) Learned words: now, claim, click, free, win, buy.
2) Results: 16/18 messages correct; recall 100%, precision 80%.
```

The manual further notes:

- False positives: “Free lunch ...” and “Win the match ...” contain spam-heavy words.
- Preprocessing: links/numbers become `urltoken`/`numtoken`; stemming merges word forms.
- Small data: only 40 training messages were used.

## Result

A Python program to implement a spam filter using NLP preprocessing and a Naive Bayes classifier was developed and executed successfully. On 18 unseen messages it classified 16 correctly (accuracy 88.9%, recall 100%, precision 80%), and it checks messages typed by the user. The two errors were normal messages containing the words *free* and *win*, showing the limits of a bag-of-words model.

---

# Experiment 10 - Implementation of Chatbot Using NLP Techniques

## Aim

To develop a Python program to design and implement a chatbot using Natural Language Processing (NLP) techniques and analyze its responses.

## Theory

### Chatbots and Their Types

A chatbot is a program that holds a conversation with a user in natural language. Three broad designs exist: rule-based bots (hand-written pattern-to-reply rules), retrieval-based bots (pick the best stored reply by matching the user's message against known examples) and generative bots (neural language models that compose new sentences). This lab builds a retrieval-based, intent-driven bot deliberately, because every step is a classical NLP technique that can be inspected and explained.

### NLP Pipeline Used

- **Tokenization:** split the sentence into lowercase word tokens (regular expression, no downloads).
- **Stop-word removal:** drop words with little meaning for intent (the, is, you, what, how ...).
- **Stemming:** reduce word forms to a common root with the Porter stemmer (applying, applied, apply all become `appli`), so differently inflected questions still match.
- **TF-IDF vectorization:** represent each sentence as a vector. Term frequency counts how often a stem occurs in the sentence; inverse document frequency down-weights stems that appear in many training patterns, so rare informative words (hostel, library) dominate common ones.
- **Cosine similarity:** compare the user's vector with every training-pattern vector.

### Intent Classification by Nearest Pattern

Each training sentence belongs to an intent (greeting, fees, library ...). For a new message the bot finds the most similar training pattern, and its intent decides the reply:

`tfidf(w, d) = tf(w, d) x idf(w)`  
`idf(w) = ln((1 + N) / (1 + df(w))) + 1`  
`cos(q, d) = (q . d) / (|q| |d|)`  
`intent(q) = intent of the pattern d with the largest cos(q, d)`

If the best similarity is below a threshold (0.20 here) the bot answers with a fallback message instead of guessing. A small regular-expression entity extractor stores the user's name, giving the bot a minimal conversational memory.

### Why TF-IDF + Cosine?

It needs no large training corpus, trains instantly, and always returns a similarity score that explains why the bot replied as it did. Its limitation is that it only sees word overlap, not meaning or word order.

## Setup

```bash
pip install nltk
python3 nlp_chatbot.py
```

The command runs the evaluation, then live chat: type a message, `quit` to exit.

Tokenization uses a plain regular expression, and Porter stemming is a pure algorithm, so no `nltk.download(...)` call is needed and the program runs on lab machines without internet once the package is installed. NLTK is used only for `PorterStemmer`; the TF-IDF model is written from scratch.

## Program

```python
"""
Experiment 10 - Retrieval-based chatbot using NLP techniques
Pipeline: tokenize -> stop-word removal -> Porter stemming -> TF-IDF
      -> cosine similarity -> intent -> response (+ name memory)
Run: python3 nlp_chatbot.py (evaluation, then live chat: type your message, 'quit' to exit)
"""
import math
import random
import re
import sys
from collections import Counter
from nltk.stem import PorterStemmer  # algorithm only, no downloads

random.seed(0)
STEM = PorterStemmer()
STOP = {
    "a", "an", "the", "is", "are", "am", "to", "of", "in", "on", "at", "do",
    "does", "you", "your", "me", "my", "i", "it", "can", "please", "there",
    "for", "and", "be", "have", "will", "what", "how", "when", "where",
    "which", "tell", "about", "much", "so", "as", "with", "this", "that"
}
THRESHOLD = 0.20  # below this similarity -> fallback reply

INTENTS = {  # intent: (training patterns, responses)
    "greeting": (
        ["hello", "hi there", "hey", "good morning", "greetings"],
        ["Hello! How can I help you today?"]
    ),
    "goodbye": (
        ["bye", "goodbye", "see you later", "see you soon", "good night"],
        ["Goodbye! Have a great day."]
    ),
    "thanks": (
        ["thanks", "thank you", "thanks a lot", "appreciate your help"],
        ["You're welcome!"]
    ),
    "identity": (
        ["who are you", "what is your name", "what are you called",
         "introduce yourself"],
        ["I am CampusBot, a chatbot built with NLP techniques."]
    ),
    "admission": (
        ["how do i apply for admission", "admission process",
         "how to join the college", "application form for admission"],
        ["Admissions open in June. Apply online on the college portal."]
    ),
    "fees": (
        ["what is the fee structure", "how much are the tuition fees",
         "how to pay fees", "semester fee amount"],
        ["Fees are paid semester-wise on the college portal."]
    ),
    "timetable": (
        ["exam timetable", "when are the exams", "exam schedule",
         "class timetable"],
        ["Timetables are published on the notice board and portal."]
    ),
    "library": (
        ["library timings", "when does the library open",
         "how to borrow books", "library opening hours"],
        ["The library is open 8 AM to 8 PM on weekdays."]
    ),
    "hostel": (
        ["hostel facilities", "how to get a hostel room",
         "hostel accommodation", "room allotment"],
        ["Apply for a hostel room at the hostel office after admission."]
    ),
    "contact": (
        ["phone number of the college", "contact details", "email address",
         "office contact number"],
        ["Office: 044-0000000 | office@college.example (9 AM - 5 PM)."]
    )
}

FALLBACK = "Sorry, I did not understand. Ask about admission, fees, exams, library, hostel or contact."

def preprocess(text):
    """lowercase -> tokenize -> remove stop words -> stem"""
    return [
        STEM.stem(t)
        for t in re.findall(r"[a-z0-9]+", text.lower())
        if t not in STOP
    ]

class TfidfIntentModel:
    def __init__(self, intents):
        self.docs = [
            (preprocess(p), lab)
            for lab, (ps, _) in intents.items()
            for p in ps
        ]
        n = len(self.docs)
        df = Counter(w for d, _ in self.docs for w in set(d))
        self.idf = {
            w: math.log((1 + n) / (1 + c)) + 1
            for w, c in df.items()
        }
        self.vecs = [(self.vec(d), lab) for d, lab in self.docs]

    def vec(self, tokens):
        v = {
            w: c * self.idf[w]
            for w, c in Counter(tokens).items()
            if w in self.idf
        }
        norm = math.sqrt(sum(x * x for x in v.values()))
        return {w: x / norm for w, x in v.items()} if norm else {}

    def classify(self, text):
        q, best, score = self.vec(preprocess(text)), None, 0.0
        for v, lab in self.vecs:
            s = sum(x * v.get(w, 0.0) for w, x in q.items())  # cosine similarity
            if s > score:
                best, score = lab, s
        return (best, score) if score >= THRESHOLD else ("fallback", score)

class ChatBot:
    HOW_RE = re.compile(
        r"\bhow (?:are|r) (?:you|u)(?: doing)?\b|\bhow is it going\b",
        re.I
    )
    STATUS = "I'm doing great, thanks for asking!"

    def __init__(self):
        self.model, self.name = TfidfIntentModel(INTENTS), None

    def reply(self, text):
        m = re.search(r"\b(?:my name is|call me)\s+([A-Za-z]+)", text, re.I)
        if m:
            self.name = m.group(1).capitalize()
            return f"Nice to meet you, {self.name}! How can I help?", "name_entity", 1.0

        asked = bool(self.HOW_RE.search(text))  # small-talk: "how are you"
        label, s = self.model.classify(self.HOW_RE.sub(" ", text))
        hello = f"Hello again, {self.name}!" if self.name else "Hello!"

        if label == "greeting":
            return (
                f"{hello} {self.STATUS} How can I help you today?" if asked
                else f"{hello} How can I help you today?"
            ), label, s
        if asked and label == "fallback":
            return f"{self.STATUS} How can I help you?", "how_are_you", 1.0
        if label == "fallback":
            return FALLBACK, label, s

        answer = random.choice(INTENTS[label][1])
        return (f"{self.STATUS} {answer}" if asked else answer), label, s

TEST_SET = [
    ("hey there", "greeting"),
    ("see you tomorrow", "goodbye"),
    ("thank you so much", "thanks"),
    ("what should I call you", "identity"),
    ("how can I apply to the college", "admission"),
    ("how much do I need to pay as fees", "fees"),
    ("when is the exam", "timetable"),
    ("what time does the library close", "library"),
    ("can I get a room in the hostel", "hostel"),
    ("what is the office phone number", "contact"),
    ("is the canteen open on sunday", "fallback"),
    ("tell me a joke", "fallback")
]

def banner(t):
    print("=" * 72, t, "=" * 72, sep="\n")

def main():
    bot = ChatBot()
    banner("STEP 1 - Evaluation on unseen test sentences")
    ok = 0
    for q, gold in TEST_SET:
        pred, s = bot.model.classify(q)
        ok += pred == gold
        print(f' {"OK " if pred == gold else "MISS"} "{q}" gold={gold} pred={pred} sim={s:.3f}')

    print(f"\n Accuracy = {ok}/{len(TEST_SET)} = {ok / len(TEST_SET):.1%}")

    banner("STEP 2 - Live chat (type a message, 'quit' to exit)")
    while True:
        try:
            u = input("You: ").strip()
        except EOFError:
            break
        if not sys.stdin.isatty():
            print(u)  # echo piped input so the session is readable
        if u.lower() in {"quit", "exit", ""}:
            print("CampusBot: Goodbye!\n")
            break
        r, intent, _ = bot.reply(u)
        print(f"CampusBot: {r}\n")
        if intent == "goodbye":
            break

if __name__ == "__main__":
    main()
```

## Output

### Evaluation on Unseen Test Sentences

```text
STEP 1 - Evaluation on unseen test sentences
OK "hey there" gold=greeting pred=greeting sim=1.000
OK "see you tomorrow" gold=goodbye pred=goodbye sim=0.669
OK "thank you so much" gold=thanks pred=thanks sim=1.000
OK "what should I call you" gold=identity pred=identity sim=1.000
OK "how can I apply to the college" gold=admission pred=admission sim=0.572
OK "how much do I need to pay as fees" gold=fees pred=fees sim=1.000
OK "when is the exam" gold=timetable pred=timetable sim=1.000
OK "what time does the library close" gold=library pred=library sim=1.000
OK "can I get a room in the hostel" gold=hostel pred=hostel sim=1.000
OK "what is the office phone number" gold=contact pred=contact sim=0.667
MISS "is the canteen open on sunday" gold=fallback pred=library sim=0.735
OK "tell me a joke" gold=fallback pred=fallback sim=0.000

Accuracy = 11/12 = 91.7%
```

### Live Chat Sample

```text
You: hi
CampusBot: Hello! How can I help you today?

You: hello how are you
CampusBot: Hello! I'm doing great, thanks for asking! How can I help you today?

You: my name is Priya
CampusBot: Nice to meet you, Priya! How can I help?

You: hello
CampusBot: Hello again, Priya! How can I help you today?

You: how are you?
CampusBot: I'm doing great, thanks for asking! How can I help you?

You: how do I apply for admission
CampusBot: Admissions open in June. Apply online on the college portal.

You: what is the fee structure
CampusBot: Fees are paid semester-wise on the college portal.

You: when does the library open
CampusBot: The library is open 8 AM to 8 PM on weekdays.

You: what is the weather today
CampusBot: Sorry, I did not understand. Ask about admission, fees, exams, library, hostel or contact.

You: thanks
CampusBot: You're welcome!

You: bye
CampusBot: Goodbye! Have a great day.
```

## Result

A Python program to implement a retrieval-based chatbot using NLP techniques (tokenization, stop-word removal, Porter stemming, TF-IDF and cosine-similarity intent matching) was developed and executed successfully. The bot accepts live user input (for example “hi” or “hello how are you”) and prints a reply. The classifier reached 11/12 (91.7%) accuracy on unseen test sentences. The one error (“is the canteen open on sunday”, answered as a library query) and the effect of stop-word removal were analyzed, showing the limits of a bag-of-words approach.

---

## End of All 10 Experiments

**End of the Natural Language Processing Theory with Laboratory record.**
