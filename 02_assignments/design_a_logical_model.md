# Assignment 1: Design a Logical Model

## Question 1
Create a logical model for a small bookstore. 📚

At the minimum it should have employee, order, sales, customer, and book entities (tables). Determine sensible column and table design based on what you know about these concepts. Keep it simple, but work out sensible relationships to keep tables reasonably sized. Include a date table. There are several tools online you can use, I'd recommend [_Draw.io_](https://www.drawio.com/) or [_LucidChart_](https://www.lucidchart.com/pages/).

## Question 2
We want to create employee shifts, splitting up the day into morning and evening. Add this to the ERD.

## Question 3
The store wants to keep customer addresses. Propose two architectures for the CUSTOMER_ADDRESS table, one that will retain changes, and another that will overwrite. Which is type 1, which is type 2?

_Hint, search type 1 vs type 2 slowly changing dimensions._

Bonus: Are there privacy implications to this, why or why not?
```
1.Overwrite Existing Address (Type 1)

When create a new customer:

CREATE TABLE CUSTOMER_ADDRESS (
    CustomerID INT PRIMARY KEY,
    Street VARCHAR(100),
    City VARCHAR(50),
    Province VARCHAR(50),
    PostalCode VARCHAR(20),
    Country VARCHAR(50)
);

When needs to update to new address:

UPDATE CUSTOMER_ADDRESS
SET Street = 'New Street',
    City = 'New City',
    Province = 'New Province',
    PostalCode = 'New PostalCode',
    Country = 'New Country'
WHERE CustomerID = 1;

2. Retain Previous Address as History (Type 2)

When create a new customer, adds date range:

CREATE TABLE CUSTOMER_ADDRESS (
    AddressID INT PRIMARY KEY AUTO_INCREMENT,
    CustomerID INT,
    Street VARCHAR(100),
    City VARCHAR(50),
    Province VARCHAR(50),
    PostalCode VARCHAR(20),
    Country VARCHAR(50),
    StartDate DATE,
    EndDate DATE
);

When needs to update to new address:

UPDATE CUSTOMER_ADDRESS
SET EndDate = '2024-05-01'
WHERE CustomerID = 1 AND EndDate IS NULL;

-- Insert the new address
INSERT INTO CUSTOMER_ADDRESS (CustomerID, Street, City, Province, PostalCode, Country, StartDate, EndDate)
VALUES (1, 'New Street', 'New City', 'New Province', 'New PostalCode', 'New Country', '2024-05-02', NULL);

The second method would potentially face more risk to privacy implication due to all previous address are stored.

```

## Question 4
Review the AdventureWorks Schema [here](https://i.stack.imgur.com/LMu4W.gif)

Highlight at least two differences between it and your ERD. Would you change anything in yours?
```
1. There are more sub tables in the provided example such as emails, contact type etc. Mine has larger tables that include everything.

2. The example is very detailed and also has the production section, which mine did not consider. 
```

# Criteria

[Assignment Rubric](./assignment_rubric.md)

# Submission Information

🚨 **Please review our [Assignment Submission Guide](https://github.com/UofT-DSI/onboarding/blob/main/onboarding_documents/submissions.md)** 🚨 for detailed instructions on how to format, branch, and submit your work. Following these guidelines is crucial for your submissions to be evaluated correctly.

### Submission Parameters:
* Submission Due Date: `June 1, 2024`
* The branch name for your repo should be: `model-design`
* What to submit for this assignment:
    * This markdown (design_a_logical_model.md) should be populated.
    * Two Entity-Relationship Diagrams (preferably in a pdf, jpeg, png format).
* What the pull request link should look like for this assignment: `https://github.com/<your_github_username>/sql/pull/<pr_id>`
    * Open a private window in your browser. Copy and paste the link to your pull request into the address bar. Make sure you can see your pull request properly. This helps the technical facilitator and learning support staff review your submission easily.

Checklist:
- [ ] Create a branch called `model-design`.
- [ ] Ensure that the repository is public.
- [ ] Review [the PR description guidelines](https://github.com/UofT-DSI/onboarding/blob/main/onboarding_documents/submissions.md#guidelines-for-pull-request-descriptions) and adhere to them.
- [ ] Verify that the link is accessible in a private browser window.

If you encounter any difficulties or have questions, please don't hesitate to reach out to our team via our Slack at `#cohort-3-help`. Our Technical Facilitators and Learning Support staff are here to help you navigate any challenges.
