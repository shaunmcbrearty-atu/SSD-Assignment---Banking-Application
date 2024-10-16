# COMP08141: Secure Software Development Assignment

The Application that must be utilised as part of the assignment for COMP08141 is a simple banking Application intended to be utilised by a Bank Teller.

At present, the Application enables a Bank Teller to:

1) Open a Bank Account (Current Account or Savings Account).
2) Retrieve Information on an existing Bank Account (based on an Account Number).
3) Lodge money to a Bank Account.
4) Withdraw money from a Bank Account (note that Current Accounts can be overdrawn up to the Overdraft Amount specified at the time of Account Creation).
5) Close a Bank Account.

The Application comprises a .NET Console Application (C# Source Code) and a SQLite Database.

As part of the assignment, students are free to make any changes they wish to, to both the source code of the Application - as well as the structure of the associated Database. Note that the rationale behind any and all changes must be outlined in a Change Document.

As part of the assignment, students must implement the following additional security-related functionality:

## 1) Data Encryption [10% - 40%]

All Personally Idenitfiable Information (PII) handled by the Application should be encrypted-at-rest.

This security control may take the form of Application-Level Encryption (ALE)  or Database-Level Encryption:

- ALE involves data being encrypted by the Application - prior to being written to the associated Database - as well as data being decrypted by the Application after being read from a Database, _i.e. the Database is only responsible for storing and retrieving data; it does not have the ability to decrypt data_.

- Database-Level Encryption involves all data within a Database being encrypted as it is being written to disk by the associated Database Server (in the case of SQLite, there is no Database Server - [as such, this function is performed by the SQLite Database Driver](https://learn.microsoft.com/en-us/dotnet/standard/data/sqlite/encryption?tabs=net-cli)); however the Database Server retains the ability to decrypt all data, as well as process that data in plaintext form.

ALE is significantly more secure than Database Level Encryption (when implemented correctly); however, the process of adding support for ALE to an existing Application is challenging as doing so requires significant changes to both the source code of the Application as well as the structure of the associated Database. In light of the scale of this task, a total of 40% of the overall Marks associated with the source code deliverable for the assignment have been allocated for this solution.

On the other hand, the process of adding support for Database Level Encryption to an existing Application is significantly less complex (at the cost of being less secure). In light of this, the total number of Marks associated with this solution is limited to 10% with respect to the source code deliverable for the assignment, _i.e. a voluntary forfeiture of 30% of the available Marks if implementing this solution when compared with implementing an ALE based solution_.

Marks will be awarded under this heading based on the following criteria:

- Identification of PII data.
- Encryption of PII data.
- Appropriate use of Public-Key Cryptography and/or Symmetric-Key Cryptography (Block/Stream Cipher). 
- Appropriate use of Cryptography with respect to Algorithm selection, Key Size selection, Block Cipher Mode of Operation selection (if applicable), Padding Algorithm selection, etc. 
- Appropriate storage and protection of encryption Key Material and/or Initialisation Vectors (IVs - if applicable).


## 2) Logging [10%]

A record of all transactions performed by Bank Tellers must be recorded to the Windows Event Log by the Application (under the Application Name 'SSD Banking Application').

Each Log Entry should record the following information:

- Name of Bank Teller who performed the transaction, _i.e. WHO - Part 1_.
- Account No associated with the transaction - as well as the name of the Account holder, _i.e. WHO - Part 2_.
- Type of Transaction performed: 1) Account Creation, 2) Account Closure, 3) Balance Query, 4) Lodgement or 5) Withdrawal, _etc., i.e. WHAT_.
- One of: 1) The MAC Address of the device used to perform the transaction, OR 2) The IP Address of the device used to perform the transaction OR 3) The Windows Security Identifier (SID) of the device used to perform the transaction, _i.e. WHERE_.
- Date/Time of the transaction, _i.e. WHEN_.
- Reason for Transaction (OPTIONAL: only required if Lodging/Withdrawing an amount that exceeds €10,000.00), _i.e. WHY_.
- Metadata of Software Application used to perform the transaction (Name, Version No, Hash Value, etc.), _i.e. HOW_.

## 3) Authentication/Access Controls [10%]

Prior to utilising the Application, users must first authenticate to the `ITSLIGO.LAN` Active Directory Server (available on the `SSD_Assignment` virtual machine hosted on [Microsoft Azure Lab Services](https://labs.azure.com/)).

Only users contained within the `Bank Teller` User Group on Active Directory are permitted to use the Application.

Prior to deleting a Bank Account from the Database, the Application must prompt for Administrator Approval. Note that only users contained within the `Bank Teller Administrator` User Group on Active Directory are permitted to approve the deletion of Bank Accounts.

Note that all successful and failed login attempts should also be recorded to the Event Log specified in the previous section.

## Other [40%]

In addition to the list of prescribed functionalities outlined above, an additional 30% of the overall Marks allocated to the source code deliverable of the assignment has been allocated to any additional security controls implemented by students. Any additional security controls implemented should be in response to vulnerabilities and security controls identified by students during the Threat Modelling exercise to be completed as part of the assignment.

Furthermore, any changes made to the source code of the Application in response to the underlying programming language (C#.NET) or the Application Architecture (SQL-Based Client-Server) will also be considered under this heading.

The remaining 10% of Marks associated with the source code deliverable are allocated under the heading 'Overall Quality of Work'. Marks will be awarded under this heading based on the Presentation/Readability of Source Code, Modularity of Solution, use of Best Practices and use of Coding Conventions, etc.