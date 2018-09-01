# SQL Exercise - Titanic Data

For this exercise, we're going to take a look at the Titanic manifest using SQL. We'll be exploring this data to see what we can learn regarding the survival rates of different groups of people.

**Be careful to do these steps in order!** Doing these steps out of order (especially after creating columns or deleting observations) may lead to unintentional results.

## Step 0: Prework
1. Go to [https://sqliteonline.com/](https://sqliteonline.com/)
2. Once you're on sqliteonline, click "File" in the upper-left hand corner, then "Open DB." Navigate to where you've cloned this repo so that you can open the `titanic.db` sqlite database.
3. Write SQL commands to tackle the problems below, testing them on the table you just uploaded to [https://sqliteonline.com/](https://sqliteonline.com/). Once they work, copy them and any other answers into a text file (with clearly labeled numbers!) that you create in this repository using a text editor of your choice.

## Step 1: Cleaning the data
1. What is the likeliest primary key?
2. Delete all rows where `Embarked` is empty, as we'll assume these individuals did not get on the ship.
3. Fill all empty cabins with **¯\\_(ツ)_/¯**

Note: `NULL` is synonymous in SQL to `NaN` in Pandas.

## Step 2: Feature extraction
1.  There are two columns that pertain to how many family members are on the boat for a given person. Create a new column called `FamilyCount` which will be the sum of those two columns.
2. Create new dummy variables:
  - 2-1. Reverends have a special title in their name, "Rev." Create a column called `IsReverend`: 1 if they're a reverend, 0 if they're not.
  - 2-2. Create 3 columns: `Embarked_C`, `Embarked_Q` and `Embarked_S`. These columns will have 1's and 0's that correspond to the `C`, `Q` and `S` values in the `Embarked` column.
  - 2-3. Create 2 columns: `M` and `F`. Create dummy variables for `Sex`.

## Step 3: Exploratory analysis

For this section, I have provided some assistance with 1 and 2 to help you create a survival rate in SQL:

1. What is the total number of individuals on the ship?

```sql
SELECT COUNT(*) FROM titanic;
```

2-1. What was the survival rate overall?

```sql
SELECT SUM(Survived) / 889 FROM titanic;
```

2-2. Hmm. The answer to 2-1 seems weird. Try this:

```sql
SELECT SUM(Survived) / 889.0 FROM titanic;
```

2-3. What's the difference between dividing by 889 and dividing by 889.0? What do you think is causing this? (Hint: Users of Python 2 might be particularly aware of this issue.)

2-4. Run this command and compare your results to those you got from 2-2.
```sql
SELECT AVG(Survived) FROM titanic;
```

3-1. What was the survival rate of men?

3-2. What was the survival rate of women?

4. What was the survival rate for each `Pclass`?

5. Did any reverends survive? How many?

6. How many unique fares are there?

7. What is the range of fares?

8. Alphabetically, what are the last five names in the passenger manifest among people who are in Pclass 1?

9. What is the survival rate for cabins marked **¯\\_(ツ)_/¯**?

10. What is the survival rate for people whose `Age` is missing?

11. What is the survival rate for each port of embarkation? Answer using a GROUP BY statement.

12. What is the survival rate for children (under 12) in each `Pclass`?

13. Did the captain of the ship survive? Is he on the list?

14. Of all the people that died, who had the most expensive ticket? How much did it cost?
  - Hint: You may want to look into the `ORDER BY` or `MAX()`

15. Does having family on the boat help or hurt your chances of survival?
  - Hint: You could create a dummy variable here.
