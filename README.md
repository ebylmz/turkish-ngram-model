# 📖 Turkish Syllable-Based N-Gram Language Model

This repository contains an implementation of a statistical language model for Turkish. The goal is to model the Turkish language statistically by working at the **syllable level**, rather than words or characters, which is especially relevant for agglutinative languages like Turkish. The project uses 1-Gram (unigram), 2-Gram (bigram), and 3-Gram (trigram) models and applies Good-Turing smoothing to handle unseen sequences. The model is evaluated using perplexity, and random sentences are generated to observe the quality of predictions. 

Please see the detailed explanation in the [project report](report.pdf).

---

## 📁 Folder Structure

    .
    ├── data/                  # Raw and preprocessed data
    ├── src/                   # Source code and modules
    ├── demo.ipynb             # Main notebook for training and evaluation
    ├── report.pdf             # Project report
    └── README.md              # This documentation


---

## 🚀 How to Run

1. Clone this repository:
   ```bash
   git clone https://github.com/yourusername/turkish-syllable-ngram-model.git
   cd turkish-syllable-ngram-model
   ```
2. Install required dependencies:
   ```bash
    pip install -e .
   ```

3. Download [Turkish Wikipedia Dump](https://www.kaggle.com/datasets/mustfkeskin/turkish-wikipedia-dump) from Kaggle, and place into **data** folder.

3. Run the [Jupyter notebook](demo.ipynb):
   ```bash
    jupyter notebook demo.ipynb
   ```

4. Follow the steps inside the notebook to:
    - Preprocess the data
    - Train the N-gram models
    - Evaluate perplexity
    - Generate sentences

---

## 🔄 Execution Pipeline

### 1. 🔧 Preprocessing

Preprocessing consisted of the following steps:

#### I. Lowercasing and Character Normalization
- All characters were converted to lowercase.
- Turkish characters were replaced with their English equivalents for consistency.

#### II. Cleaning
- Non-alphabetic characters (punctuation, numbers, etc.) were removed.

#### III. Syllabification
- Each word was segmented into syllables using an open-source library:
  [ftkurt/python-syllable](https://github.com/ftkurt/python-syllable)

#### IV. Tokenization and Formatting
- Special tokens were added to denote sentence boundaries and spaces.
- Resulting tokenized data was written to a new file preserving structure.

#### V. Dataset Splitting
- The tokenized data was split into training (95%) and test (5%) sets.

---

## 2. 🧠 Model Training

### N-Gram Models
- Implemented **unigram**, **bigram**, and **trigram** models.
- Frequency counts were stored in nested dictionaries for space and time efficiency.

### Good-Turing Smoothing
- Applied to all N-gram models to avoid zero probabilities for unseen sequences.
- Improves generalization and robustness by redistributing probability mass.

---

## 3. 📉 Evaluation with Perplexity

**Perplexity** measures how well the language model predicts unseen data:
- Lower perplexity = better performance
- Calculated using the **chain rule of probability** and **Markov assumptions**
- Logarithmic probabilities were used to avoid underflow

### Example Sentences and Their Perplexity Scores

| Sentence | Unigram | Bigram | Trigram |
|----------|---------|--------|---------|
| Kablumbağalar uzun yaşar. | 280.03 | 40.33 | 4.33 |
| Cengiz han dünyaya hükmetti. | 152.35 | 28.49 | 4.45 |
| Soğuktan üşüyen kediye süt ısıtıp verdi. | 159.40 | 35.70 | 7.81 |
| Ormanda yürüyüş yaparken... | 136.28 | 29.64 | 11.17 |
| Dağların zirvesine tırmanırken... | 98.61 | 34.60 | 12.76 |

### Overall Perplexity

| Model   | Perplexity |
|---------|------------|
| Unigram | 126.94     |
| Bigram  | 26.63      |
| Trigram | 8.58       |


---

## 4. ✍️ Random Sentence Generation

Sentences were generated using the top 5 most probable next syllables at each step.

### Example Outputs

#### 🔹 Unigram (1-Gram)

- la..la le.la lalalela.lala la.le.la la..lelelala.lelala...
- . ...lela lalale.le lalalalala .le le. le..lelela lele le. la.lalalalela . ..le lale

#### 🔹 Bigram (2-Gram)

- birle olamasinadogu ikisinindadir olusmaktaydi olanmislarlarina anayaziya olustusureket oluslaraktigini verini i alanma verenlerindenlemelerindaginindekiyeti ala isecim onemlerden icindenlerlerinda
- verengibilimcileresinayilindigibiligin olanmalarinayinetirilmek ve ise ve icin onem alamalarinden ola birlerece ozellidir olustur.yinedegininmisti ilereceleri olusmaktaydi bir birlinemindandirmesi

#### 🔹 Trigram (3-Gram)

- rostan anafilenin yapildiktan alan verilerekta bulu ana gorecelinince isein verenlererasinaviniminininluteryenler.adalarin yasasi verileri bulunabilgisa dayanirlar tarihli veya sahipliginagini a
- tepe veri olusturmasinabilimlererasinabilimin bir yapilan verenle ikilestirilendirmeye verilir.ocak.yiginin.yilinininluteryen takma olusmayacaksa verildikle illeriyken birlikin ozelligiyla alandaki

Trigram sentences are noticeably more coherent and grammatically sound, highlighting the benefit of larger context windows.

---

## Conclusion

- Trigram model achieved the best perplexity and most coherent sentences.
- As the N-gram order increases, model performance improves.
- Good-Turing smoothing was effective in mitigating sparsity.

---

## 📚 References

- [Turkish Wikipedia Dump (Kaggle)](https://www.kaggle.com/datasets/mustfkeskin/turkish-wikipedia-dump)
- [Syllabification Tool](https://github.com/ftkurt/python-syllable)
- Manning, C., Schütze, H. *Foundations of Statistical Natural Language Processing*

--- 

Feel free to ⭐ star this repo or fork it for your own research or academic use!