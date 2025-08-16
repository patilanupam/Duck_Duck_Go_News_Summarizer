# Duck_Duck_Go_News_Summarizer


# 🤖 AI News Summarizer

A powerful yet simple Python script that automatically fetches and summarizes the latest news articles on any topic you choose. Stop sifting through long articles and get the key takeaways in seconds\!

-----

## ✨ Overview

This project provides a streamlined way to stay informed. You simply provide a topic (e.g., "advances in renewable energy" or "latest smartphone launches"), and the script does the rest:

1.  **Searches the Web**: It uses the DuckDuckGo search engine to find relevant and recent news articles related to your topic.
2.  **Extracts Article Content**: It visits each link and intelligently pulls out the main body of the article, ignoring ads, headers, and other clutter.
3.  **Generates a Summary**: It uses a sophisticated AI model from Hugging Face to read the article text and generate a concise, human-readable summary.
4.  **Displays Results**: It presents you with a clean list containing the link to the original article and its generated summary.

This tool is perfect for researchers, students, and anyone who wants to quickly get up to speed on a specific subject without the manual effort of finding and reading multiple sources.

-----

## 🛠️ Components & Libraries Used

This project is built on a few key open-source libraries. Here’s what they are and why they were chosen for the job.

### 1\. **Hugging Face `transformers`**

  * **What it is**: This is the core library for all the AI magic. It provides a straightforward way to access and use thousands of pre-trained NLP (Natural Language Processing) models for tasks like translation, sentiment analysis, and, in our case, summarization.
  * **Why we used it**: It dramatically simplifies the process of using a state-of-the-art AI model. Instead of needing to build and train a model from scratch (which would require massive amounts of data and computing power), we can use a ready-made one in just a few lines of code with the `pipeline` function.
  * **The Model**: `facebook/bart-large-cnn`
      * This specific model is a variant of Google's BART architecture that was fine-tuned by Facebook (now Meta) on the CNN/DailyMail news dataset.
      * **Why this model?**: Since it was specifically trained to summarize news articles, it's exceptionally good at identifying key information and generating high-quality summaries for the exact type of content this project handles.

### 2\. **`duckduckgo-search`**

  * **What it is**: A lightweight Python library to programmatically perform searches on DuckDuckGo.
  * **Why we used it**: It's incredibly simple, fast, and **does not require an API key** or any complex setup. This makes it a hassle-free choice for finding article URLs based on the user's query.

### 3\. **`newspaper3k`**

  * **What it is**: A library designed for article scraping and curation. Given a URL, it can download the page, identify the main article text, and extract it cleanly.
  * **Why we used it**: Web pages are messy. They have navigation bars, ads, footers, and sidebars. `newspaper3k` is specialized in parsing this HTML structure to isolate and return *only* the content of the article itself, which is exactly what we need to feed into our summarization model.

-----

## 🚀 Getting Started

Follow these steps to get the project up and running in a Google Colab environment.

### Prerequisites

  * A Google Account to use Google Colab.
  * A Hugging Face Account (Optional, but highly recommended).

### Step 1: Open Google Colab

1.  Go to [colab.research.google.com](https://colab.research.google.com).
2.  Click on **"New notebook"** to create a fresh workspace.

### Step 2: Install the Required Libraries

Before you can run the code, you need to install the libraries we discussed. Copy the following command into a new cell in your Colab notebook and run it by clicking the play button (▶️) or pressing `Shift+Enter`.

```python
!pip install transformers duckduckgo-search newspaper3k torch
```

  * This command tells Colab's package manager (`pip`) to download and install `transformers`, `duckduckgo-search`, `newspaper3k`, and `torch` (a core dependency for `transformers`).

### Step 3: (Recommended) Add Your Hugging Face API Token

The script is configured to use a Hugging Face API token. This is good practice to avoid rate limits and warnings.

1.  Log in to your [Hugging Face](https://huggingface.co/) account.
2.  Go to your profile picture in the top-right corner, then click **Settings \> Access Tokens**.
3.  Click **"New token"**, give it a name (e.g., "Colab Summarizer"), set the role to "read", and generate the token.
4.  Copy the generated token (`hf_...`).
5.  In your Colab notebook, click the **key icon (🔑) on the left sidebar** to open the "Secrets" manager.
6.  Click **"Add a new secret"**.
      * For the **Name**, enter `HF_API_TOKEN`.
      * For the **Value**, paste your copied token.
      * Toggle the switch to make it available to this notebook.

Now your script can securely access your token without you having to paste it directly into the code.

### Step 4: Add and Run the Project Code

1.  Copy the entire Python script you provided and paste it into a new cell in your Colab notebook.
2.  Run the cell. It will load the libraries and the AI model. The first time you run it, it may take a minute or two to download the model (`facebook/bart-large-cnn`). You should see a message saying the Hugging Face token was loaded successfully.

### Step 5: Use the Summarizer\!

1.  In a **new cell** below the main script, type the following code to summarize a topic of your choice.
2.  Replace `"AI in Healthcare"` with any topic you are interested in.
3.  Run the cell to see the results\!

<!-- end list -->

```python
# Now, let's use the function to get summaries
topic = "AI in Healthcare"
summaries = summarize_news(topic)

print(summaries)
```

-----

## 📋 Example Output

Running the code in Step 5 will produce an output that looks something like this:

```
🔗 https://www.example-news.com/article/ai-in-healthcare-2025
📝 Artificial intelligence is revolutionizing the healthcare industry by enabling faster and more accurate diagnoses. Machine learning algorithms are being used to analyze medical images like X-rays and MRIs, often detecting diseases earlier than human radiologists. AI is also personalizing treatment plans and accelerating drug discovery...

🔗 https://www.tech-journal.com/news/how-ai-is-changing-patient-care
📝 AI-powered tools are improving patient outcomes and streamlining hospital operations. From predictive analytics that identify at-risk patients to chatbots that provide 24/7 support, technology is making healthcare more efficient and accessible. Ethical considerations regarding data privacy and algorithmic bias remain a key area of focus for developers and policymakers...
```
