# LoanProcessor Overview
Federal and state laws regulate the fees that lenders can charge for processing mortgages.  While most regulations fall into standard categories, states often define their own limits they place on the total fees that can be charged.  Lenders need a way to tell whether a given loan passes all the regulatory compliance checks.

# Instructions
Create a web service that runs loan data through a suite of tests to validate whether the loan conforms to state-specific compliance regulations:
1. Create a RESTful, JSON-based web API using the .NET web platform and tools of your choice.  The API should contain at least one endpoint that processes a single loan.
2. The two tests described below comprise a single test suite: the application should be able to determine whether the loan needs to be checked for compliance, and if so, perform the checks and produce pass/fail results.
3. The API should return a response object that indicates which tests were run for the loan and whether the loan passed or failed each test.
4. Include one unit test as an example of how you would test the rules and/or engine.
5. Commit your work to this repository.

#### Notes:
* Your design should assume that there will eventually be more rules, with values coming from all 50 states.
* Don't put too much effort into the API aspects; focus on processing the validation rules.

# Tests

## APR Test

A mortgage's APR must not exceed rates specified by the states in which the property is located.  The rates may be different depending on the type of loan and whether it will be the owner's primary residence.

| State          | Percent Threshold                                                                             |                    |
| :------------- | :-------------------------------------------------------------------------------------------- | :----------------- |
| **New York**   | *Conventional Loans*:&nbsp;&nbsp;Primary Occupancy: 6%&nbsp;&nbsp;Secondary Homes: 8%         |
| **Virginia**   | *All Loans*:&nbsp;&nbsp;Primary Occupancy: 5%&nbsp;&nbsp;Secondary Homes: 8%                  |
| **Maryland**   | *All Loans*: 4%                                                                               |
| **California** | *Conventional and FHA Loans*:&nbsp;&nbsp;Primary Occupancy: 5%&nbsp;&nbsp;Secondary Homes: 4% | *All VA Loans*: 3% |



## Fee Test

The total fees charged for processing a mortgage cannot exceed the amount specified by each state.  The states also determine which fees are used to calculate the "Total Fees" amount.

| State          | Fees included in Total Fees                    | Maximum percent that can be charged                                                                      |
| :------------- | :--------------------------------------------- | :------------------------------------------------------------------------------------------------------- |
| **Virginia**   | Flood Certification, Processing, Settlement    | 7%                                                                                                       |
| **Maryland**   | Application, Credit Report                     | Loan amount <= 200,000: 4%; if > 200,000: 6%                                                             |
| **California** | Application, Settlement                        | Loan amount <= 50,000: 3%; if >50,000 and <= 150,000: 4%; if > 150,000: 5%                               |
| **Florida**    | Application, Flood Certification, Title Search | Loan amount <= 20,000: 6% if >20,000 and <= 75,000: 8%; if >75,000 and <= 150,000: 9%; if > 150,000: 10% |

For example, in Virginia, the sum of the amounts paid for Flood Certification, Processing, and Settlement cannot be greater than 7% of the total loan amount.

## Global Parameters

Run both tests only for loans of the following amounts and types:

| State          | Maximum Loan Amount | Loan Types                             |
| :------------- | :------------------ | :------------------------------------- |
| **New York**   | $750,000            | Conventional                           |
| **Virginia**   | No maximum          | Conventional, FHA, VA (all loan types) |
| **Maryland**   | $400,000            | Conventional, FHA, VA (all loan types) |
| **California** | $600,000            | Conventional, FHA, VA (all loan types) |
| **Florida**    | No maximum          | Conventional, VA                       |