# **Ad Fraud Analysis: IVT Pattern Detection**

## **Project Objective**

The goal of this project is to analyze ad traffic data from six different mobile applications to identify the specific patterns and key metrics that distinguish fraudulent or Invalid Traffic (IVT) from legitimate, valid traffic.

The analysis provides a data-driven answer to the question: **"Why were some apps flagged for IVT while others were not?"**

This analysis was performed as part of an internship assignment for Hunt Digital Media.

## **Data Source**

The dataset was provided in a Google Sheet and contains hourly/daily aggregated traffic metrics for 6 apps (3 valid, 3 invalid).

* **Data:** [Google Sheets Link](https://docs.google.com/spreadsheets/d/1MTnRFZvwCDI1lnrKsQXau-zqcPzDpkg_wsnkP0wkcaA/edit?usp=sharing)  
* **Analysis Notebook:** ivt\_analysis.ipynb

### **Key Metrics Analyzed:**

* idfa\_ip\_ratio: unique\_idfas / unique\_ips. A high ratio suggests many "devices" are coming from a single IP, a strong indicator of a datacenter or proxy.  
* idfa\_ua\_ratio: unique\_idfas / unique\_uas. A high ratio suggests many "devices" are spoofing the same user-agent string, a strong indicator of device spoofing.  
* IVT: The percentage of traffic flagged as invalid.

## **Methodology**

The analysis was conducted in a Jupyter Notebook (ivt\_analysis.ipynb) using the Python data stack.

1. **Data Loading:** The 6 sheets were loaded from the Excel file and combined into a single master pandas DataFrame.  
2. **Data Cleaning:** Timestamps were converted to datetime objects, junk rows (like empty or partial header rows) were dropped, and all numeric columns were converted to numeric types, handling errors and infinite values.  
3. **Analysis & Visualization:** pandas, matplotlib, and seaborn were used to create comparative boxplots and time-series line plots to isolate the differences between the "No IVT" and "IVT" app groups.

## **Analysis & Key Findings**

The analysis reveals clear, statistically significant differences between the two groups of apps. The "Invalid" apps were not flagged by chance; they exhibit classic, persistent signs of non-human bot traffic.

### **Finding 1: IVT Apps Show Extreme "Device Spoofing" & "Proxy" Traffic**

The boxplots compare the overall distribution of key risk metrics between the "No IVT" and "IVT" groups. The difference is not subtle; it's a night-and-day separation.

* **Device Spoofing (idfa\_ua\_ratio):** The "No IVT" apps have a median ratio near 1.0, which is healthy (1 device \= 1 user agent). The "IVT" apps show a median ratio that is exponentially higher, with a massive distribution. This indicates large-scale device spoofing, where one user-agent is being used to fake thousands of different devices.  
* **Proxy Traffic (idfa\_ip\_ratio):** Similarly, the "No IVT" apps have a healthy ratio near 1.0 (1 device \= 1 IP). The "IVT" apps show a dramatically higher ratio, proving that a high volume of "unique" devices are all originating from the same few IP addresses—a classic signature of a bot farm operating from a datacenter.

### **Finding 2: The Fraudulent Traffic is Persistent, Not an Anomaly**

The time-series plot answers the "when" part of the analysis. It shows the average of these key metrics over time for both groups.

* The **"No IVT"** group (blue line) is flat and stable, with ratios staying near 1.0 for the entire period. This is the baseline for healthy traffic.  
* The **"IVT"** group (orange line) *starts* at a high-risk level and *stays* high. This confirms that the behavior is persistent. The apps were flagged not because of a single bad day or a temporary glitch, but because they were consistently sending traffic that was fundamentally fraudulent in nature.

## **Conclusion**

The data provides a definitive answer as to why some apps were flagged for IVT:

**The invalid apps were flagged because they exhibited persistent, high-velocity patterns of non-human traffic, specifically device spoofing (high idfa\_ua\_ratio) and traffic originating from datacenters/proxies (high idfa\_ip\_ratio).**

The valid apps, by contrast, showed stable, healthy, and low-risk metrics throughout the entire observation period.

## **How to Reproduce this Analysis**

1. Clone this repository:

git clone \[https://github.com/YOUR\_USERNAME/YOUR\_REPO\_NAME.git\](https://github.com/YOUR\_USERNAME/YOUR\_REPO\_NAME.git)  
cd YOUR\_REPO\_NAME

2.   
3. Install the required libraries:

pip install \-r requirements.txt

4.   
5. Open the Jupyter Notebook to review the code:

jupyter notebook ivt\_analysis.ipynb

6. 

