# sql-election-analysis
# SQL Election Query Project - India General Elections 2024

## 📌 Project Overview
This SQL-based project provides an analytical view of the **India General Elections 2024** results. The queries help in extracting insights about seat distribution, party-wise performance, candidate rankings, vote breakdowns, and alliance-wise seat share. The dataset includes tables such as **constituencywise_results, partywise_results, statewise_results,** and **constituencywise_details** to facilitate an in-depth analysis.

## 📊 Key Insights & Queries
- **Total Number of Seats:**
  ```sql
  SELECT DISTINCT COUNT(Parliament_Constituency) AS Total_seats
  FROM constituencywise_results;
  ```
- **Total Seats by State:**
  ```sql
  SELECT s.State AS State_Name, COUNT(cr.Constituency_ID) AS Total_Seats
  FROM constituencywise_results cr
  INNER JOIN statewise_results sr ON cr.Parliament_Constituency = sr.Parliament_Constituency
  INNER JOIN states s ON sr.State_ID = s.State_ID
  GROUP BY s.State;
  ```
- **Seats Won by NDA Alliance:**
  ```sql
  SELECT SUM(CASE WHEN party IN ('Bharatiya Janata Party - BJP', 'Telugu Desam - TDP', 'Janata Dal (United) - JD(U)',
                                'Shiv Sena - SHS', 'AJSU Party - AJSUP', 'Apna Dal (Soneylal) - ADAL')
                  THEN [Won] ELSE 0 END) AS NDA_Total_Seats_Won
  FROM partywise_results;
  ```
- **Seats Won by I.N.D.I.A Alliance:**
  ```sql
  SELECT SUM(CASE WHEN party IN ('Indian National Congress - INC', 'Aam Aadmi Party - AAAP', 'All India Trinamool Congress - AITC')
                  THEN [Won] ELSE 0 END) AS INDIA_Total_Seats_Won
  FROM partywise_results;
  ```
- **Top Performing Parties in a State:**
  ```sql
  SELECT pr.Party, COUNT(cr.Constituency_ID) AS Seats_Won
  FROM constituencywise_results cr
  INNER JOIN partywise_results pr ON cr.Party_ID = pr.Party_ID
  INNER JOIN statewise_results sr ON cr.Parliament_Constituency = sr.Parliament_Constituency
  INNER JOIN states s ON sr.State_ID = s.State_ID
  WHERE s.State = 'Andhra Pradesh'
  GROUP BY pr.Party
  ORDER BY Seats_Won DESC;
  ```
- **Winning Candidate Details by State & Constituency:**
  ```sql
  SELECT cr.Winning_Candidate, pr.Party, pr.party_alliance, cr.Total_Votes, cr.Margin, cr.Constituency_Name, s.State
  FROM constituencywise_results cr
  JOIN partywise_results pr ON cr.Party_ID = pr.Party_ID
  JOIN statewise_results sr ON cr.Parliament_Constituency = sr.Parliament_Constituency
  JOIN states s ON sr.State_ID = s.State_ID
  WHERE s.State = 'Gujarat' AND cr.Constituency_Name = 'Bhavnagar';
  ```
- **Top 10 Candidates with Highest EVM Votes:**
  ```sql
  SELECT TOP 10 cr.Constituency_Name, cd.Candidate, cd.EVM_Votes
  FROM constituencywise_details cd
  JOIN constituencywise_results cr ON cd.Constituency_ID = cr.Constituency_ID
  ORDER BY cd.EVM_Votes DESC;
  ```

## 📂 Project Structure
- `SQL Election Project.sql` - Contains all SQL queries for election analysis.
- `Database/` - Information about tables and relationships.
- `README.md` - Project documentation.
- `SQL Election Query` - SQL documentation.

## 🚀 How to Use
1. **Clone the repository:**
   ```bash
    https://github.com/deepa115/sql-election-analysis.git
   ```
2. **Run the SQL Queries:** Execute the queries in an Microsoft SQL environment with the election dataset.
3. **Analyze Results:** Extract insights on election results, party performance, and candidate details.

## 📌 Requirements
- Microsoft SQL Server
- Access to the `India General Elections 2024` dataset

## 📧 Contact
For any queries, feel free to reach out:
- **Email:** deepapalani10@gmail.com
- **GitHub:** [deepa115](https://github.com/deepa115)

---
### 🚀 Gain Election Insights with SQL! 🗳️📊

