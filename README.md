# Grouping-Data--SQL


                     II. SELECTING AND GROUPING DATA.
CREATE THE FOLLOWING TABLE

TABLE NAME: dbo.BBall_Stats
COLUMNS : PlayerID (int, null)
PlayerName (varchar(50), null)
PlayerNum (int, null)
PlayerPosition (varchar(50), null)
Assist (int, null)
Rebounds (int, null)
GamesPlayed (int, null)
Points (int, null)
PlayersCoach (varchar(50), null) */

CREATE TABLE dbo.BBall_Stats
(
PlayerID int null,
PlayerName varchar(50) null,
PlayerNumber int null,
PlayerPosition varchar(50) null,
Assist int null,
Rebounds int null,
GamesPlayed int null,
Points int null,
PlayerCoach varchar(50) null
)

/*2. RUN THE FOLLOWING SCRIPTS.

INSERT INTO BBALL_STATS(PLAYERID, PLAYERNAME,PLAYERNUMBER,PLAYERPOSITION,ASSIST,
REBOUNDS,GAMESPLAYED,POINTS,PLAYERCOACH)
select 1,'ali',20,'guard',125,80,10,60,'thompson' union
select 2,'james',22,'forward',65,100,10,65,'garret' union
SELECT 3,'ralph',24, 'center',30 ,120,9,70,'samson' union
SELECT 4,'terry',30,'guard',145,90,9,75,'garret' union
SELECT 5,'dirk',32,'forward',70,110,10,80,'thompson'union
SELECT 6,'alex',34,'center',35 ,130,10,90,'garret' union
SELECT 7,'nina',40,'guard',155 ,100,9,100 ,' samson'union
SELECT 8,'krystal',42,'forward',75,100,9,95,'thompson' union
SELECT 9,'bud',44, 'center',40,125,10,90,'thompson' union
SELECT 10,'tiger',50, 'guard',160,90,10,85,'samson' union
SELECT 11,'troy',52, 'forward',80,125,10,80,'samson' union
SELECT 12,'anand',54, 'center',50,145,10,110,'samson' union
SELECT 13,'kishan',60, 'guard',120,150,9,115,'samson' union
SELECT 14,'spock',62, 'forward',85,105,8,120,'thompson' union
SELECT 15,'cory',64, 'center',55,175,10,135,'samson' */

INSERT INTO BBALL_STATS(PLAYERID, PLAYERNAME,PLAYERNUMBER,PLAYERPOSITION,
ASSIST,REBOUNDS,GAMESPLAYED,POINTS,PLAYERCOACH)
SELECT 1,'Ali',20,'Guard',125,80,10,60,'Thompson'
UNION
SELECT 2,'James',22,'Forward',65,100,10,65,'Garret'
UNION
SELECT 3,'Ralph',24, 'Center',30 ,120,9,70,'Samson'
UNION
SELECT 4,'Terry',30,'Guard',145,90,9,75,'Garret'
UNION
SELECT 5,'Dirk',32,'Forward',70,110,10,80,'Thompson'
UNION
SELECT 6,'Alex',34,'Center',35 ,130,10,90,'Garret'
UNION
SELECT 7,'Nina',40,'Guard',155 ,100,9,100 ,'Samson'
UNION
SELECT 8,'Krystal',42,'Forward',75,100,9,95,'Thompson'
UNION
SELECT 9,'Bud',44, 'Center',40,125,10,90,'Thompson'
UNION
SELECT 10,'Tiger',50, 'Guard',160,90,10,85,'Samson'
UNION
SELECT 11,'Troy',52, 'Forward',80,125,10,80,'Samson'
UNION
SELECT 12,'Anand',54, 'Center',50,145,10,110,'Samson'
UNION
SELECT 13,'Kishan',60, 'Guard',120,150,9,115,'Samson'
UNION
SELECT 14,'Spock',62, 'Forward',85,105,8,120,'Thompson'
UNION
SELECT 15,'Cory',64, 'Center',55,175,10,135,'Samson'

/*
3. ANSWER THE BELOW QUESTIONS.

a. Find the Number of Players at each Position
b. Find the Number of Players assigned to each Coach
c. Find the Most Points scored per game by Position
d. Find the Number of Rebounds per game by Coach
e. Find the Average number of Assist by Coach
f. Find the Average number of Assist per game by Position
g. Find the Total number of Points by each Player Position.

3.A Find the Number of Players at each Position */

SELECT PLAYERPOSITION, COUNT(PlayerName) AS [NUMBER OF PLAYERS]
FROM BBALL_STATS
GROUP BY PLAYERPOSITION

/*
3.B Find the Number of Players assigned to each Coach*/

SELECT PLAYERCOACH, COUNT(PLAYERNAME) AS [NUMBER OF PLAYERS]
FROM BBALL_STATS
GROUP BY PLAYERCOACH

/*
3.C Find the Most Points scored per game by Position*/

SELECT PLAYERPOSITION, MAX(POINTS/GAMESPLAYED) AS [MAX POINT PER GAME]
FROM [dbo].[BBall_Stats]
GROUP BY PLAYERPOSITION
ORDER BY 2 DESC

/*
3.D Find the Number of Rebounds per game by Coach*/

SELECT PLAYERCOACH, SUM(REBOUNDS)/SUM(GamesPlayed) AS [REBOUND PER GAME]
FROM [dbo].[BBall_Stats]
GROUP BY PLAYERCOACH
ORDER BY 2 DESC

/*
3.E Find the Average number of Assist by Coach*/

SELECT PLAYERCOACH, AVG(ASSIST) AS [AVERAGE ASSIST]
FROM [dbo].[BBall_Stats]
GROUP BY PLAYERCOACH

/*
3.F Find the Average number of Assist per game by Position*/

SELECT PLAYERPOSITION, AVG(ASSIST/GamesPlayed) AS [ASSIST PER GAME]
FROM [dbo].[BBall_Stats]
GROUP BY PLAYERPOSITION

/*
3.G Find the Total number of Points by each Player Position*/

SELECT PLAYERPOSITION, SUM(POINTS) AS [TOTAL POINTS]
FROM [dbo].[BBall_Stats]
GROUP BY PLAYERPOSITION

---USING ADVENTUREWORKS DATABASE.

--Product.Product Table, return the COUNT of all product and the AVERAGE price,GROUPED BY by the product color.
--a.Count By Color
SELECT [Color] ,COUNT(ProductID)as CountByColor,AVG (ListPrice) AS AverageListPrice
FROM [AdventureWorks2017].[Production].[Product]
GROUP BY [Color]

--Sales.SalesOrderHeader:Return Minimum TotalDue and Maximum Total Due grouped by the TerritoryID.

SELECT [TerritoryID], MIN ([TotalDue]) AS MinTotalDue , MAX ([TotalDue]) AS MaxTotalDue
FROM [AdventureWorks2017].[Sales].[SalesOrderHeader]
GROUP BY [TerritoryID]

---Sales.SalesTerritory:Return the Territory Name and Territory Group with the highest sales year-to-date (SalesYTD),excluding the North American Territory Group.

SELECT [Name], [Group],MAX ([SalesYTD]) AS TotalSalesYTD
FROM [AdventureWorks2017].[Sales].[SalesTerritory]
WHERE [Group] != ('North America')
GROUP BY [Name], [Group]
ORDER BY [Group]
