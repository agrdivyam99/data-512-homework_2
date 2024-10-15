
# Wikipedia Articles on Political Figures: Data Analysis

## Purpose

This project investigates potential biases in Wikipedia's representation of political figures from different regions and countries. We focus on the coverage and quality of articles concerning politicians, using data from Wikipedia and population datasets. By leveraging ORES (a machine learning tool for assessing article quality), we analyze how many articles exist for politicians in each country and the proportion of those that are considered high-quality.

Our aim is to identify imbalances in article coverage and quality across different countries and geographic regions. The analysis produces rankings of countries and regions based on their article coverage and quality, normalized by population size.

## Data Overview

- **Wikipedia Politicians Data**: Contains articles about politicians across various countries, including article URLs, country names, revision IDs, and ORES-predicted quality scores.
  
- **Population Data**: Provides population figures from the Population Reference Bureau, grouped by country and region (e.g., continents and subregions).

## Methodology

### 1. Data Preparation

We began by cleaning and aligning the Wikipedia and population datasets. This included handling duplicate records and ensuring consistency in country names across both datasets. The merge of these datasets is based on the country names, with any mismatches logged in `wp_countries-no_match.txt`.

### 2. Retrieving Article Quality Scores

The ORES API was used to obtain quality predictions for each Wikipedia article related to a politician. Articles rated as "FA" (Featured Article) or "GA" (Good Article) were considered high-quality. Articles that could not be rated were logged in `error_log.txt`.

### 3. Article Metadata Retrieval

Using the [MediaWiki REST API](https://www.mediawiki.org/wiki/API:Main_page), we retrieved up-to-date revision IDs for articles to ensure accuracy in quality predictions. The API documentation [API:Info](https://www.mediawiki.org/wiki/API:Info) provides further details on the data retrieval process.

### 4. Dataset Merge and Analysis

After data cleaning, the datasets were merged on country names. Unmatched entries were recorded for later review. We calculated two key metrics:
- **Articles per Capita**: Total number of articles about politicians in a country, normalized by population.
- **High-Quality Articles per Capita**: The number of high-quality articles (as rated by ORES), also normalized by population.

The analysis was also aggregated at the regional level.

### 5. Ranking Countries and Regions

Countries and regions were ranked by:
- **Articles per Capita**: Top and bottom 10 countries for article coverage.
- **High-Quality Articles per Capita**: Top and bottom 10 countries for high-quality article coverage.
- **Regional Rankings**: Rankings of geographic regions by both metrics.

### 6. Error Handling

Articles that could not be scored by ORES were logged in `error_log.txt`. The overall error rate was low, around 0.11%, which is within acceptable limits.

## Key Insights

This analysis revealed clear geographic disparities in Wikipedia's coverage of politicians. Western Europe and South America had the highest coverage and article quality, while regions like Africa and Southeast Asia had significantly lower representation. This reflects a broader digital divide, with wealthier regions enjoying better article coverage and quality due to higher internet access and more active Wikipedia contributors.

## Recommendations for Future Work

To improve representation on Wikipedia, potential strategies include:
- Expanding the analysis to non-English Wikipedias.
- Engaging with underrepresented regions to increase local content contributions.
- Enhancing data collection processes to avoid missing or biased data.


## Results

The analysis reveals several notable findings based on the metrics calculated:

1. **Top 10 Countries by Coverage**: Small nations like Antigua and Barbuda, Federated States of Micronesia, and Marshall Islands ranked highest in articles per capita. This is largely due to their small populations, which inflate the per capita metrics even with relatively few articles.

2. **Bottom 10 Countries by Coverage**: Larger nations such as China, India, and Saudi Arabia had low article coverage per capita, despite their significant populations. This suggests that even though these countries have a large number of articles, they are underrepresented in proportion to their population size.

3. **Top 10 Countries by High-Quality Articles**: Montenegro, Luxembourg, and Albania ranked the highest in terms of high-quality articles per capita. These countries may not have a large number of total articles but excel in producing high-quality content as assessed by ORES.

4. **Bottom 10 Countries by High-Quality Articles**: Countries like China, Antigua and Barbuda, and Barbados had no high-quality articles per capita, indicating areas where further contributions are needed to improve the depth and quality of political coverage.

5. **Geographic Regions by Total Coverage**: Northern Europe and Oceania had the highest articles per capita, indicating stronger political coverage in these regions compared to others.

6. **Geographic Regions by High-Quality Articles**: Regions like Southern and Northern Europe led in high-quality articles per capita, demonstrating a higher concentration of top-quality content, while South and East Asia were among the lowest ranked.

## Research Implications

### Expected Biases

Before conducting the analysis, it was expected that English-speaking countries, such as the U.S. and U.K., would have more Wikipedia articles about politicians, reflecting the bias toward countries with higher internet access and larger English-speaking populations. Wealthier countries or those with greater global political influence were also expected to have more and higher-quality articles compared to regions with less internet penetration.

### Biases Discovered During the Analysis

1. **Geographic Disparities**: The data confirms the anticipated biases, with countries in Western Europe and Oceania leading in terms of both article coverage and quality. Small-population countries like Antigua and Barbuda and Marshall Islands had the highest articles per capita, while Montenegro ranked highest for high-quality articles per capita. Conversely, countries like China, Ghana, and India were among those with the lowest articles per capita, revealing the digital divide between regions with strong internet infrastructure and those without.

2. **Country Name Issues**: Merging datasets posed challenges due to country name mismatches (e.g., "China" vs. "China (Hong Kong SAR)"). These discrepancies affected the data merge process, leading to some countries being excluded from the analysis, such as North and South Korea, which could not be easily combined without introducing new biases.

3. **Small Population Bias**: Countries with small populations, such as Antigua and Barbuda, ranked disproportionately high in the articles per capita metric. Their small populations skewed the results, pushing them to the top despite having relatively few articles.

### Insights on Wikipedia's Data Bias

The results of this analysis reflect Wikipedia’s inherent bias toward countries with greater internet access and active contributor bases. While Wikipedia is open to global contributors, the platform disproportionately represents wealthier nations and regions with stronger digital infrastructures. This imbalance underscores the broader digital divide, affecting access to and creation of information across different parts of the world.

## Conclusion

This project has highlighted several challenges and key takeaways in dealing with large, global datasets like Wikipedia articles on political figures. The biggest lessons learned include:

1. **Data Cleaning and Consistency**: Ensuring that data is cleaned and consistent across different sources is crucial for accurate analysis. The discrepancies in country names, missing population data, and improper formatting directly impacted the accuracy of the per capita metrics. Data cleaning and preprocessing should be thorough to prevent skewed results or biases from being introduced unintentionally.

2. **Impact of Population Size**: The choice of unit measurement (e.g., using millions for population values) significantly affects the final metrics. Small countries with tiny populations can appear artificially inflated in terms of per capita metrics, which can distort the interpretation of the results. Properly handling such units and outliers is key for producing meaningful insights.

3. **Global Digital Disparities**: The analysis confirms the existing digital inequalities, with countries in wealthier regions enjoying better representation and higher-quality articles. Countries with smaller populations or lower internet penetration are underrepresented, emphasizing the need for a more balanced approach to digital content creation.


## References

- Wikipedia API: https://www.mediawiki.org/wiki/API:Main_page
- ORES API Documentation: https://www.mediawiki.org/wiki/ORES
- Population Reference Bureau: United Nations Population Database (August 2024)
- Dr. David W. McDonald's example code, licensed under Creative Commons (CC-BY).
