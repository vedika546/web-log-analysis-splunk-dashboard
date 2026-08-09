# Web Log Analysis & Threat Monitoring Dashboard using Splunk

## Overview

This project demonstrates hands-on web log analysis and security monitoring using Splunk. Apache web server logs were ingested into Splunk and analyzed using SPL queries to understand web traffic patterns, HTTP response behavior, client IP activity, requested URIs, and geographic distribution of web traffic.

The project focuses on building a SOC-style monitoring dashboard that provides a quick overview of web activity and helps identify unusual traffic patterns and potentially suspicious client activity.

## Objectives

* Analyze Apache web server logs using Splunk.
* Monitor overall web request activity.
* Analyze successful HTTP responses and client/server errors.
* Identify frequently requested URIs.
* Analyze web activity by client IP address.
* Visualize geographic distribution of client traffic.
* Build an interactive Splunk dashboard using a shared time-range filter.

## Lab Setup

### Tools & Technologies

* Splunk
* SPL (Search Processing Language)
* Apache Web Logs
* JSON log data
* Splunk Dashboard
* IP Geolocation

## Dashboard Components

### 1. Web Activity

The dashboard provides a quick summary of web activity through:

* Total Web Requests
* Successful Responses
* Client Errors (4xx)
* Server Errors (5xx)

Example SPL:

```spl
source="apache_mixed_access_full (1).json" host="webserver" sourcetype="_json"
| stats count AS "Total Web Requests"
```

### 2. Web Statistics

The dashboard analyzes:

* Top Requested URIs
* Top Users by IP Address

Example SPL:

```spl
source="apache_mixed_access_full (1).json" host="webserver" sourcetype="_json"
| stats count AS "Hits" by uri
```

Client IP analysis:

```spl
source="apache_mixed_access_full (1).json" host="webserver" sourcetype="_json"
| stats count AS IP by ip
```

### 3. Geographic Web Traffic Analysis

Client IP addresses were enriched using Splunk's `iplocation` command and visualized geographically.

```spl
source="apache_mixed_access_full (1).json" host="webserver" sourcetype="_json" method=GET
| table ip
| iplocation ip
| stats count by Country
| geom geo_countries featureIdField="Country"
```

## Dashboard Features

* Interactive time-range selection
* Single-value security metrics
* URI activity visualization
* Client IP activity visualization
* Geographic traffic visualization
* HTTP response analysis

## Key Observations

The completed dashboard provided visibility into:

* Overall web request volume
* Successful HTTP requests
* Client-side error activity
* Server-side error activity
* Frequently accessed web resources
* High-volume client IP addresses
* Geographic distribution of web traffic

The dashboard captured 2,000 total web requests in the analyzed dataset, with 1,168 successful responses and visible error activity.

## Security Relevance

This project demonstrates practical SOC L1 skills including:

* Log ingestion and analysis
* SPL query writing
* Web traffic monitoring
* HTTP status-code analysis
* IP-based investigation
* Basic threat-hunting workflow
* Dashboard creation
* Security event visualization

The dashboard can be used as a starting point for investigating suspicious IP activity, unusual request patterns, excessive errors, and potentially malicious web traffic.

## Project Structure

```text
web-log-analysis-splunk-dashboard/
│
├── README.md
│
├── screenshots/
│   ├── dashboard-overview.png
│   ├── web-statistics.png
│   └── geographic-traffic.png
│
└── spl-queries/
    └── web-log-analysis.spl
```

## Disclaimer

This project was created for educational and cybersecurity lab purposes using sample Apache web log data. No production or confidential logs are included.


`Splunk` `SPL` `Log Analysis` `Web Traffic Analysis` `HTTP Monitoring` `IP Analysis` `Threat Hunting` `Security Monitoring` `Dashboard Development`
