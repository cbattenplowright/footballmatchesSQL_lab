# Football Matches - Tasks

Each of the questions/tasks below can be answered using a `SELECT` query. When you find a solution copy it into the code block under the question before pushing your solution to GitHub.

1) Find all the matches from 2017.

There were 7810 matches in 2017
```sql
SELECT COUNT (*) FROM matches WHERE season = 2017;


```

2) Find all the matches featuring Barcelona.

There were 608 matches featuring Barcelona
```sql
SELECT COUNT (*) FROM matches WHERE hometeam = 'Barcelona' OR awayteam = 'Barcelona';


```

3) What are the names of the Scottish divisions included?

The names of the Scottish divisions are Scottish Premiership, Scottish Championship and Scottish League One
```sql
SELECT name FROM divisions WHERE country = 'Scotland';

```

4) Find the value of the `code` for the `Bundesliga` division. Use that code to find out how many matches Freiburg have played in that division. HINT: You will need to query both tables

Freiburg played 374 matches.
```sql
--One line solution
SELECT COUNT(*) AS matches_played FROM matches JOIN divisions ON matches.division_code = divisions.code WHERE divisions.name = 'Bundesliga' AND (hometeam = 'Freiburg' OR awayteam = 'Freiburg');

--Two line solution
SELECT code FROM divisions WHERE name = 'Bundesliga';
SELECT COUNT(*) FROM matches WHERE division_code = 'D1' AND (hometeam = 'Freiburg' OR awayteam = 'Freiburg');


```

5) Find the teams which include the word "City" in their name. 
There are 4 teams with the word "City" in their name
```sql
SELECT COUNT(DISTINCT hometeam) FROM matches WHERE LOWER(hometeam) LIKE LOWER('%City%');


```

6) How many different teams have played in matches recorded in a French division?

There were 61 different teams.
```sql
-- One line solution
SELECT COUNT(DISTINCT hometeam) FROM matches JOIN divisions ON matches.division_code = divisions.code WHERE divisions.country = 'France' AND division_code = 'F1' OR division_code = 'F2';

-- Two line solution
SELECT code FROM divisions WHERE country = 'France';
SELECT COUNT(DISTINCT hometeam) FROM matches WHERE division_code = 'F1' OR division_code = 'F2';

```

7) Have Huddersfield played Swansea in any of the recorded matches?

Huddersfield and Swansea have played each other 12 times between 2006 and 2021.
```sql
SELECT COUNT(*) FROM matches WHERE hometeam = 'Huddersfield' AND awayteam = 'Swansea' OR hometeam = 'Swansea' AND awayteam = 'Huddersfield';

```

8) How many draws were there in the `Eredivisie` between 2010 and 2015?

There were 431 draws. 
```sql
SELECT COUNT(ftr) FROM matches JOIN divisions ON matches.division_code = divisions.code WHERE (divisions.name = 'Eredivisie') AND ftr = 'D' AND (season BETWEEN 2010 AND 2015);

```

9) Select the matches played in the Premier League in order of total goals scored from highest to lowest. When two matches have the same total the match with more home goals should come first.

```sql
SELECT * FROM matches JOIN divisions ON matches.division_code = divisions.code WHERE (divisions.name = 'Premier League') ORDER BY (matches.fthg + matches.ftag) DESC, matches.fthg DESC; -- Need the DESC after matches.fthg so matches with more home goals are displayed first

```

10) In which division and which season were the most goals scored?

The division where the most goals 1592 were scored was in the National League and in 2013 
```sql
SELECT divisions.name, season, SUM(fthg+ftag) AS total_goals FROM matches JOIN divisions ON divisions.code = matches.division_code GROUP BY season, divisions.name ORDER BY total_goals DESC;

```

### Useful Resources

- [Filtering results](https://www.w3schools.com/sql/sql_where.asp)
- [Ordering results](https://www.w3schools.com/sql/sql_orderby.asp)
- [Grouping results](https://www.w3schools.com/sql/sql_groupby.asp)