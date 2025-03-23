CREATE TABLE Customers (
CustomerID NUMBER PRIMARY KEY,
Name VARCHAR2(100),
DOB DATE,
Phone VARCHAR2(15),
Email VARCHAR2(100),
Address VARCHAR2(255)
);
CREATE TABLE Policies (
    PolicyID NUMBER PRIMARY KEY,
    PolicyName VARCHAR2(100),
    PolicyType VARCHAR2(50),
    PremiumAmount NUMBER,
    CoverageAmount NUMBER
);
CREATE TABLE CustomerPolicies (
    CustomerPolicyID NUMBER PRIMARY KEY,
    CustomerID NUMBER REFERENCES Customers(CustomerID),
    PolicyID NUMBER REFERENCES Policies(PolicyID),
    StartDate DATE,
    EndDate DATE,
    Status VARCHAR2(20) CHECK (Status IN ('Active', 'Expired', 'Cancelled'))
);
INSERT INTO Customers VALUES (1, 'John Doe', TO_DATE('1990-05-15', 'YYYY-MM-DD'), '9876543210', 'john.doe@example.com', '123 Street, City');
INSERT INTO Policies VALUES (101, 'Health Insurance', 'Health', 5000, 200000);
INSERT INTO Policies VALUES (102, 'Life Insurance', 'Life', 7000, 500000);
INSERT INTO CustomerPolicies VALUES (1001, 1, 101, TO_DATE('2023-01-01', 'YYYY-MM-DD'), TO_DATE('2028-01-01', 'YYYY-MM-DD'), 'Active');
SELECT c.Name, c.Phone, p.PolicyName, cp.StartDate, cp.EndDate, cp.Status
FROM Customers c
JOIN CustomerPolicies cp ON c.CustomerID = cp.CustomerID
JOIN Policies p ON cp.PolicyID = p.PolicyID;
SELECT COUNT(*) AS ActivePolicies FROM CustomerPolicies WHERE Status = 'Active';
SELECT * FROM Policies WHERE PremiumAmount < 6000;

