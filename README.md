
[![MIT License](https://img.shields.io/apm/l/atomic-design-ui.svg?)](https://github.com/tterb/atomic-design-ui/blob/master/LICENSEs)
![contributors](https://img.shields.io/github/contributors/sravankr96/data-512-homework_2.svg)
![codesize](https://img.shields.io/github/languages/code-size/sravankr96/data-512-homework_2.svg) 

# data-512-homework_2

Wikipedia article quality analysis to explore and understand bias

# Goal: Considering Bias in Data

The primary goal of this project is to explore and understand the general biases in the models that originate from the bias in the training data. We will be performing an analysis of politician articles in wikipedia and see how the percapita articles and percapita high-quality articles varies with in the same countries to identify possible bias.

## Navigating the repository
```bash
.
├── LICENSE
├── README.md
├── data
│   ├── politicians_by_country_SEPT.2022.csv
│   ├── population_by_country_2022.csv
│   └── wp_politicians_by_country.csv
├── data-512-homework_2.ipynb
├── figures
│   ├── article_regions_by_coverage.png
│   ├── bottom10_countries_by_coverage.png
│   ├── bottom10_highquality_countries_by_coverage.png
│   ├── highquality_article_regions_by_coverage.png
│   ├── top10_countries_by_coverage.png
│   └── top10_highquality_countries_by_coverage.png
├── intermediate_data
│   ├── page_info_responses.json
│   └── page_ores_responses.json
├── requirements.txt
└── wp_countries-no_match.txt
```

## Datasource Information

The input data for this project is extracted from the below wikipedia (politicians wikipedia pages) and prb (population) web pages. Additionally, two more endpoints are used for page information and ORES scores. The datasource endpoints are licensed under the [CC-BY-SA 3.0]( CC-BY-SA 3.0 and GFDL licenses) and [GFDL licenses](CC-BY-SA 3.0 and GFDL licenses). ORES is a machine learning tool that can provide estimates of Wikipedia article quality. The ORES API endpoint provides the article quality estimates from best to worst:

FA - Featured article

GA - Good article

B - B-class article

C - C-class article

Start - Start-class article

Stub - Stub-class article

## Issues and Special Considerations

1. There are few duplicates in the politicians input data file. All the absolute duplicates are filtered from the data but the duplicates at article name level are taken into account for per-capita calculations. 
2. There are few countries where the population is 0. This can be because the value is in millions and is rounded to the nearest decimal. These countries are filtered at Step 4 where the article-per-capita is calculated as they give infinity values because of 0 in the denominator
3. Regions with cumulative population values are eliminated and the countries are mapped to the regions that are closest/lowest in the hierarchy of regions

Links of Data sources used in this analysis:

 - [Politicians by Nationality](https://en.wikipedia.org/wiki/Category:Politicians_by_nationality)
 - [World Population](https://www.prb.org/international/indicator/population/table/)
 - [ORES REST API](https://www.mediawiki.org/wiki/ORES)
 - [Wikimedia Foundation REST API terms of use](https://www.mediawiki.org/wiki/REST_API#Terms_and_conditions)

## Research Implications

Understanding the biases in the source data will help you spot any model biases and prevent incorrect interpretation of the results. The majority of information found online is biased by nature. Numerous factors, including demographics, gender, cultural prejudices, literacy rates, etc., may contribute to the biases. Several queries regarding the articles per capita were raised during the posthoc analysis, including whether it was a trustworthy measure of coverage and whether it was related to ORES scores. In the course of the post-hoc study, few biases in the data are visible. There are biases present in Eastern Europe and Western Asia, where high-quality articles score higher than the overall number of articles. The per capita values of the articles seem to be very dependent on the population of the nation/region. For instance, the majority of the nations/regions with the highest coverage also have the lowest populations and vice versa. Non-native English speakers had fewer high-quality articles than native speakers, which suggests a linguistic and cultural prejudice. I questioned the accuracy of the per capita computation made during the last stages of the exercise due to all these inherent biases and a few extra data anomalies.

### What biases did you expect to find in the data (before you started working with it), and why?

I expected the highest quality of articles to be from the first world countries. However, it was unexpected to discover that numerous first-world nations, including the United States and Australia, were missing from the dataset following the exercise. Japan is ranked among the lowest 10 nations for high-quality articles produced per capita.
We are severely biased, in my opinion, because we only take into consideration articles written in English, even if the majority of high-caliber articles may be written in other languages in large nations like China and India.

### What might your results suggest about (English) Wikipedia as a data source?

Data is dynamically changing on multiple runs hence could lead to inconsistency in analysis. The ORES scores might not be reliable because they were generated by an AI model that might be prejudiced on the basis of ideology, race, gender, or culture. I learned from the ORES Wiki that the ORES model appears to be biased toward the article's structure rather than the content when assessing the quality of the article itself.

### Can you think of a realistic data science research situation where using these data (to train a model, perform hypothesis-driven research, or make business decisions) might create biased or misleading results, due to the inherent gaps and limitations of the data?

The above readings have a similar context along the lines of limitations of text classifiers in online content. In the article that was presented at the 2018 Conference on Fairness, Accountability, and Transparency, it is thoroughly discussed how it is crucial for policymakers to comprehend NLP's limits before making choices. The paper discusses the text classifier NLP research that is currently being done to fill in policymakers' knowledge gaps. The article backs up its arguments with a troubling illustration of how AI has exacerbated the problem of Islamophobia.

### How might a researcher supplement or transform this dataset to potentially correct for the limitations/biases you observed?

For the regions and countries, there are missing Wikipedia articles information in the dataset. Few nations have populations that are zero. The articles-per-capita may not accurately reflect actual levels because to the aforementioned two factors. The researcher should therefore extract the Wikipedia entries for the missing countries' politicians. To gain a true picture of the high-quality article per capita, it is also necessary to acquire the ORES scores of the articles for these nations.


### Additional files

1. Countries with No Match - wp_countries-no_match.txt - All countries for which there are no matches i.e., either the population dataset does not have an entry for the equivalent Wikipedia country, or vice-versa

2. Consolidated Data - wp_politicians_by_country.csv - Consolidated the remaining data that contains politicians data with population data into a single CSV file

### Screenshots

Examples of output plots generated by the functions

- Results 1: Top 10 Countries by Coverage

The plot shows the top 10 countries by coverage (total-article-per-capita)

![Top 10 Countries with highest percapita articles](https://github.com/sravankr96/data-512-homework_2/blob/main/figures/top10_countries_by_coverage.png)

- Results 2: Bottom 10 Countries by Coverage

The plot shows the bottom 10 countries by coverage (total-article-per-capita)

![Bottom 10 countries with lowest percapita articles](https://github.com/sravankr96/data-512-homework_2/blob/main/figures/bottom10_countries_by_coverage.png)

- Results 3: Top 10 Countries by High Quality Articles Coverage

The third graph contains the bar plot indicating the top 10 countries by high quality coverage (high-quality-article-per-capita)

![Top 10 countries with highest percapita articles](https://github.com/sravankr96/data-512-homework_2/blob/main/figures/top10_highquality_countries_by_coverage.png)

- Results 4: Bottom 10 Countries by High Quality Articles Coverage

The plot shows the bottom 10 countries by high quality coverage (high-quality-article-per-capita)

![Bottom 10 countries with lowest percapita articles](https://github.com/sravankr96/data-512-homework_2/blob/main/figures/bottom10_highquality_countries_by_coverage.png)

- Results 5: Geographic Regions by Total Coverage

The plot shows the regions by coverage (article-per-capita)

![Articles by Region](https://github.com/sravankr96/data-512-homework_2/blob/main/figures/article_regions_by_coverage.png)

- Results 6: Geographic Regions by High Quality Articles Coverage

The plot shows the regions by high quality coverage (high-quality-article-per-capita)

![High quality articles by region](https://github.com/sravankr96/data-512-homework_2/blob/main/figures/highquality_article_regions_by_coverage.png)

## Authors
- [Sravan Kumar Reddy Hande](https://github.com/sravankr96)

![GitHub Contributors Image](https://contrib.rocks/image?repo=sravankr96/data-512-homework_2)
