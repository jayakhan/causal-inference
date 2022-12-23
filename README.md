# Causal Inference Project
Determining the impact of `super host` label on the revenue generation of Airbnb 

**Target Industry:** Travel and Hospitability

## Abstract
Our hypothesis is, that hosts who have the `super host` label awarded by Airbnb, can generate
more annual revenue than `regular hosts` with similar characteristics but without the super host
label, because customers elect to stay in their properties more frequently. [InsideAirbnb.com](http://insideairbnb.com/get-the-data.html) makes some of Airbnb data available publicly, which makes it accessible to thorough data science analysis (Airbnb 2022a).

## Project Development Plan 
Project is developed in four parts:

### 1. Data Selection
Since California and Florida are the two highest ranking states for Airbnb revenue generation in the USA, Los Angeles, California and Broward County, Florida were chosen for the study.

![Alt text](30_results/LA_County.png?raw=true "Los Angeles, California")
![Alt text](30_results/Broward_Map.png?raw=true "Broward County, Florida")

### 2. Data Cleaning
Once our data collection was complete, we went on to data processing and data wrangling. First, we excluded the columns that we assume to have no impacts on our response of interest – estimated annual revenue per listing – logically (e.g., addresses of listings, host name, description). Second, we decided to drop all columns that had duplicate information (e.g., one of ‘bathrooms’ and ‘bathroom_text’). Third, we decided to drop the columns with the most missing data and to impute the rows with few missing data. To estimate annual revenue, we multiplied the price of the listing with reviews in the last 12 months because only 67% of travellers leave a review after their stay (Zervas, Proserpio, and Byers 2017).

`estimated annual revenue = price of listing * number of reviews in the last 12 months * 100/67`

### 3. Matching (Creating Treatment and Control Groups)
To be able to analyse what influence the `super host` label has on the estimated annual revenue per listing, we needed to match all other factors that might influence revenue (e.g., location, size of property, star-rating) between the regular hosts and super hosts as closely as possible. To do this, we decided to use DAME-FLAME. This is to ensure we do not have any bias estimate when estmating the actual difference in revenue generation between control (regular hosts) and treatment (super host) groups.

### The prediction error increases markedly between the 3rd and 4th iteration.

![Alt text](30_results/visualization_50.png?raw=true "Matching with 50 iterations")
![Alt text](30_results/visualization_10.png?raw=true "Matching with 10 iterations")

### 4. Regression
Our regressions were based on the matched dataset provided by DAME-FLAME output. We first ran a regression that included our response variable grouped by host status and all predictors (except the one used in revenue calculation that was part of our analysis after data cleaning). Assessment of this model violated the assumption of linearity and normality with a Q-Q-plot that suggested an exponential distribution (Figure 1.3), which led us to run a second regression on log-transformed data. This second regression satisfied the assumptions for linear regressions (Figure 1.4), and we proceeded to use it four our statistical analysis.

### The shape of the second QQ plot suggests that a log transformation of the data could improve model performance down the line.
![Alt text](30_results/qq_before_log.png?raw=true "On Original Response Variable")
![Alt text](30_results/Q-Q-Plot_post_log.png?raw=true "On Log Transformed Response Variable")

## Results
![Alt text](30_results/Regression.JPG?raw=true "Regression Results")

### Average Treatment Effect
The average difference in annual revenue between listings by hosts who we observe as super hosts and listings by hosts who we observe as regular hosts in a world whether neither is a super host is $3,127.

![Alt text](30_results/ate_zoomed_in.png?raw=true "Difference in Revenue Generation")

To explore which other variables might be relevant for revenue generation of an Airbnb listing, we generated a plot that visualizes both error bars and confidence intervals.

Below table shows statistical significance of super host variable which is way above the ‘0’ level boundary and have negligible error bands.

![Alt text](30_results/error_bands.png?raw=true "Confidence Interval and Error Bands")

## References

[1] Airbnb. (2015). "Airbnb Summer Travel Report 2015." Retrieved 04/03/2022, from
https://blog.atairbnb.com/wp-content/uploads/2015/09/Airbnb-Summer-Travel-Report-1.pdf.Airbnb. (2022). "Get the Data." Retrieved 04/03/2022, from http://insideairbnb.com/get-the-data.html.

[2] Airbnb. (2022). "Superhost: Recognizing the best in hospitality." Retrieved 04/03/2022, from https://www.airbnb.com/d/superhost.

[3] Chattopadhyay, M. and S. K. Mitra (2020). "What Airbnb Host Listings Influence Peer-to-Peer Tourist Accommodation Price?" Journal of Hospitality & Tourism Research44(4): 597-623.

[4] Deboosere, R., D. J. Kerrigan, D. Wachsmuth and A. El-Geneidy (2019). "Location, location and professionalization: a multilevel hedonic analysis of Airbnb listing prices and revenue." Regional Studies, Regional Science6(1): 143-156.

[5] Dogru, T., M. Mody, C. Suess, N. Line and M. Bonn (2020). "Airbnb 2.0: Is it a sharing economy platform or a lodging corporation?" Tourism Management78: 104049.

[6] Kwok, L. and K. L. Xie (2019). "Pricing strategies on Airbnb: Are multi-unit hosts revenue pros?" International Journal of Hospitality Management82: 252-259.

[7] Lane, J. and R. M. Woodworth (2016). "The sharing economy checks in: An analysis of Airbnb in the United States." CBRE Hotel’s Americas Research.

[8] Lewis, T. (2020). "Airbnb Statistics (Growth, Revenue, Hosts + More!)." Retrieved 04/03/2022, from 8 https://hostsorter.com/airbnb-statistics/.Management, i. (2022). "Airbnb Statistics." from https:/ ipropertymanagement.com/research/airbnb-statistics.

[9] Poppick, S. (2015). "Airbnb Says Renting Your Place Is Like Getting a Big Raise." Retrieved 04/03/2022, from https://money.com/airbnb-raise-income-report/.Xie, K., C. Y. Heo and Z. E. Mao (2021). "Do professional hosts matter? Evidence from multi-listing and full-time hosts in Airbnb." Journal of Hospitality and Tourism Management47: 413-421.

[10] Xie, K.and Z. Mao (2019). "Locational strategy of professional hosts: Effect on perceived quality and revenue performance of Airbnb listings." Journal of Hospitality & Tourism Research43(6): 919-929.

[11] Zervas, G., D. Proserpio and J. W. Byers (2017). "The Rise ofthe Sharing Economy: Estimating the Impact of Airbnb on the Hotel Industry." Journal of Marketing Research54(5): 687-705.