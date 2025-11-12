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
- Employee Request 

```pseudocode
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
```
- manager response
```pseudocode
Start
  IF manager.ClickEmail OR manager.Login("VTSHOMEPAGE") THEN
      Display("VTS Home Page")

      VTS.DisplayManagerRequests(manager)
      VTS.DisplaySubordinatePendingRequests(manager)

      FOR each request IN SubordinatePendingRequests DO
          PROMPT "Approve or Deny the request?"
          INPUT decision 

          IF decision = "Approve" THEN
              ApproveRequest(request)
              OUTPUT "Request approved successfully!"
              SendNotificationToEmployee(request.Employee, 
                  "Your vacation request has been approved.")
          
          ELSE IF decision = "Deny" THEN
              PROMPT "Enter reason for denial"
              INPUT denialReason
              DenyRequest(request, denialReason)
              OUTPUT "Request denied and reason saved."
              SendNotificationToEmployee(request.Employee, 
                  "Your vacation request has been denied. Reason: " + denialReason)
          END IF
      END FOR
  ELSE
      OUTPUT "Access denied. Please log in to VTS."
  END IF
End
```
---

## 📘 **Alternate flow: Withdraw Request**

1. The employee navigates to the VTS home page through the intranet portal application, which identifies and authenticates the   employee with the privileges necessary for using the VTS.
2. The VTS home page contains a summary of vacation time requests, outstanding balances per category of time, and the current status of all active vacation time requests for the previous 6 months and up to 18 months in the future.
3. The employee selects a vacation time request to withdraw, one that is currently pending approval. 
4. The VTS prompts the employee to confirm the request to withdraw the previously submitted vacation time request.
5. The employee confirms the desire to withdraw, and the request is removed from the manager’s list of pending approvals. 
6. The system sends a notification e-mail to the manager. 
7. The system updates the request state to withdrawn.

---
## 📊 **Flowchart**

![Flowchart - Withdraw Request](https://github.com/ABDULLAH1SAID/Vacation-Tracking-System/blob/main/images/flowchart_Withdrow_Request.drawio.png?raw=true)


## 🔄 **Sequence Diagram**

![Sequence Diagram - Withdraw Request](https://github.com/ABDULLAH1SAID/Vacation-Tracking-System/blob/main/images/sequence_Digram_WithDraw.drawio.png?raw=true)


---


## 📘 **Alternate flow:  Cancel Approved Request**

1. The employee navigates to the VTS home page through the intranet portal application, which identifies and authenticates the employee with the privileges necessary for using the VTS.
2. The VTS home page contains a summary of vacation time requests, outstanding balance per category of time, and the current status of all active vacation time requests for the previous 6 months and up to 18 months in the future.
3. The employee selects a vacation time request to cancel, one that is in the future (or recent past) and has been approved.
 4. If the request is in the future, the employee is prompted to confirm the cancellation. If the request is in the recent past, the employee is 
prompted to confirm the cancellation and provide a short explanation. If the employee approves the cancellation and provides the required information, an e-mail notification is sent to the manager, and the state of the request is changed to canceled. The time allowances used to make the request are returned to the employee. The employee can also abort the cancellation, effecting no changes to the current requests.
5. The employee is returned to the main VTS home page. The summaries are updated to reflect any changes made to the employee’s outstanding vacation time requests


---
## 📊 **Flowchart**

![Flowchart - Withdraw Request](https://github.com/ABDULLAH1SAID/Vacation-Tracking-System/blob/main/images/flowchart_Cancel_Request.drawio.png?raw=true)


## 🔄 **Sequence Diagram**

![Sequence Diagram - Withdraw Request](https://github.com/ABDULLAH1SAID/Vacation-Tracking-System/blob/main/images/cancel_approved_Request_sequenceDigram.drawio.png?raw=true)


---


## 📘 **Alternate flow:  Edit Pending Request**

1. The employee navigates to the VTS home page through the intranet portal application, which identifies and authenticates the employee with the privileges necessary for using the VTS.
2. The VTS home page contains a summary of vacation time requests, outstanding balances per category of time, and the current status of all active vacation time requests for the previous 6 months and up to 18 months in the future.
3. The employee selects a request to edit, one that is pending approval.
4. The VTS displays an editable view of the request. The employee is allowed to change the title, comments, or dates. The employee can also choose to delete or withdraw this request.
5. The employee changes request information and submits the changes to the system.
6. If the employee withdraws the request, the VTS prompts for confirmation before withdrawing the request. If changes are made only to the information, the changes are accepted, and the screen returns to the main VTS home page. If there are errors or problems with the information changes, the VTS redisplays the editing page andhighlights and explains all problems.

---
## 📊 **Flowchart**

![Flowchart - Withdraw Request](https://github.com/ABDULLAH1SAID/Vacation-Tracking-System/blob/main/images/flowchart_update_pending_RequestDiagram.drawio.png?raw=true)


## 🔄 **Sequence Diagram**

![Sequence Diagram - Withdraw Request](https://github.com/ABDULLAH1SAID/Vacation-Tracking-System/blob/main/images/Sequence_Digram_Edit_Pending_Request.drawio.png?raw=true)


---

## 📊 **State Machine**
![State Machine](https://github.com/ABDULLAH1SAID/Vacation-Tracking-System/blob/main/images/State%20Machine.png?raw=true)




