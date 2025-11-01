# 🧩 Vacation Tracking System – Complete Analysis

## 1️⃣ Requirements

### Vision
The goal is to enable employees to manage their vacations easily without the need for full familiarity with company policies, while meeting the need to simplify HR department tasks and reduce non-core administrative activities.

### Functional Requirements
- Implements a flexible rules-based system for validating and verifying leave time requests
- Enables manager approval (optional)
- Provides access to previous and future vacation requests
-  Uses e-mail notification to request manager approval and notify employees 
of request status changes
- Keeps activity logs for all transactions
-  Enables the HR and system administration personnel to override all actions 
restricted by rules, with logging of those overrides
- Allows managers to directly award personal leave time (within system-set limits)
- Provides a Web service interface for other internal systems to query any 
given employee’s vacation request summary
- Interfaces with the HR department’s legacy systems 

### Non-Functional Requirements
- The system must be easy to use.
- The system must provide a fast response time to user actions.
- The system must operate using the existing hardware and middleware infrastructure without requiring additional resources or major upgrades.
- The system must be added as a module to the company’s existing intranet portal and shall use the same Single Sign-On (SSO) mechanism for authentication.
  
### Constraints
- The system must use existing hardware and middleware.
- The system must be implemented as a module within the existing intranet portal.
- The system must use the same Single Sign-On (SSO) mechanism for authentication.
  
---

## 2️⃣ Domain – Define Problem
- Domain: Vacation Tracking System
- Problem Definition: the current vacation request process is manual and inefficient Employees must submit requests to their managers, who then forward them to the HR department for verification and approval
  
---

## 3️⃣ Actors
- Employee
- Manager
- HR Staff


