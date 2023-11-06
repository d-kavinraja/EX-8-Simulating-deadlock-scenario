# EX 8: Simulating deadlock scenario
## Date: 22.9.2023
## AIM: 
To simulate a scenario of deadlock in concurrent execution of transactions.
## PROCEDURE:
1. Create a accounts table with the schema Accounts (account_id INT PRIMARY KEY,balance DECIMAL(10, 2))
2. Insert the values in the accounts table
3. Cteate a transaction T1 and T2
4. T1 updates the balance by debiting 200
5. Simulate a delay and make T2 inteferes T1
6. T2 updates balance by debiting 150
7. Simulate a delay and make T1 inteferes T2
## QUERY
```sql
-- Creating Accounts table
CREATE TABLE Accounts (account_id INT PRIMARY KEY,balance DECIMAL(10, 2));
-- Inserting sample account data
INSERT INTO Accounts VALUES(1, 1000.00);
INSERT INTO Accounts VALUES(2, 2500.00);
```
## OUTPUT
![image](https://github.com/dineshgl/EX-8-Simulating-deadlock-scenario/assets/143793356/2f35d3f2-474d-4366-ade6-d0a151da1d2c)

## Now, let's set up the two transactions T1 and T2:
## Transaction T1
```sql
BEGIN TRANSACTION;
UPDATE Accounts
SET balance = balance - 200.00
WHERE account_id = 1;
-- Simulate a delay to ensure T2 interferes
WAITFOR DELAY '00:00:10'; -- This line introduces a delay
UPDATE Accounts
SET balance = balance + 200.00
WHERE account_id = 2;
COMMIT;
```
## Transaction T2
```sql
BEGIN TRANSACTION;
UPDATE Accounts
SET balance = balance - 150.00
WHERE account_id = 2;
-- Simulate a delay to ensure T1 interferes
WAITFOR DELAY '00:00:10'; -- This line introduces a delay
UPDATE Accounts
SET balance = balance + 150.00
WHERE account_id = 1;
COMMIT;
```
## OUTPUT:
```sql
Msg 1205, Level 13, State 51, Line 3
Transaction (Process ID) was deadlocked
on resourceswith anotherprocess and has been
chosen as the deadlock victim. Rerun the transaction.
```
## RESULT:
Thus the program for the simulation of deadlock has been executed successfully.
