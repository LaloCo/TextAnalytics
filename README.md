# Using the Azure Text Analytics Cognitive Service

This project uses Microsoft Azure's Text Analytics Cognitive Service to analyze different sets of text and extract key information that can be very important to achieve several business objectives. It is conformed of a single Python Notebook that:

- Analyzes the sentiment in "_documents_"
- Extracts key phrases and words
- Executes some manual processing of a text file
- Analyzes the important part of a text to extract the most used words

## Installation

You can clone this repository locally and start editing the _ipynb_ file in Jupyter Notebooks or other tools such as Google Colab. If you have Anaconda installed you can install Jupyter Notebooks, start a server and open this file. If you don't want to install anything, you can also try using Google Colab or Azure Notebooks.

I recommend using Google Colab, here are the steps that you need to perform to get this repo in your Drive folders:

1. Mount Drive on a new Google Colab notebook (which you can create [here](https://colab.research.google.com/)
```python
from google.colab import drive
drive.mount('/content/drive')
```
2. Change directory over to one of the folders in your Drive:
```python
%cd drive/My\ Drive/repos/TextAnalytics
```
> Note: be very mindful about that __%__ sign, if you use the usual __!__ the cd command won't work.
3. Clone the repo preferrably using this notation:
```python
!git clone https://{github_username}:{github_password_with_url_encoding}@github.com/LaloCo/TextAnalytics.git
```

## Usage

The first code block in the notebook defines the URL and KEY for the Cognitive Service, I strongly suggest you create your own Text Analytics Cognitive Service over on [azure.com](https://azure.microsoft.com/) (you can create a free account and even get 200 USD of credit). When creating the service you may not select South Central US as the location, so you would have to update right here, and also, you will have your own keys, so update that here as well.

```python
textAnalyticsURL = 'southcentralus.api.cognitive.microsoft.com'
textAnalyticsKey = 'd01a6b835c8244619c42e824dc2faf19'
```

The last cell on the other hand displays the distribution of words in a bar chart only up until the 60th most used word, you can of course change that.


```python
%matplotlib inline
import matplotlib.pyplot as plt

counts = fd_df.sort_values(0, ascending = False)
ar = plt.figure(figsize=(16,9))
ax = ar.gca()
counts[0][:60].plot(kind='bar', ax=ax)
ax.set_title("Frequency Distribution")
ax.set_ylabel("Freq. or words")
ax.set_xlabel("Stems")
plt.show()
```

![png](output_7_0.png)

## Contributing

Please read the CONTRIBUTING.md
