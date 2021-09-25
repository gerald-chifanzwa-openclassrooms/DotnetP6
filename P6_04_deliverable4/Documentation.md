## Stored Procedures Documentation

### Fields

All stored procedures return the same field sets.
The fields are as follows

- *Id* - Int - This is the unique identifier for an issue
- *Product* - String - This is the name of the product to which the issue refers
- *Version* - String - The version of the product to which the issue refers
- *OperatingSystem* - String - Identifies the reported operating system on which the issue occurred
- *DateReported* - DateTime - Gives the date and time on which the issue was reported
- *Status* - String - Shows the current status of the issues. Available values are Resolved/Pending. 
- *ProblemDescription* - String - Gives the reported description of the problem
- *ProblemSolution* - String - If the issue is resolved, this field gives the reported solution to the problem. Otherwise this field will be _null_ for unresolved issues.
- *DateResolved* - DateTime, nullable - If the issue is resolved, this will give the date and time on which the issue was resolved. Otherwise this will be _null_.
- *ResolvedBy* - String - This field gives the name of the user who resolved an issue. This field is nullable as well. If the issue is yet to be resolved, the field will be null. If resolved, it will have the username of the user who resolved the issue. Should the system devleopers choose not to save usernames, this will be null all the time.



## Queries

## 1. Get all outstanding issues (all products)

The stored procedure for this query is called _QueryOutstandingIssuesAllProducts_.
This procedure required no parameters, it will return the issues at the Pending status, ordered by their Created date, in descending order.

### Example: 
- _EXEC QueryOutstandingIssuesAllProducts;_


## 2. Get all outstanding issues for a product (all versions)

### Query name: _QueryOutstandingIssuesByProduct_
### Parameters:
- @ProductId - _Int_ - The unique Id for the product. This can be obtained from getting all products.

### Returns:
Issues belonging to the given product, ordered by their Created Date, in descending order.

### Example:

- _EXEC QueryOutstandingIssuesByProduct 1;_

## 3. Get all outstanding issues for a product (single version)
### Query name: _QueryOutstandingIssuesByProductAndVersion_
### Parameters:
- @ProductId - _Int_ - The unique Id for the product. This can be obtained from getting all products.
- @Version - String/NVARCHAR(50) - Gives the version required

### Returns:
Issues at the Pending status belonging to the given product, at the given version, ordered by their Created Date, in descending order.

### Example:

- _EXEC QueryOutstandingIssuesByProductAndVersion 1, '1.0';_



## 4. Get all outstanding issues within date range for a product (all versions)
### Query name: QueryOutstandingIssuesByProductAndDateRange
### Parameters:
- @ProductId - _Int_ - The unique Id for the product. This can be obtained from getting all products.
- @From - DateTime/DATE - Gives the starting date to filter the results, inclusive.
- @To - DateTime/DATE - Gives the ending date to filter the results, inclusive.

### Returns:
Issues at the Pending status belonging to the given product, created between the From date and the To date, inclusive, ordered by their Created Date, in descending order.

### Example:

- _EXEC QueryOutstandingIssuesByProductAndDateRange					    1, '2021-05-01', '2021-09-25';_



## 5. Get all outstanding issues within date range for a product (single version)
### Query name: QueryOutstandingIssuesByProductVersionAndDateRange
### Parameters:
- @ProductId - _Int_ - The unique Id for the product. 
This can be obtained from getting all products.
- @Version - String/NVARCHAR(50) - Gives the version required
- @From - DateTime/DATE - Gives the starting date to filter the results, inclusive.
- @To - DateTime/DATE - Gives the ending date to filter the results, inclusive.

### Returns:
Issues at the Pending status belonging to the given product at the specified, created between the From date and the To date, inclusive, ordered by their Created Date, in descending order.

### Example
- _EXEC QueryOutstandingIssuesByProductVersionAndDateRange			    1, '1.0', '2021-05-01', '2021-09-25';_


## 6. Get all outstanding issues containing list of keywords (all products)
### Query name: QueryOutstandingIssuesWithKeyWords
### Parameters:
- @KeyWords - _String/NVARCHAR(MAX)_ - A string containing the keywords to use to search, seperated by spaces.

### Returns:
Issues at the Pending status containing the key words specified in the ProblemDescription, created between the From date and the To date, inclusive, ordered by their Created Date, in descending order.

### Example
- _EXEC QueryOutstandingIssuesWithKeyWords								    'TCP matrix';_


## 7. Get all outstanding issues for a product containing list of keywords (all versions)
### Query name: QueryOutstandingIssuesWithKeyWords
### Parameters:
- @ProductId - _Int_ - The unique Id for the product. 
This can be obtained from getting all products.
- @KeyWords - _String/NVARCHAR(MAX)_ - A string containing the keywords to use to search, seperated by spaces.

### Returns:
Issues at the Pending status  belonging to the given product specified containing the key words specified in the ProblemDescription, created between the From date and the To date, inclusive, ordered by their Created Date, in descending order.

### Example
- _EXEC QueryOutstandingIssuesWithKeyWordsForProduct 1,								    'TCP matrix';_


## 8. Get all outstanding issues for a product containing list of keywords (single version)
### Query name: QueryOutstandingIssuesWithKeyWordsForProductAndVersion
### Parameters:
- @ProductId - _Int_ - The unique Id for the product. 
This can be obtained from getting all products.
- @Version - String/NVARCHAR(50) - Gives the version required
- @KeyWords - _String/NVARCHAR(MAX)_ - A string containing the keywords to use to search, seperated by spaces.

### Returns:
Issues at the Pending status  belonging to the given product at the specified version containing the key words specified in the ProblemDescription, ordered by their Created Date, in descending order.

### Example
- _EXEC QueryOutstandingIssuesWithKeyWordsForProductAndVersion 1,								    '1.0', 'TCP matrix';_


## 9. Get all outstanding issues within date range for a product containing list of keywords (all versions)

### Query name: QueryOutstandingIssuesWithKeyWordsForProductAndDateRange
### Parameters:
- @ProductId - _Int_ - The unique Id for the product. 
This can be obtained from getting all products.
- @From - DateTime/DATE - Gives the starting date to filter the results, inclusive.
- @To - DateTime/DATE - Gives the ending date to filter the results, inclusive.
- @KeyWords - _String/NVARCHAR(MAX)_ - A string containing the keywords to use to search, seperated by spaces.

### Returns:
Issues at the Pending status  belonging to the given product containing the key words specified in the ProblemDescription, created between the From date and the To date, inclusive, ordered by their Created Date, in descending order.

### Example
- _EXEC QueryOutstandingIssuesWithKeyWordsForProductAndVersion 1,								    '1.0', 'TCP matrix';_


## 10. Get all outstanding issues within date range for a product containing list of keywords (all versions)

### Query name: QueryOutstandingIssuesWithKeyWordsForProductAndVersionAndDateRange
### Parameters:
- @ProductId - _Int_ - The unique Id for the product. 
This can be obtained from getting all products.
- @Version - String/NVARCHAR(50) - Gives the version required
- @From - DateTime/DATE - Gives the starting date to filter the results, inclusive.
- @To - DateTime/DATE - Gives the ending date to filter the results, inclusive.
- @KeyWords - _String/NVARCHAR(MAX)_ - A string containing the keywords to use to search, seperated by spaces.

### Returns:
Issues at the Pending status  belonging to the given product at the specified version containing the key words specified in the ProblemDescription, created between the From date and the To date, inclusive, ordered by their Created Date, in descending order.

### Example
- _EXEC QueryOutstandingIssuesWithKeyWordsForProductAndVersionAndDateRange 1, '1.2', '2021-01-01', '2021-09-25', 'TCP Matrix';_


## Queries

## 11. Get all resolved issues (all products)

The stored procedure for this query is called _QueryResolvedIssuesAllProducts_.
This procedure required no parameters, it will return the issues at the resolved status, ordered by their Created date, in descending order.

### Example: 
- _EXEC QueryResolvedIssuesAllProducts;_


## 12. Get all resolved issues for a product (all versions)

### Query name: _QueryResolvedIssuesByProduct_
### Parameters:
- @ProductId - _Int_ - The unique Id for the product. This can be obtained from getting all products.

### Returns:
Issues belonging to the given product, ordered by their Created Date, in descending order.

### Example:

- _EXEC QueryResolvedIssuesByProduct 1;_

## 13. Get all resolved issues for a product (single version)
### Query name: _QueryResolvedIssuesByProductAndVersion_
### Parameters:
- @ProductId - _Int_ - The unique Id for the product. This can be obtained from getting all products.
- @Version - String/NVARCHAR(50) - Gives the version required

### Returns:
Issues at the resolved status belonging to the given product, at the given version, ordered by their Created Date, in descending order.

### Example:

- _EXEC QueryResolvedIssuesByProductAndVersion 1, '1.0';_



## 14. Get all resolved issues within date range for a product (all versions)
### Query name: QueryResolvedIssuesByProductAndDateRange
### Parameters:
- @ProductId - _Int_ - The unique Id for the product. This can be obtained from getting all products.
- @From - DateTime/DATE - Gives the starting date to filter the results, inclusive.
- @To - DateTime/DATE - Gives the ending date to filter the results, inclusive.

### Returns:
Issues at the resolved status belonging to the given product, created between the From date and the To date, inclusive, ordered by their Created Date, in descending order.

### Example:

- _EXEC QueryResolvedIssuesByProductAndDateRange					    1, '2021-05-01', '2021-09-25';_



## 15. Get all resolved issues within date range for a product (single version)
### Query name: QueryResolvedIssuesByProductVersionAndDateRange
### Parameters:
- @ProductId - _Int_ - The unique Id for the product. 
This can be obtained from getting all products.
- @Version - String/NVARCHAR(50) - Gives the version required
- @From - DateTime/DATE - Gives the starting date to filter the results, inclusive.
- @To - DateTime/DATE - Gives the ending date to filter the results, inclusive.

### Returns:
Issues at the resolved status belonging to the given product at the specified, created between the From date and the To date, inclusive, ordered by their Created Date, in descending order.

### Example
- _EXEC QueryResolvedIssuesByProductVersionAndDateRange			    1, '1.0', '2021-05-01', '2021-09-25';_


## 16. Get all resolved issues containing list of keywords (all products)
### Query name: QueryResolvedIssuesWithKeyWords
### Parameters:
- @KeyWords - _String/NVARCHAR(MAX)_ - A string containing the keywords to use to search, seperated by spaces.

### Returns:
Issues at the resolved status containing the key words specified in the ProblemDescription, created between the From date and the To date, inclusive, ordered by their Created Date, in descending order.

### Example
- _EXEC QueryResolvedIssuesWithKeyWords								    'TCP matrix';_


## 17. Get all resolved issues for a product containing list of keywords (all versions)
### Query name: QueryResolvedIssuesWithKeyWords
### Parameters:
- @ProductId - _Int_ - The unique Id for the product. 
This can be obtained from getting all products.
- @KeyWords - _String/NVARCHAR(MAX)_ - A string containing the keywords to use to search, seperated by spaces.

### Returns:
Issues at the resolved status  belonging to the given product specified containing the key words specified in the ProblemDescription, created between the From date and the To date, inclusive, ordered by their Created Date, in descending order.

### Example
- _EXEC QueryResolvedIssuesWithKeyWordsForProduct 1,								    'TCP matrix';_


## 18. Get all resolved issues for a product containing list of keywords (single version)
### Query name: QueryResolvedIssuesWithKeyWordsForProductAndVersion
### Parameters:
- @ProductId - _Int_ - The unique Id for the product. 
This can be obtained from getting all products.
- @Version - String/NVARCHAR(50) - Gives the version required
- @KeyWords - _String/NVARCHAR(MAX)_ - A string containing the keywords to use to search, seperated by spaces.

### Returns:
Issues at the resolved status  belonging to the given product at the specified version containing the key words specified in the ProblemDescription, ordered by their Created Date, in descending order.

### Example
- _EXEC QueryResolvedIssuesWithKeyWordsForProductAndVersion 1,								    '1.0', 'TCP matrix';_


## 19. Get all resolved issues within date range for a product containing list of keywords (all versions)

### Query name: QueryResolvedIssuesWithKeyWordsForProductAndDateRange
### Parameters:
- @ProductId - _Int_ - The unique Id for the product. 
This can be obtained from getting all products.
- @From - DateTime/DATE - Gives the starting date to filter the results, inclusive.
- @To - DateTime/DATE - Gives the ending date to filter the results, inclusive.
- @KeyWords - _String/NVARCHAR(MAX)_ - A string containing the keywords to use to search, seperated by spaces.

### Returns:
Issues at the resolved status  belonging to the given product containing the key words specified in the ProblemDescription, created between the From date and the To date, inclusive, ordered by their Created Date, in descending order.

### Example
- _EXEC QueryResolvedIssuesWithKeyWordsForProductAndVersion 1,								    '1.0', 'TCP matrix';_


## 20. Get all resolved issues within date range for a product containing list of keywords (all versions)

### Query name: QueryResolvedIssuesWithKeyWordsForProductAndVersionAndDateRange
### Parameters:
- @ProductId - _Int_ - The unique Id for the product. 
This can be obtained from getting all products.
- @Version - String/NVARCHAR(50) - Gives the version required
- @From - DateTime/DATE - Gives the starting date to filter the results, inclusive.
- @To - DateTime/DATE - Gives the ending date to filter the results, inclusive.
- @KeyWords - _String/NVARCHAR(MAX)_ - A string containing the keywords to use to search, seperated by spaces.

### Returns:
Issues at the resolved status  belonging to the given product at the specified version containing the key words specified in the ProblemDescription, created between the From date and the To date, inclusive, ordered by their Created Date, in descending order.

### Example
- _EXEC QueryResolvedIssuesWithKeyWordsForProductAndVersionAndDateRange 1, '1.2', '2021-01-01', '2021-09-25', 'TCP Matrix';_
