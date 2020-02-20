Table: Person - PersonId is the primary key column for this table.
| Column Name | Type    |
| ------------- | ------------- |
| PersonId    | int     |
| FirstName   | varchar |
| LastName    | varchar |

Table: Address - AddressId is the primary key column for this table.
| Column Name | Type    |
| ------------- | ------------- |
| AddressId   | int     |
| PersonId    | int     |
| City        | varchar |
| State       | varchar |

Write a SQL query for a report that provides the following information for each person in the Person table, 
**regardless if there is an address for each of those people**:
```
FirstName, LastName, City, State 
```
---
### My Answer:
```
SELECT Person.FirstName, Person.LastName, Address.City, Address.State
FROM   Person JOIN Address
ON     Person.PersonId = Address.PersonId
```
Wrong!

Testcase:
```
{"headers": {"Person": ["PersonId", "LastName", "FirstName"], 
"Address": ["AddressId", "PersonId", "City", "State"]}, 
"rows": {"Person": [[1, "Wang", "Allen"]], "Address": [[1, 2, "New York City", "New York"]]}}

Output is EMPTY! []
```
---
### Solution:
```
select FirstName, LastName, City, State
from   Person left join Address
on     Person.PersonId = Address.PersonId
```

Expected output:
```
{"headers": ["FirstName", "LastName", "City", "State"], "values": [["Allen", "Wang", null, null]]}
```
Person 可能没有对应的Address => 要用**left join**
