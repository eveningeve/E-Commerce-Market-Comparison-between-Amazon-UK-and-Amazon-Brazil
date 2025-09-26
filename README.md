# 01 Project Overview

Understanding online shoppers' spending habits, along with regional  differences in consumer behavior on Amazon can help businesses optimize their marketing and product strategies for specific markets. This comparison between the UK and Brazil offers valuable insights for companies aiming to expand globally and tailor their approaches to maximize sales. This project analyzes and compares the e-commerce markets of Amazon UK and Amazon Brazil, focusing on product categories, pricing structures, sales performance, and customer engagement. The goal is to uncover key differences in market dynamics and provide insights into how cultural, economic, and regional factors influence online retail.

# 02 Business Goal
This project aims to compare consumer buying patterns on Amazon UK and Amazon Brazil, providing insights into how regional market conditions influence e-commerce activity. The following tasks will be performed on both datasets:
* Identify differences in consumer preferences
  * Segment customers based on purchasing patterns and interests 
* Track pricing trends & Adjust real-time pricing
  * Collect and analyze historical pricing data using time series analysis to detect trends, seasonality, and price fluctuations across different product categories
  * Explore the relationship between pricing and customer reviews
  * Implement dynamic pricing algorithms that adjust prices based on demand, competition, and customer behavior
* Develop insights into consumer purchasing behavior 
  * Identify which niches are the easiest to make sales in
  * Build a predictive model to forecast customer churn based on purchasing behaviors

# 03 Dataset
1. The first dataset（https://www.kaggle.com/datasets/asaniczka/amazon-uk-products-dataset-2023）, Amazon UK, has 2.2 million Amazon products. It includes titles of the products, number of reviews, ratings, prices, and sales data from October 2023. The dataset includes product titles, image URLs, product URLs, star ratings, reviews, prices, bestseller status, recent purchase activity, and product category.
2. The second dataset （https://www.kaggle.com/datasets/asaniczka/amazon-brazil-products-2023-1-3m-products）, Amazon Brazil, offers a comprehensive view of the products available on Amazon with over 1.3 million unique products. Collected through a web scraping process in 2023 by Asaniczka, this dataset also includes product titles, pricing, ratings, and more.

# 04 Methodology

* Data Cleaning & Preprocessing: 
  * Translation (Reference): From the reduced Brazil dataset, the columns containing Portuguese text, such as title and categoryName, were translated into English using the Google Cloud Translation API. This process took approximately 4-5 hours. Initially, we attempted to use the unofficial googletrans==4.0.0-rc1 library for translation, but it frequently failed and took too long for large-scale translation tasks. Therefore, we switched to the official Google Cloud Translation API. We obtained the API key from the Google Cloud Platform (GCP) website and used it in Colab.
  * Currency Conversion: The price column in the Brazil dataset was in Brazil Real, and the price column in the UK dataset was in British Pound Sterling. We converted both into U.S. dollars based on the exchange rate on September 27, 2024: 1 Brazil Real = 0.18 USD, and 1 Pound Sterling = 1.34 USD.
  * Removal of Unnecessary Columns: We removed the imgUrl, listPrice, and boughtInLastMonth columns. The boughtInLastMonth column was removed because it wasn’t clear what timeframe "LastMonth" referred to. The listPrice column was removed as its meaning was unclear. The imgUrl column was deleted because it contained too many erroneous URLs.
  * Handling Missing Values While there were no NaN values in either the Brazilian or UK datasets, both contained rows with zero values in the reviews and stars columns. Since analyzing less popular products might still be useful, we decided to leave these values as they were. However, the Brazilian dataset had 19,664 rows with a price value of 0. After investigating, we found that these items were likely not currently for sale, so we deleted these rows as they were not relevant to the analysis.

* Exploratory Data Analysis (EDA):
  * Consumer Preference Analysis
  * Price and Consumer Review Analysis
* Comparative Analysis:
  * Cross-National ASIN Analysis (Analysis of differences in the same products between countries using ASIN)
  * Product Category Analysis
  * Google Trends Analysis
  * Consumer Demand Clustering Analysis
  * Dynamic Pricing
  * Ratings Analysis
  * Discount Rate Analysis
  * Price Range Analysis
  * Key Variables and Product Categories for Predicting 'Bought Last Month'

# 05 Key Findings

First, regarding star ratings and the number of reviews, both markets show a clustering of ratings between 4.0 and 5.0, with more reviews generally associated with higher ratings. However, it’s important to note that this relationship is not strictly linear, meaning that while higher-rated products tend to have more reviews, the number of reviews may not necessarily correlate directly with sales volume. Sellers should, therefore, strategically focus on managing star ratings while encouraging reviews to maximize their impact.

Looking at the relationship between price and reviews, the analysis reveals that initially, higher-priced products tend to have fewer reviews. After a certain point, however, an increase in reviews does not lead to significant price changes, indicating a nonlinear pattern. This is particularly important for sellers of high-priced items. In the UK, lower-priced alternatives are more abundant, leading to fewer reviews for expensive products. Meanwhile, in Brazil, higher-priced items tend to attract more reviews, suggesting that Brazilian consumers may place more emphasis on reviews when purchasing premium products, possibly due to limited access to such items or cultural differences in review behavior.

From a category pricing strategy perspective, the demand for premium products such as electronics is stronger in Brazil. In contrast, the UK shows higher average prices in categories like sports, outdoor, and DIY, indicating an opportunity to expand premium offerings in these areas. In Brazil, it may be effective to focus initially on value-for-money products and gradually introduce premium products as the market matures.

Products in Cluster 2, characterized by low prices and high demand, present a significant opportunity, particularly in Brazil. These products can handle price increases of up to 15% without a significant decrease in demand, providing a chance for sellers to maximize profitability through moderate price hikes. Brazilian consumers, particularly in categories like electronics, tend to be less price-sensitive due to factors such as brand loyalty or product necessity, allowing for higher price flexibility in these premium categories.

**In conclusion, when developing a sales strategy for Amazon in Brazil and the UK, sellers should focus on driving interest in premium products in Brazil while initially prioritizing value-driven offerings. In the UK, expanding premium product ranges in categories like sports, outdoor, and DIY could prove beneficial. By understanding the price sensitivity and review behavior in each market, sellers can develop localized strategies to maximize profitability.**

# 06 Tools & Technologies
* Python (Pandas, NumPy, Matplotlib, Seaborn)
* Jupyter/Colab Notebook

# 07 Challenges
1. Since the dataset lacks sales information, we cannot directly determine the popularity of the products. Therefore, we have opted to use the number of reviews as a proxy for measuring popularity.
2. For the comparison of best-sellers in the price range analysis, we could not directly compare items within the same category due to variations in wording in different languages. To address this, we mapped similar names, such as 'baby' and 'babies,' together to facilitate the comparison.
3. Due to the dataset's large size, Google Colab has repeatedly crashed when attempting to process certain tasks. As a result, we've had to switch to a more robust platform to generate the necessary outputs. This was particularly effective when we worked on developing the recommendation system based on product similarity, where Spyder allowed us to execute the process smoothly without interruptions.

All the contributors to this project: Shuomeng Guan (me), Donghyeon Na, Wei-An Huang, Hui Gao, Courtney Vincent, Aashrith Reddy
