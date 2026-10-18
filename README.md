Online Retail RFM Analysis & Customer Segmentation

Customer segmentation of an online retailer using RFM (Recency, Frequency, Monetary) analysis and K-Means clustering in Python, with segment profiles, visualizations and an Excel report.

Overview

RFM analysis groups customers by their buying behaviour:

Recency: how many days ago the customer last purchased
Frequency: how many orders the customer placed
Monetary: how much the customer spent in total

Using these three metrics, the project splits 4,338 customers into four behaviour-based segments so a business can decide whom to reward, nurture or win back.

Business Questions
Which customers generate most of the revenue?
Which customers are at risk of being lost?
How should marketing effort differ across customer groups?
Dataset
Source: Online Retail dataset (UCI Machine Learning Repository), transactions of a UK-based online retailer
Period: 1 Dec 2010 to 9 Dec 2011
Size: 541,909 rows, 8 columns (InvoiceNo, StockCode, Description, Quantity, InvoiceDate, UnitPrice, CustomerID, Country)
Full file (Excel): Download from Google Drive
Methodology
Data quality check and cleaning
Step	Rows affected
Original data	541,909
Removed rows with missing CustomerID (cannot be assigned to a customer)	135,080
Removed rows with Quantity <= 0 or UnitPrice <= 0 (cancellations, returns, price errors)	8,945
Removed exact duplicate rows	5,192
Clean data	392,692 rows, 4,338 customers
Revenue per row = Quantity x UnitPrice. Total clean revenue: about £8.89M.
Exploration: monthly revenue trend and revenue by country (the UK accounts for 82% of revenue).
RFM calculation per customer, using the day after the last transaction (10 Dec 2011) as the reference date. Monetary is the sum of revenue across all of a customer's orders.
Feature preparation: RFM values are highly skewed (Frequency skew 12.1, Monetary skew 19.3), so a log transform is applied before standardization. Without this, a handful of extreme customers dominate the clusters.
K-Means clustering with the elbow method and silhouette score to choose k. k = 4 was chosen for business interpretability (silhouette 0.34; k = 2 scores higher at 0.43 but gives too coarse a split to act on).
Segment profiling and visualization with boxplots.
Excel export of customer-level results, a segment summary and the cleaning log.
Results
Segment	Customers	% of customers	Avg recency (days)	Avg orders	Avg spend (£)	% of revenue
Champions	713	16.4%	12	13.8	8,088	64.9%
Regular Customers	1,166	26.9%	72	4.1	1,802	23.6%
New / Low-Spend	837	19.3%	18	2.2	557	5.2%
Lost / Churned	1,622	37.4%	182	1.3	341	6.2%

Show Image

Show Image Boxplots use a log scale for Frequency and Monetary because of heavy outliers.

Show Image

Key Insights
Revenue is concentrated: the top 20% of customers generate 74.7% of revenue, and the 16.4% of customers in the Champions segment generate 64.9%.
Over a third of customers are lost: the Lost / Churned segment (37.4%) last purchased about 182 days ago on average and contributes only 6.2% of revenue.
Regular Customers are the growth opportunity: they order about 4 times, but their last purchase was around 72 days ago on average.
Business Recommendations
Segment	Suggested action
Champions	Loyalty programme, early access to new products, avoid heavy discounting
Regular Customers	Re-engagement emails and personalised offers before they drift away
New / Low-Spend	Welcome series and second-purchase incentives
Lost / Churned	Low-cost win-back campaign; limit spend on this group
Tech Stack
Python: Pandas, NumPy
Machine learning: Scikit-learn (StandardScaler, KMeans, silhouette score)
Visualization: Matplotlib, Seaborn
Reporting: Excel (openpyxl)
Environment: Google Colab / Jupyter Notebook
Repository Structure
online-retail-rfm-analysis/
├── notebooks/
│   └── project.ipynb          # full analysis with outputs
├── outputs/
│   ├── rfm_segments.xlsx      # customer-level RFM + segment summary + cleaning log
│   ├── rfm_boxplots.png
│   ├── segment_share.png
│   └── elbow_silhouette.png
└── README.md
How to Run
Download the dataset from the link above and save it as Online Retail.xlsx.
Open notebooks/project.ipynb in Google Colab (or Jupyter) and upload the file next to the notebook.
Run all cells in order. Charts and the Excel report are saved in outputs/.
Limitations
About 25% of rows have no CustomerID, so they could not be included in the customer analysis.
The data covers one year of a single retailer, and 82% of revenue comes from the UK. Many customers are wholesalers, which explains the very large spenders.
K-Means results depend on the chosen k and on feature scaling; segment names are interpretations of the cluster profiles.
Author

Aakanksha Singh Sengar: GitHub | LinkedIn
