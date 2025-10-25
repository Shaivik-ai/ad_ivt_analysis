Ad Traffic IVT Analysis

Objective

This project analyzes data from six mobile apps (3 "Valid," 3 "Invalid") to identify the key data patterns and metrics that cause traffic to be flagged as Invalid Traffic (IVT).

The analysis was conducted in the ivt_analysis.ipynb notebook.

Key Findings

The analysis successfully identified clear, persistent indicators that separate valid traffic from IVT. The primary drivers are metrics related to device spoofing and datacenter/proxy traffic.

Finding #1: IVT Apps Show Dramatically Higher Risk Ratios

The boxplots show that, on average, the apps flagged for IVT have significantly higher and more erratic ratios for idfa_ua_ratio and idfa_ip_ratio.

Device Spoofing (idfa_ua_ratio): Valid apps have a ratio very close to 1, meaning each device has its own unique user agent. IVT apps show a much wider and higher distribution, indicating many "devices" are spoofing the same user agent.

Proxy Traffic (idfa_ip_ratio): Valid apps also have a ratio close to 1, meaning one device per IP. IVT apps show a high ratio, indicating that many unique "devices" are originating from the same IP address—a classic sign of a datacenter or proxy server.

Finding #2: IVT Is a Persistent Pattern, Not a One-Time Event

The time-series analysis confirms that this behavior is not an isolated incident.

The "No IVT" apps remain flat and stable over time, exhibiting healthy, low-risk metrics.

The "IVT" apps consistently demonstrate high-risk, high-velocity idfa_ua_ratio and idfa_ip_ratio metrics from the beginning of the data. This shows the IVT flagging was a result of a persistent, fraudulent traffic pattern rather than a temporary data anomaly.

Conclusion

The "why" behind the IVT flagging is clear:

The "Invalid" apps were flagged because their traffic exhibited classic signs of non-human activity, specifically device spoofing (high idfa_ua_ratio) and traffic originating from datacenters/proxies (high idfa_ip_ratio). The valid apps showed no such behavior.