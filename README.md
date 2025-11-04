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
- System admin

## 4️⃣ Use Case
🧭 Use Case: Manage Time

## 🎯 **Goal**
The employee wishes to submit a new request for vacation time.

## ✅ **Preconditions**
- The employee is authenticated by the portal framework.  
- The employee is identified as a valid company employee with privileges to manage his/her own vacation time.  

## 🏁 **Postconditions**
- A new vacation request is created and saved in a **Pending Approval** state.  
- An email notification is sent to the employee’s manager for approval.  

---

## 📘 **Main Flow**

1. The employee begins by selecting a link from the intranet portal to the VTS.
2. The VTS uses the employee’s credentials to look up the current status of all the employee’s vacation time requests and outstanding balances. Information is displayed for the previous 6 months and up to 18 months in the future.
3. The employee wants to create a new request. The employee selects one of the categories of vacation time with a positive balance to use.
4. The VTS prompts the employee for the date(s) and time for which torequest vacation time. The employee should have access to a visual calendar to help select and compare chosen dates.
5. The employee selects the desired dates and hours per date (e.g., four hours might indicate a half-day vacation time request). The employee enters a short title and description (no more than a paragraph in length) so that the manager will have more information with which to approve this request. When all the information is entered, the employee submits the request.
6. If the submitted information is incomplete or incorrect or does not pass validation, the Web page is redisplayed, with the errors highlighted and documented.
7. The employee has an opportunity to change the information or cancel the request. 
8. If the information is complete and passes validation, the employee is returned to the main VTS home page. If the employee’s vacation time requests require manager approval, an e-mail is immediately sent to 
the manager(s) authorized to approve the employee’s requests. 
9. The vacation time request is placed in a state of pending approval.
10. The manager responds to the e-mail by clicking on a link embedded in the e-mail or by explicitly logging into the intranet portal and navigating to the main VTS home page. 
11. The manager may be required to supply necessary authentication credentials to gain access to the portal and VTS application.
12. The VTS home page lists the manager’s own vacation time requests and outstanding balances but also has a separate section listing requests pending approval by subordinate employees. The manager selects each of these one at a time to individually approve or deny.
13. The VTS displays the details of the requested time and prompts the manager to approve or disapprove the request. If the request is disapproved, the manager is required to enter an explanation. Once the man
ager submits the result, the internal state of the request is changed to 
approved or rejected.
14. Whether a request is approved or rejected, an e-mail notification is immediately sent to the employee who made the request. The manager’s screen returns to the main VTS home page, and the manager may approve other outstanding requests, make a request for him- or herself, or simply leave the VTS application.

---
## 📊 **Flowchart**

![Flowchart - Manage Time](https://github.com/ABDULLAH1SAID/Vacation-Tracking-System/blob/main/images/FlowchartDiagram.jpg?raw=true)



## 🔄 **Sequence Diagram: Employee

![Sequence Diagram - Employee](https://github.com/ABDULLAH1SAID/Vacation-Tracking-System/blob/main/images/SequenceDigram.png?raw=true)



## 🔄 **Sequence Diagram: Manager

![Sequence Diagram - Manager](https://github.com/ABDULLAH1SAID/Vacation-Tracking-System/blob/main/images/managerSequence.drawio.png?raw=true)

---

## Pseudocode 
- //Employee Request 

Start
  Employee ← Connect("VTSLINK")
  systemVTS ← UseEmployeeCredentials(Employee)

  VTS.DisplayVacationRequestsAndBalances(Employee)

  IF Employee.CreatesRequest THEN
      categories ← GetCategoriesWithPositiveBalance(Employee)
      Display(categories)

      PROMPT "Select date(s) and time for which to request vacation"
      INPUT vacationDates, vacationTime

      isValid ← ValidateVacationInput(vacationDates, vacationTime)

      IF isValid THEN
          SaveVacationRequest(Employee, vacationDates, vacationTime)
          OUTPUT "Vacation request submitted successfully!"
          EmailSendTo("Manager")
      ELSE
          Display("An error occurred: " + Message.Error)
      END IF
  END IF
End

---






