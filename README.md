============================================================
EXPERIMENT 1 – TEXT PREPROCESSING USING NLTK
============================================================
import re
import nltk
from nltk.tokenize import sent_tokenize, word_tokenize
from nltk.corpus import stopwords
from nltk.stem import PorterStemmer, WordNetLemmatizer

for package in ["punkt", "punkt_tab", "stopwords", "wordnet",
                "omw-1.4", "averaged_perceptron_tagger_eng"]:
    nltk.download(package, quiet=True)

text = input("Enter the text corpus: ")

email_pattern = r"\b[\w.+-]+@[\w.-]+\.[A-Za-z]{2,}\b"
number_pattern = r"\b\d+(?:\.\d+)?\b"
word_pattern = r"\b[A-Za-z]+\b"
special_pattern = r"[^A-Za-z0-9\s]"

print("\nREGULAR EXPRESSIONS")
print("Alphabetic Words:", re.findall(word_pattern, text))
print("Numbers:", re.findall(number_pattern, text))
print("Email Addresses:", re.findall(email_pattern, text))
print("Special Characters:", re.findall(special_pattern, text))

print("\nSENTENCE TOKENIZATION")
sentences = sent_tokenize(text)
for i, sentence in enumerate(sentences, 1):
    print("Sentence", i, ":", sentence)

words = word_tokenize(text)
print("\nWORD TOKENIZATION")
print(words)

pos_words = [word for word in words if word.isalpha()]
print("\nPOS TAGGING")
for word, tag in nltk.pos_tag(pos_words):
    print(word, "->", tag)

stop_words = set(stopwords.words("english"))
filtered_words = [
    word for word in words
    if word.isalpha() and word.lower() not in stop_words
]
print("\nSTOP WORD REMOVAL")
print(filtered_words)

stemmer = PorterStemmer()
stemmed_words = [stemmer.stem(word) for word in filtered_words]
print("\nSTEMMING")
for original, stemmed in zip(filtered_words, stemmed_words):
    print(original, "->", stemmed)

lemmatizer = WordNetLemmatizer()
lemmatized_words = [
    lemmatizer.lemmatize(word) for word in filtered_words
]
print("\nLEMMATIZATION")
for original, lemma in zip(filtered_words, lemmatized_words):
    print(original, "->", lemma)

print("\nFINAL RESULTS")
print("Stemmed Words:", stemmed_words)
print("Lemmatized Words:", lemmatized_words)
print("Text preprocessing completed successfully.")


============================================================
EXPERIMENT 2 – TF-IDF AND COSINE SIMILARITY
============================================================
import re
import math
from collections import Counter

docs = {
    "D1": "the cat sat on the mat",
    "D2": "the dog sat on the log",
    "D3": "the cat chased the dog",
    "D4": "dogs and cats are pets"
}

words = {
    name: re.findall(r"\b\w+\b", text.lower())
    for name, text in docs.items()
}
N = len(docs)
terms = sorted(set(word for tokens in words.values() for word in tokens))

tf = {}
df = Counter()

for name, tokens in words.items():
    counts = Counter(tokens)
    tf[name] = {
        term: counts[term] / len(tokens)
        for term in terms
    }
    df.update(set(tokens))

idf = {
    term: math.log10(N / df[term])
    for term in terms
}
tfidf = {
    name: {
        term: tf[name][term] * idf[term]
        for term in terms
    }
    for name in docs
}

def heading(title):
    print("\n" + "=" * 60)
    print(title)
    print("=" * 60)

def display_table(data):
    print(f"{'Term':<12}" + "".join(f"{name:>9}" for name in docs))
    for term, values in data.items():
        print(
            f"{term:<12}" +
            "".join(f"{values[name]:>9.3f}" for name in docs)
        )

heading("TERM FREQUENCY (TF)")
display_table({
    term: {name: tf[name][term] for name in docs}
    for term in terms
})

heading("INVERSE DOCUMENT FREQUENCY (IDF)")
print(f"{'Term':<12}{'DF':>8}{'IDF':>10}")
for term in terms:
    print(f"{term:<12}{df[term]:>8}{idf[term]:>10.3f}")

heading("TF-IDF SCORES")
display_table({
    term: {name: tfidf[name][term] for name in docs}
    for term in terms
})

heading("ANALYSIS")
for name in docs:
    top = sorted(terms, key=lambda term: -tfidf[name][term])
    top = [term for term in top if tfidf[name][term] > 0][:3]
    print(name, "top keywords:", ", ".join(top))

print("Common terms:", [term for term in terms if df[term] == N] or "None")
print("Unique terms:", [term for term in terms if df[term] == 1])

def cosine(doc_a, doc_b):
    dot = sum(
        tfidf[doc_a][term] * tfidf[doc_b][term]
        for term in terms
    )
    norm_a = math.sqrt(sum(value ** 2 for value in tfidf[doc_a].values()))
    norm_b = math.sqrt(sum(value ** 2 for value in tfidf[doc_b].values()))
    return dot / (norm_a * norm_b) if norm_a and norm_b else 0.0

heading("COSINE SIMILARITY")
names = list(docs)
for i, doc_a in enumerate(names):
    for doc_b in names[i + 1:]:
        print(doc_a, "-", doc_b, ":", round(cosine(doc_a, doc_b), 3))


============================================================
EXPERIMENT 3 – UNIGRAM, BIGRAM AND TRIGRAM LANGUAGE MODELS
============================================================
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
    return [
        tuple(words[i:i + n])
        for i in range(len(words) - n + 1)
    ]

corpus = [tokenize(document) for document in documents]
test = tokenize(test_sentence)

counts = {
    n: Counter(
        gram
        for sentence in corpus
        for gram in ngrams(sentence, n)
    )
    for n in (1, 2, 3)
}
total_words = sum(counts[1].values())

print("INPUT CORPUS")
for i, document in enumerate(documents, 1):
    print("Sentence", i, ":", document)
print("\nTest Sentence:", test_sentence)

results = []

for n in (1, 2, 3):
    print(f"\nTEST SENTENCE - {n}-GRAM PROBABILITIES")

    if n == 1:
        print(f"{'Word':<15}{'Count':>10}{'Total Words':>15}{'Probability':>15}")
    elif n == 2:
        print(f"{'Bigram':<18}{'Count':>10}{'Previous Count':>18}{'Probability':>15}")
    else:
        print(f"{'Trigram':<18}{'Count':>10}{'Bigram Count':>18}{'Probability':>15}")

    probability_product = 1.0
    number_of_grams = 0

    for gram in ngrams(test, n):
        count = counts[n][gram]
        denominator = (
            total_words if n == 1
            else counts[n - 1][gram[:-1]]
        )
        probability = count / denominator if denominator else 0.0

        print(
            f"{' '.join(gram):<18}{count:>10}"
            f"{denominator:>18}{probability:>15.4f}"
        )

        probability_product *= probability
        number_of_grams += 1

    perplexity = (
        math.exp(-math.log(probability_product) / number_of_grams)
        if probability_product > 0 and number_of_grams > 0
        else float("inf")
    )
    results.append((n, probability_product, perplexity))

print("\nPROBABILITY & PERPLEXITY OF TEST SENTENCE")
print(f"{'Model':<15}{'Probability':>20}{'Perplexity':>18}")
print("-" * 53)

for n, probability, perplexity in results:
    model_name = {1: "Unigram", 2: "Bigram", 3: "Trigram"}[n]
    print(f"{model_name:<15}{probability:>20.6f}{perplexity:>18.4f}")


============================================================
EXPERIMENT 4 – CYK PARSING FOR SENTENCE ANALYSIS
============================================================
G = {
    "S": [("Pron", "VP")],
    "NP": [("Det", "N"), ("NP", "PP")],
    "VP": [("V", "NP"), ("VP", "PP")],
    "PP": [("P", "N")],
    "Pron": ["i"],
    "Det": ["the"],
    "N": ["man", "telescope"],
    "V": ["saw"],
    "P": ["with"]
}

words = input("Enter sentence: ").lower().split()
n = len(words)

if n == 0:
    print("Empty sentence")
    raise SystemExit

table = [[{} for _ in range(n)] for _ in range(n)]

for i, word in enumerate(words):
    for lhs, rules in G.items():
        if word in rules:
            table[i][i].setdefault(lhs, []).append((lhs, word))

for length in range(2, n + 1):
    for i in range(n - length + 1):
        j = i + length - 1
        for k in range(i, j):
            for lhs, rules in G.items():
                for rule in rules:
                    if isinstance(rule, tuple):
                        left, right = rule
                        for left_tree in table[i][k].get(left, []):
                            for right_tree in table[k + 1][j].get(right, []):
                                tree = (lhs, left_tree, right_tree)
                                table[i][j].setdefault(lhs, []).append(tree)

print("\nCYK PARSING TABLE")
for length in range(1, n + 1):
    cells = [
        sorted(table[i][i + length - 1].keys())
        for i in range(n - length + 1)
    ]
    print("Length", length, ":", cells)

def show_tree(tree, prefix="", last=True):
    branch = "└── " if last else "├── "
    print(prefix + branch + tree[0], end="")

    if len(tree) == 2 and isinstance(tree[1], str):
        print(" -> " + tree[1])
        return

    print()
    for index, child in enumerate(tree[1:]):
        new_prefix = prefix + ("   " if last else "│  ")
        show_tree(child, new_prefix, index == len(tree[1:]) - 1)

parses = table[0][n - 1].get("S", [])

if not parses:
    print("\nSentence is REJECTED")
else:
    print("\nSentence is ACCEPTED")
    print("Number of parse trees:", len(parses))

    for index, tree in enumerate(parses, 1):
        print("\nParse Tree", index)
        show_tree(tree)

    if len(parses) > 1:
        print("\nAMBIGUITY DETECTED")
    else:
        print("\nNo ambiguity detected.")


============================================================
EXPERIMENT 5 – WORD2VEC: CBOW AND SKIP-GRAM
============================================================
import re
import numpy as np
import matplotlib.pyplot as plt
from gensim.models import Word2Vec
from sklearn.decomposition import PCA

corpus = (
    "Cat chases mouse. Dog chases cat. Cat eats food. Mouse eats cheese. "
    "Dog likes food. Cat likes fast mouse. Mouse runs away fast. "
    "Dog sees cat. Cat catches mouse. Mouse sees cheese. Dog runs fast."
)

print("Input Corpus:", corpus)

sentences = [
    re.findall(r"[a-z]+", sentence.lower())
    for sentence in corpus.split(".")
    if sentence.strip()
]

params = {
    "sentences": sentences,
    "vector_size": 50,
    "window": 2,
    "min_count": 1,
    "epochs": 100,
    "workers": 1,
    "seed": 42
}

cbow_model = Word2Vec(sg=0, **params)
skipgram_model = Word2Vec(sg=1, **params)

print("\nVocabulary:")
print(list(cbow_model.wv.index_to_key))

def show_similar(model, name, word="cat", topn=3):
    print(f"\n{name} - Words similar to '{word}':")
    for similar_word, score in model.wv.most_similar(word, topn=topn):
        print(similar_word, ":", round(float(score), 4))

show_similar(cbow_model, "CBOW")
show_similar(skipgram_model, "Skip-gram")

print("\nCBOW Vector for 'cat':")
print(cbow_model.wv["cat"])

print("\nSkip-gram Vector for 'cat':")
print(skipgram_model.wv["cat"])

def plot_embeddings(model, ax, title):
    words = list(model.wv.index_to_key)
    vectors = np.array([model.wv[word] for word in words])
    points = PCA(n_components=2).fit_transform(vectors)

    for i, word in enumerate(words):
        ax.scatter(points[i, 0], points[i, 1], s=15)
        ax.annotate(
            word,
            (points[i, 0], points[i, 1]),
            textcoords="offset points",
            xytext=(5, 5),
            fontsize=8
        )

    ax.set_title(title)
    ax.set_xlabel("PCA Component 1")
    ax.set_ylabel("PCA Component 2")
    ax.grid(True)

fig, axes = plt.subplots(1, 2, figsize=(12, 5.5))
plot_embeddings(cbow_model, axes[0], "CBOW Word Embeddings")
plot_embeddings(skipgram_model, axes[1], "Skip-gram Word Embeddings")
fig.suptitle("Comparison of CBOW and Skip-gram")
plt.tight_layout()
plt.show()


============================================================
EXPERIMENT 6 – STATISTICAL MACHINE TRANSLATION USING IBM MODEL 1
============================================================
import math
from collections import defaultdict
from nltk.translate.bleu_score import sentence_bleu, SmoothingFunction

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

data = [
    (["NULL"] + tokenize(english), tokenize(french))
    for english, french in pairs
]

possible_f = defaultdict(set)
for english_words, french_words in data:
    for english_word in english_words:
        possible_f[english_word].update(french_words)

translation = {}
for english_word, french_words in possible_f.items():
    for french_word in french_words:
        translation[(french_word, english_word)] = 1.0 / len(french_words)

def log_likelihood():
    total = 0.0
    for english_words, french_words in data:
        for french_word in french_words:
            probability = sum(
                translation.get((french_word, english_word), 0.0)
                for english_word in english_words
            ) / len(english_words)
            total += math.log(max(probability, 1e-300))
    return total

print("STEP 1 - TRAINING IBM MODEL 1 WITH EM")
print("Corpus size:", len(pairs), "sentence pairs")

for iteration in range(1, 13):
    count_fe = defaultdict(float)
    count_e = defaultdict(float)

    for english_words, french_words in data:
        for french_word in french_words:
            denominator = sum(
                translation.get((french_word, english_word), 0.0)
                for english_word in english_words
            )

            if denominator:
                for english_word in english_words:
                    delta = (
                        translation.get((french_word, english_word), 0.0)
                        / denominator
                    )
                    count_fe[(french_word, english_word)] += delta
                    count_e[english_word] += delta

    for (french_word, english_word), value in count_fe.items():
        translation[(french_word, english_word)] = (
            value / count_e[english_word]
        )

    print(
        f"Iteration {iteration:2d}: "
        f"log-likelihood = {log_likelihood():.4f}"
    )

def best_translation(english_word):
    candidates = [
        (probability, french_word)
        for (french_word, source_word), probability in translation.items()
        if source_word == english_word
    ]
    return max(candidates)[1] if candidates else english_word

def align(english, french):
    source = ["NULL"] + tokenize(english)
    result = []

    for french_word in tokenize(french):
        english_word = max(
            source,
            key=lambda word: translation.get((french_word, word), 0.0)
        )
        result.append((
            french_word,
            english_word,
            translation.get((french_word, english_word), 0.0)
        ))

    return result

print("\nSTEP 2 - SAMPLE WORD ALIGNMENTS")
for english, french in [pairs[4], pairs[5]]:
    print("EN:", english, "| FR:", french)
    for french_word, english_word, probability in align(english, french):
        print(f"{french_word:<8} <-- {english_word:<8} t={probability:.3f}")

tests = [
    ("the black house", "la maison noire"),
    ("i see a white cat", "je vois un chat blanc")
]

smooth = SmoothingFunction().method1

print("\nSTEP 3 - TRANSLATION AND BLEU EVALUATION")
for source, reference in tests:
    output = " ".join(
        best_translation(word) for word in tokenize(source)
    )
    score = sentence_bleu(
        [tokenize(reference)],
        tokenize(output),
        smoothing_function=smooth
    )

    print("Source:", source)
    print("SMT output:", output)
    print("Reference:", reference)
    print(f"BLEU score: {score:.3f}\n")


============================================================
EXPERIMENT 7 – NEURAL MACHINE TRANSLATION USING LSTM
============================================================
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

src = [english.split() for english, _ in pairs]
tgt = [
    ["<s>"] + french.split() + ["</s>"]
    for _, french in pairs
]

src_vocab = {
    word: index + 1
    for index, word in enumerate(
        sorted({word for sentence in src for word in sentence})
    )
}
tgt_vocab = {
    word: index + 1
    for index, word in enumerate(
        sorted({word for sentence in tgt for word in sentence})
    )
}
inverse_vocab = {index: word for word, index in tgt_vocab.items()}

src_len = max(map(len, src))
tgt_len = max(map(len, tgt))

def encode(sentence, vocabulary, length):
    return (
        [vocabulary.get(word, 0) for word in sentence]
        + [0] * (length - len(sentence))
    )

X = np.array([encode(sentence, src_vocab, src_len) for sentence in src])
D = np.array([
    encode(sentence[:-1], tgt_vocab, tgt_len)
    for sentence in tgt
])
Y = np.array([
    encode(sentence[1:], tgt_vocab, tgt_len)
    for sentence in tgt
])

encoder_input = Input((src_len,))
decoder_input = Input((tgt_len,))

embedded_encoder = Embedding(len(src_vocab) + 1, 32)(encoder_input)
_, hidden, cell = LSTM(64, return_state=True)(embedded_encoder)

embedded_decoder = Embedding(len(tgt_vocab) + 1, 32)(decoder_input)
decoder_output = LSTM(
    64,
    return_sequences=True
)(embedded_decoder, initial_state=[hidden, cell])

output = Dense(len(tgt_vocab) + 1, activation="softmax")(decoder_output)

model = Model([encoder_input, decoder_input], output)
model.compile(
    optimizer="adam",
    loss="sparse_categorical_crossentropy",
    metrics=["accuracy"]
)
model.fit([X, D], Y, epochs=300, verbose=0)

accuracy = model.evaluate([X, D], Y, verbose=0)[1]
print("Training accuracy:", round(accuracy, 3))

def translate(sentence):
    encoded = np.array([
        encode(sentence.lower().split(), src_vocab, src_len)
    ])
    decoder_tokens = [tgt_vocab["<s>"]]
    output_words = []

    for _ in range(tgt_len - 1):
        decoder_array = np.array([
            decoder_tokens + [0] * (tgt_len - len(decoder_tokens))
        ])
        prediction = model.predict(
            [encoded, decoder_array],
            verbose=0
        )[0][len(decoder_tokens) - 1]

        word_index = int(np.argmax(prediction))
        word = inverse_vocab.get(word_index)

        if word == "</s>" or word is None:
            break

        output_words.append(word)
        decoder_tokens.append(tgt_vocab[word])

    return " ".join(output_words)

for sentence in [
    "i see the cat",
    "the cat is black",
    "she has a dog",
    "i see a book"
]:
    print(f"EN: {sentence:<20} FR: {translate(sentence)}")


============================================================
EXPERIMENT 8 – NEXT WORD PREDICTION USING LSTM
============================================================
import numpy as np
import tensorflow as tf
from tensorflow.keras.preprocessing.text import Tokenizer
from tensorflow.keras.preprocessing.sequence import pad_sequences
from tensorflow.keras.models import Sequential
from tensorflow.keras.layers import Embedding, LSTM, Dense

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

tokenizer = Tokenizer()
tokenizer.fit_on_texts([corpus])
vocab_size = len(tokenizer.word_index) + 1

sequences = []
for sentence in corpus.lower().split("\n"):
    if sentence.strip():
        word_ids = tokenizer.texts_to_sequences([sentence])[0]
        for i in range(1, len(word_ids)):
            sequences.append(word_ids[:i + 1])

max_len = max(map(len, sequences))
sequences = pad_sequences(
    sequences,
    maxlen=max_len,
    padding="pre"
)

X = sequences[:, :-1]
y = tf.keras.utils.to_categorical(
    sequences[:, -1],
    num_classes=vocab_size
)

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

def predict_next_word(text):
    sequence = tokenizer.texts_to_sequences([text])[0]
    sequence = pad_sequences(
        [sequence],
        maxlen=max_len - 1,
        padding="pre"
    )

    prediction = model.predict(sequence, verbose=0)
    index = int(np.argmax(prediction))

    for word, word_index in tokenizer.word_index.items():
        if word_index == index:
            return word

    return "Unknown"

seed = "natural language"
print("\nSeed Text:", seed)
print("Predicted Next Word:", predict_next_word(seed))

while True:
    text = input("\nEnter a sentence (or 'exit'): ")

    if text.lower() == "exit":
        break

    print("Predicted Next Word:", predict_next_word(text))


============================================================
EXPERIMENT 9 – SPAM FILTERING USING NLP AND NAIVE BAYES
============================================================
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
    return [
        STEM.stem(token)
        for token in re.findall(r"[a-z]+", text)
        if token not in STOP
    ]

class NaiveBayes:
    def __init__(self, spam_messages, ham_messages):
        self.counts = {
            1: Counter(
                word
                for message in spam_messages
                for word in preprocess(message)
            ),
            0: Counter(
                word
                for message in ham_messages
                for word in preprocess(message)
            )
        }

        total_messages = len(spam_messages) + len(ham_messages)
        self.prior = {
            1: len(spam_messages) / total_messages,
            0: len(ham_messages) / total_messages
        }

        self.vocab = set(self.counts[1]) | set(self.counts[0])
        self.total_words = {
            category: sum(self.counts[category].values())
            for category in (0, 1)
        }

    def log_probability(self, word, category):
        numerator = self.counts[category][word] + 1
        denominator = self.total_words[category] + len(self.vocab)
        return math.log(numerator / denominator)

    def spam_probability(self, text):
        words = [
            word for word in preprocess(text)
            if word in self.vocab
        ]

        scores = {
            category: math.log(self.prior[category]) +
            sum(self.log_probability(word, category) for word in words)
            for category in (0, 1)
        }

        maximum = max(scores.values())
        exponentials = {
            category: math.exp(value - maximum)
            for category, value in scores.items()
        }

        return exponentials[1] / sum(exponentials.values())

def banner(title):
    print("\n" + "=" * 72)
    print(title)
    print("=" * 72)

def main():
    classifier = NaiveBayes(SPAM, HAM)

    banner("STEP 1 - TRAINING AND EVALUATION")
    print(
        f"Training: {len(SPAM)} spam + {len(HAM)} ham | "
        f"Vocabulary: {len(classifier.vocab)} stems"
    )

    top_words = sorted(
        classifier.vocab,
        key=lambda word: (
            classifier.log_probability(word, 1)
            - classifier.log_probability(word, 0)
        ),
        reverse=True
    )[:6]
    print("Strongest spam words:", ", ".join(top_words))

    tp = fp = tn = fn = 0

    for message, actual in TEST:
        probability = classifier.spam_probability(message)
        predicted = int(probability >= 0.5)

        tp += int(predicted == 1 and actual == 1)
        fp += int(predicted == 1 and actual == 0)
        tn += int(predicted == 0 and actual == 0)
        fn += int(predicted == 0 and actual == 1)

        status = "OK" if predicted == actual else "MISS"
        label = "spam" if predicted else "ham"
        print(f'{status} {label:<5} P(spam)={probability:.3f} "{message[:48]}"')

    precision = tp / (tp + fp) if tp + fp else 0
    recall = tp / (tp + fn) if tp + fn else 0
    accuracy = (tp + tn) / len(TEST)
    f1 = (
        2 * precision * recall / (precision + recall)
        if precision + recall else 0
    )

    print(f"\nConfusion matrix: TP={tp} FP={fp} TN={tn} FN={fn}")
    print(
        f"Accuracy={accuracy:.1%} Precision={precision:.1%} "
        f"Recall={recall:.1%} F1={f1:.1%}"
    )

    banner("STEP 2 - LIVE SPAM CHECK")
    while True:
        try:
            message = input("Message: ").strip()
        except EOFError:
            break

        if message.lower() in {"quit", "exit", ""}:
            break

        probability = classifier.spam_probability(message)
        result = "SPAM" if probability >= 0.5 else "NOT SPAM (ham)"
        print(f"Result: {result} (P(spam)={probability:.3f})")

    banner("STEP 3 - ANALYSIS")
    print("Learned words:", ", ".join(top_words))
    print(f"Results: {tp + tn}/{len(TEST)} messages correct")
    print("False positives may occur when normal messages contain words like free and win.")
    print("Links and numbers are replaced by urltoken and numtoken.")
    print("A larger training dataset can improve real-world performance.")

if __name__ == "__main__":
    main()


============================================================
EXPERIMENT 10 – CHATBOT USING NLP TECHNIQUES
============================================================
import math
import random
import re
import sys
from collections import Counter
from nltk.stem import PorterStemmer

random.seed(0)
STEM = PorterStemmer()

STOP = {
    "a", "an", "the", "is", "are", "am", "to", "of", "in", "on", "at",
    "do", "does", "you", "your", "me", "my", "i", "it", "can", "please",
    "there", "for", "and", "be", "have", "will", "what", "how", "when",
    "where", "which", "tell", "about", "much", "so", "as", "with",
    "this", "that"
}

THRESHOLD = 0.20

INTENTS = {
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
        ["phone number of the college", "contact details",
         "email address", "office contact number"],
        ["Office: 044-0000000 | office@college.example (9 AM - 5 PM)."]
    )
}

FALLBACK = (
    "Sorry, I did not understand. Ask about admission, fees, exams, "
    "library, hostel or contact."
)

def preprocess(text):
    tokens = re.findall(r"[a-z0-9]+", text.lower())
    return [
        STEM.stem(token)
        for token in tokens
        if token not in STOP
    ]

class TfidfIntentModel:
    def __init__(self, intents):
        self.documents = [
            (preprocess(pattern), label)
            for label, (patterns, _) in intents.items()
            for pattern in patterns
        ]

        total_documents = len(self.documents)
        document_frequency = Counter(
            word
            for document, _ in self.documents
            for word in set(document)
        )

        self.idf = {
            word: math.log(
                (1 + total_documents) / (1 + count)
            ) + 1
            for word, count in document_frequency.items()
        }

        self.vectors = [
            (self.vector(document), label)
            for document, label in self.documents
        ]

    def vector(self, tokens):
        counts = Counter(tokens)
        values = {
            word: count * self.idf[word]
            for word, count in counts.items()
            if word in self.idf
        }

        norm = math.sqrt(sum(value ** 2 for value in values.values()))
        return {
            word: value / norm
            for word, value in values.items()
        } if norm else {}

    def classify(self, text):
        query = self.vector(preprocess(text))
        best_label = None
        best_score = 0.0

        for vector, label in self.vectors:
            score = sum(
                value * vector.get(word, 0.0)
                for word, value in query.items()
            )

            if score > best_score:
                best_label = label
                best_score = score

        if best_score >= THRESHOLD:
            return best_label, best_score

        return "fallback", best_score

class ChatBot:
    HOW_RE = re.compile(
        r"\bhow (?:are|r) (?:you|u)(?: doing)?\b|\bhow is it going\b",
        re.I
    )
    STATUS = "I'm doing great, thanks for asking!"

    def __init__(self):
        self.model = TfidfIntentModel(INTENTS)
        self.name = None

    def reply(self, text):
        match = re.search(
            r"\b(?:my name is|call me)\s+([A-Za-z]+)",
            text,
            re.I
        )

        if match:
            self.name = match.group(1).capitalize()
            return (
                f"Nice to meet you, {self.name}! How can I help?",
                "name_entity",
                1.0
            )

        asked_status = bool(self.HOW_RE.search(text))
        label, score = self.model.classify(self.HOW_RE.sub(" ", text))
        greeting = (
            f"Hello again, {self.name}!"
            if self.name else "Hello!"
        )

        if label == "greeting":
            response = (
                f"{greeting} {self.STATUS} How can I help you today?"
                if asked_status
                else f"{greeting} How can I help you today?"
            )
            return response, label, score

        if asked_status and label == "fallback":
            return f"{self.STATUS} How can I help you?", "how_are_you", 1.0

        if label == "fallback":
            return FALLBACK, label, score

        response = random.choice(INTENTS[label][1])
        if asked_status:
            response = f"{self.STATUS} {response}"

        return response, label, score

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

def banner(title):
    print("\n" + "=" * 72)
    print(title)
    print("=" * 72)

def main():
    bot = ChatBot()

    banner("STEP 1 - EVALUATION ON TEST SENTENCES")
    correct = 0

    for question, expected in TEST_SET:
        predicted, score = bot.model.classify(question)
        correct += int(predicted == expected)
        status = "OK" if predicted == expected else "MISS"
        print(
            f'{status} "{question}" expected={expected} '
            f'predicted={predicted} similarity={score:.3f}'
        )

    print(
        f"\nAccuracy = {correct}/{len(TEST_SET)} "
        f"= {correct / len(TEST_SET):.1%}"
    )

    banner("STEP 2 - LIVE CHAT")
    while True:
        try:
            user_text = input("You: ").strip()
        except EOFError:
            break

        if user_text.lower() in {"quit", "exit", ""}:
            print("CampusBot: Goodbye!")
            break

        response, intent, _ = bot.reply(user_text)
        print("CampusBot:", response)

        if intent == "goodbye":
            break

if __name__ == "__main__":
    main()


============================================================
END OF ALL 10 EXPERIMENTS
============================================================
ents; this file numbers them sequentially as Experiments 5 and 6.
