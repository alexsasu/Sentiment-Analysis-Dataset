# Sentiment-Analysis-Dataset

Group project for the Natural Language Processing 2 course taken in the 2nd year of the Artificial Intelligence master program at the Faculty of Mathematics and Computer Science, University of Bucharest.

The project consisted of supplementing an already existing corpus with samples, or creating a new corpus, and performing an NLP task on it. We chose to create a new corpus for the task of sentiment analysis, containing Romanian book reviews from the website [Goodreads](https://www.goodreads.com/).

<details>
<summary><h4>Dataset Creation:</h4></summary>

The way we chose to collect samples for the dataset was through a custom scraper built with **Selenium** and **Beautiful Soup**. We sought to **mitigate bias** in our data, so the books scraped were from 10 genres, had mostly different authors, and were from different series. After the scraping process the dataset had **6661 reviews**. Besides a "review" column containing only the actual text of the review, the .csv file of the dataset also had an "id" column automatically incremented by us, a "genre" column containing only the main genre of the book from which the review was taken, and a "label" column. The "label" column was constructed in the following way: if a review had 1 or 2 stars we would deem it "negative" and insert in the column the value 0, if it had 3 stars we would consider it "neutral" and insert in the column the value 1, and if it had 4 or 5 stars we would consider it "positive" and insert in the column the value 2. 
</details>

<details>
<summary><h4>Dataset Cleanup:</h4></summary>

In order to clean our corpus, we did the following: removed entries consisting only of links (we were interested in text, so these did not add any value to our task), removed entries missing any content in the "review" column, removed trailing and leading whitespaces in reviews, removed duplicate reviews, and performed **outliers removal through text embeddings and Isolation Forest**. After this step, our dataset had **6283 samples**.
</details>

<details>
<summary><h4>Data Preprocessing:</h4></summary>

Before training AI models and making an in-depth analysis of our data, we preprocessed it in the following ways: we normalized the text font of reviews, replaced ş Ş ţ Ţ “ ” with ș Ș ț Ț ", removed links, and removed the English variants of some reviews (in the same comment, some users wrote two variants of their review, one in English and one in Romanian). We intentionally left out other preprocessing methods, in order not to skew the training of models (for example cased transformers).
</details>

<details>
<summary><h4>Exploratory Data Analysis:</h4></summary>

![samples_visualization_after_preprocessing](https://github.com/user-attachments/assets/aa571483-a5f9-48bd-935a-9a17fae73f38)  
A lot of samples coincide with each other and are really descriptive. Moreover, on average, reviews from each category are of considerable length: 625 for negative, 741 for neutral, 829 for positive (in number of characters).

![sentiment_words_distribution](https://github.com/user-attachments/assets/79410998-d3f3-4b9b-a79f-53bb20ed877d)  
In each review category, in total there are more positive words than negative words. This was unexpected, as we thought that negative and neutral reviews would have more negative than positive words.

![image](https://github.com/user-attachments/assets/32ebbfe0-98cb-4e23-990f-7f6269bdd9aa)  
We considered only the values in bold to potentially be able to aid in the task of sentiment analysis.
</details>

<details>
<summary><h4>Machine Learning Experiments:</h4></summary>

After cleaning and preprocessing the data, we used it to fine-tune a multitude of BERT models, showing promising scores for a couple of baseline results:

|     Model     | Macro-Avg. F1 Score |
|     :---:     |        :---:        |
|   [BERT base](https://huggingface.co/dumitrescustefan/bert-base-romanian-cased-v1)   |        0.59         |
|  [RoBERT base](https://huggingface.co/readerbench/RoBERT-base)  |        0.61         |
|  [RoBERT small](https://huggingface.co/readerbench/RoBERT-small) |        0.50         |
|   [BERT Legal](https://huggingface.co/snisioi/bert-legal-romanian-cased-v1)  |        0.09         |
</details>

### Contributors:
- [Alexandru Sasu](https://github.com/alexsasu/)
- [Monica Gîrbea](https://github.com/monicaandreea/)
