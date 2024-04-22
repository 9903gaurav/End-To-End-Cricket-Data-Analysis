# T20 World Cup Analysis

This project involves an end-to-end data analytics and data engineering effort for T20 World Cup team selection. The main goals are to ensure a minimum average of 180 runs per match and the ability to defend against 150 runs. The project uses AWS infrastructure, including Selenium on EC2 for web scraping from ESPN, AWS Glue for ETL processes, Redshift for data warehousing, and a Power BI dashboard for insights.

[Demo Link](https://app.powerbi.com/links/o_FLHQIpI0?ctid=d1f14348-f1b5-4a09-ac99-7ebf213cbc81&pbi_source=linkShare)

## Web Scraping

### Prerequisites

- Python 3.x
- Selenium library
- Re module
- CSV library
- Chrome Web Driver
- boto3
- io

This code runs on an AWS EC2 instance (OS: Linux) using Selenium to interact with ESPNcricinfo for match and player data extraction.

Generated JSON files in `s3/staged/` include:
- `staged_match_bowling_summary.json`: Bowling statistics for each match.
- `staged_match_batting_summary.json`: Batting statistics for each match.
- `staged_match_summary.json`: Match Summary.
- `staged_players.json`: Player data.

### Limitations

The code is tailored for a specific ESPNcricinfo URL and may not handle website structure changes.

## ETL / Pre-Processing

### Prerequisites

- Python 3.x
- AWS account

ETL processes in AWS Glue include:
1. Extract & Transform:
   - Fetch data from S3, process, and save as `.parquet` in `s3/output_staged`.
2. Loading Data Into Redshift:
   - Fetch database schema from Redshift.
   - Load parquet data into Redshift.

## Power BI

### Team Selection Criteria

Overview:
- Average 180 runs per match.
- Defend against 150 runs per match.

Criteria:
1. **Opener (2 Players, 1 Left-Handed, 1 Right-Handed)**
   - Batting Average: > 30
   - Strike Rate: > 140
   - Innings Batted: > 3
   - Boundary Percentage: > 50
   - Batting Position: < 4

2. **Middle Order (3 Players)**
   - Batting Average: > 40
   - Strike Rate: > 125
   - Innings Batted: > 3
   - Average Balls Faced: > 20
   - Batting Position: > 2

3. **Finisher / Lower Order (2 Players)**
   - Batting Average: > 25
   - Strike Rate: > 130
   - Innings Batted: > 3
   - Average Balls: > 12
   - Batting Position: > 4
   - Innings Bowled: > 1

4. **All-Rounders / Lower Order**
   - Batting Average: > 15
   - Strike Rate: > 140
   - Innings Batted: > 2
   - Batting Position: > 4
   - Innings Bowled: > 2
   - Bowling Economy: < 7
   - Bowling Strike Rate: < 20

This analysis aims to optimize team selection for success in the T20 World Cup.
