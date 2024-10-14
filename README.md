# Considering Bias in Data

## Project Goal

The main goal of this homework is to analyze the biases present in English Wikipedia articles and understand their implications on data representation. Towards the end, we identify potential sources of bias, discuss the limitations of using Wikipedia as a data source, and reflect on how it affects the way society thinks.

### Key Objectives

- **Data Acquisition:** Clean raw input data by removing duplicates and handling missing values, then use the MediaWiki API and ORES to obtain quality scores for politicians' articles, merge this with population data, and calculate metrics like articles per capita and high-quality articles per capita for countries and regions. Unmatched countries should be documented, while matched data should be saved for further analysis. Further, generate two metrics that tells the count of articles/high-quality articles per capita for both countries and regions.
- **Data Analysis:** Summarize the findings through six tables: the top and bottom ten countries by coverage, the top and bottom ten countries by high-quality articles, and coverage metrics by geographic regions.

This project follows to the best practices for open scientific research as mentioned in chapters "Assessing Reproducibility" and "The Basic Reproducible Workflow Template" of ["The Practice of Reproducible Research: Case Studies and Lessons from the Data-Intensive Sciences"](https://www.ucpress.edu/books/the-practice-of-reproducible-research/paper) publication, ensuring transparency and reproducibility throughout the process.

## Licenses
### Input Data
The Wikipedia [Category:Politicians by nationality](https://en.wikipedia.org/wiki/Category:Politicians_by_nationality) was crawled to generate a list of Wikipedia article pages about politicians (politicians_by_country_AUG.2024.csv) from a wide range of countries. The webpage is licensed under the [Creative Commons Attribution-ShareAlike 4.0 International](f_the_Creative_Commons_Attribution-ShareAlike_4.0_International_License) License. Contributers can share and adapt the material for any purpose, even commercially, as long as they give appropriate credit to Wikipedia, indicate any changes made, and distribute the contributions under the same license.

This population dataset (population_by_country_AUG.2024.csv) was downloaded from the [world population data sheet](https://www.prb.org/international/indicator/population/table) published by the Population Reference Bureau. For more information on the permissions, make a request [here](https://www.prb.org/permissions/).

### Data Generated for Analysis
To have additional information of the articles, we used two APIs to crawl,
- [`MediaWiki REST API for the EN Wikipedia`](https://www.mediawiki.org/wiki/API:Main_page): We used this API to obtain the `pageid` and `lastrevid`. 
- [`Objective Revision Evaluation Service (ORES)`](https://www.mediawiki.org/wiki/ORES): We used this API to obtain the quality prediction for each of the published article. 

Both the APIs are licensed under [Creative Commons Attribution-ShareAlike 3.0 Unported License](https://en.wikipedia.org/wiki/Wikipedia:Text_of_the_Creative_Commons_Attribution-ShareAlike_3.0_Unported_License). The Wikimedia Foundation's [Terms of Use](https://foundation.wikimedia.org/wiki/Policy:Terms_of_Use) allows users to freely read, print, share, and reuse educational content while contributing to various projects under free licenses. 

### Repository
The repository is licensed under the MIT License, and it permits users to freely use, modify, and distribute the code, provided that the original copyright notice and permission notice are included in all copies or substantial portions of the software.

A few snippets used in the script is developed by Dr. David W. McDonald for use in DATA 512, a course in the UW MS Data Science degree program. This code is provided under the [Creative Commons](https://creativecommons.org) [CC-BY license](https://creativecommons.org/licenses/by/4.0/). Revision 1.2 - September 16, 2024

## Workflow

The code was executed on MacBook Pro. Before running this project, ensure that the [required libraries](https://github.com/parvatijay2901/data-512-homework_2/blob/main/requirements.txt) are installed. Additionally, please create the necessary folders and adjust the file paths as required for your environment.

To run this project, execute the notebook[(considering_bias_in_data.ipynb)](https://github.com/parvatijay2901/data-512-homework_2/blob/main/scripts/considering_bias_in_data.ipynb) in the same order. 

### Step 1: Data Acquisition

In this section, we talk about transforming and combining the [politicians_by_country_AUG.2024.csv](https://github.com/parvatijay2901/data-512-homework_2/blob/main/data/input_data/politicians_by_country_AUG.2024.csv) and [population_by_country_AUG.2024.csv](https://github.com/parvatijay2901/data-512-homework_2/blob/main/data/input_data/population_by_country_AUG.2024.csv) datasets to a form required for further analysis.
1. In the initial step, we clean the raw input dataset by removing duplicates and irrelevant entries and save it as [revised_politicians_by_country_with_pageinfo_AUG.2024.csv](https://github.com/parvatijay2901/data-512-homework_2/blob/main/data/generated_intermediate_data/revised_politicians_by_country_AUG.2024.csv).
2. We then use MediaWiki's REST API for the EN Wikipedia to get additional fields - `pageid` and `current revision id`. We save the intermediate file as [revised_politicians_by_country_with_pageinfo_AUG.2024.csv](https://github.com/parvatijay2901/data-512-homework_2/blob/main/data/generated_intermediate_data/revised_politicians_by_country_with_pageinfo_AUG.2024.csv).
3. In the next step, we obtain the ORES quality predictions for each of the articles using their own API. We combine all the fields and save the intermediate file as [revised_politicians_by_country_with_pageinfo_and_quality_prediction_AUG.2024.csv](https://github.com/parvatijay2901/data-512-homework_2/blob/main/data/generated_intermediate_data/revised_politicians_by_country_with_pageinfo_and_quality_prediction_AUG.2024.csv).
4. In the subsequent steps, we combine the revised and complete politicians dataset with the population dataset. We perform some transformations and save the list of countries with no matching Wikipedia articles as [wp_countries-no_match.txt](https://github.com/parvatijay2901/data-512-homework_2/blob/main/data/generated_output_data/wp_countries-no_match.txt) and the complete daatset (where we have all the details) as [wp_politicians_by_country.csv](https://github.com/parvatijay2901/data-512-homework_2/blob/main/data/generated_output_data/wp_politicians_by_country.csv).
5. In the final step of this sub-section, we generate two more fields: 
`total_articles_per_capita` that represents the number of articles available for each person in a given country or region and `high_quality_articles_per_capita` that represents the number of high-quality articles available per person. We add the fields and again save the complete data as [articles_per_capita_analysis.csv](https://github.com/parvatijay2901/data-512-homework_2/blob/main/data/generated_intermediate_data/articles_per_capita_analysis.csv).

### Step 2: Data Analysis/Results
In this section, we produce six tables in the notebook that provides further insights into data coverage and quality across countries and regions, helping identify trends, benchmark performance, and inform resource allocation.
- **Top 10 countries by coverage:** The 10 countries with the highest total articles per capita (in descending order) .
- **Bottom 10 countries by coverage:** The 10 countries with the lowest total articles per capita (in ascending order) .
- **Top 10 countries by high quality:** The 10 countries with the highest high quality articles per capita (in descending order) .
- **Bottom 10 countries by high quality:** The 10 countries with the lowest high quality articles per capita (in ascending order).
- **Geographic regions by total coverage:** A rank ordered list of geographic regions (in descending order) by total articles per capita.
- **Geographic regions by high quality coverage:** A rank ordered list of geographic regions (in descending order) by high quality articles per capita.

## Known Issues and Special Considerations
- I observed that in some cases, the politician's name and URL appears with different countries. This probably happens because some politicians are known in multiple countries and may have different affiliations from their original nationality. To fix this, I manually checked the backgrounds of all 41 politicians and kept only the rows that clearly state their country of nationality. I dropped all other rows to make the data more accurate.
- Some politicians in the dataset had Wikipedia articles linked to them, but I noticed that several links were invalid. Upon manually checking each link, I found that six politicians had articles in non-English languages. Since our MediaWiki REST API call specifically searches for English articles, we could not fetch their information. To resolve this, I manually added the pageid and lastrevid for these politicians to link their articles to the non-English versions. However, there were two politicians for whom I was unable to find a valid Wikipedia reference. To reduce errors in the dataset, I removed their entries before calculating the ORES scores.

## Research Implications

In this analysis, I learned that the number of political articles on Wikipedia varies a lot between different countries. Smaller countries often have more articles per person, while larger countries tend to have fewer articles when you look at their population size. I was surprised to find that countries like China and India, which have many political issues to discuss, had very low articles per person. This shows that just looking at Wikipedia might not give us the full picture of political conversations happening around the world.

One of the reasons for these biases is language. Most articles on Wikipedia are in English. This can create a narrow view of global political discussions as we failed in looking at the non-English speaking countries properly. It also seems that wealthier countries, with more resources and freedom to express themselves, have a larger presence on Wikipedia. Wikipedia also tends to highlight the interests of those who can contribute, while ignoring important topics in poorer countries.

To improve this dataset and deal with these biases, future research could include articles from Wikipedia in other languages, gather data from various online platforms, and collaborate with local organizations for deeper insights. 

### What biases did you expect to find in the data (before you started working with it), and why?

Before beginning the analysis, I expected to find biases primarily related to socioeconomic factors. I thought that wealthier countries would have a higher number of political articles on Wikipedia due to better access to resources, media freedom, and the capacity to produce content. Additionally, I also thought about how the English-language articles would make it difficult for us to see the viewpoints from countries that don’t speak English.

### What (potential) sources of bias did you discover in the course of your data processing and analysis?

During the analysis, several sources of bias emerged:
- **Language Bias:** Most articles on Wikipedia are in English (especially, most of them we crawled), which means that the views from countries that don’t speak English are often left out. This makes it hard to get a clear picture of their political situations (skewed).
- **Population Bias:** Countries with big populations, like China and India, have fewer articles per person because there have a large population. This can make it seem like they have less political content available than they actually do.
- **Cultural Bias:** As far as I know, the articles on Wikipedia are mostly written by general public and we cannot entirely see the true political issues or realities of regions that don't have many contributors.

### How might a researcher supplement or transform this dataset to potentially correct for the limitations/biases you observed?

To enhance the dataset and reduce observed biases, researchers could:

- **Incorporate Data from Other Languages:** Add articles from Wikipedia in languages other than English to get a better understanding of political conversations worldwide.
- **Also Utilize Alternative Platforms:** Collect information from other places, like news websites, discussion forums, and social media, especially in countries that don’t speak English. 
- **Collaborate with Local Sources:** Partner with local journalists or organizations to gather real-life views and stories that may not be shown on Wikipedia.

## Research Practices

The project followed the best practices outlined in “The Practice of Reproducible Research” to ensure transparency and ease of replication:

- The project maintained a hierarchical structure, separating scripts and data, into distinct folders (`scripts/` and `data/`) for better organization. 
- Dependencies were clearly listed in the [requirements.txt](https://github.com/parvatijay2901/data-512-homework_2/blob/main/requirements.txt) file. This helps in easy replication of the environment.
- The workflow was automated using Jupyter notebooks. This helps in seamless re-execution of the analysis.
- We avoided hard coding paths. This made the project more simple and better adaptable for different environments.
- The scripts and functions are clearly separated to provide anyone looking into the project to have better clarity.
- Finally, the README provided clear instructions for running the project and understanding its objectives.

The project could be improved by incorporating best practices such as using logging, maintaining a .gitignore file, and applying additional workflow improvements. However, it serves its purpose for the current scope of analysis to a good extent.

## Additional Notes

ChatGPT was used in this assignment as a grammar and vocabulary checker, as well as to rephrase content that I wrote myself.

