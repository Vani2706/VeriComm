# VeriComm Telecommunication System

## Overview

The VeriComm telecommunication system is a Java-based application using Spring Boot for managing telecommunication data. It comprises entities for handling calls, customers, and plans. The application provides functionalities for CRUD operations, querying, and business logic implementation related to calls, customers, and plans.

## Project Structure

### Entities

#### Call
Represents a telecommunication call record.

- **Fields:**
  - `callId` (Integer): Unique identifier for the call.
  - `duration` (Integer): Duration of the call in minutes.
  - `from` (String): The phone number from which the call originated.
  - `to` (String): The phone number to which the call was made.
  - `customer` (Customer): Reference to the `Customer` entity.
  - `plan` (Plan): Reference to the `Plan` entity.

- **Methods:**
  - `getCallId()`, `setCallId(Integer callId)`: Getter and Setter for `callId`.
  - `getDuration()`, `setDuration(Integer duration)`: Getter and Setter for `duration`.
  - `getFrom()`, `setFrom(String from)`: Getter and Setter for `from`.
  - `getTo()`, `setTo(String to)`: Getter and Setter for `to`.
  - `getCustomer()`, `setCustomer(Customer customer)`: Getter and Setter for `customer`.
  - `getPlan()`, `setPlan(Plan plan)`: Getter and Setter for `plan`.

#### Customer
Represents a customer using the telecommunication services.

- **Fields:**
  - `cid` (Integer): Unique identifier for the customer.
  - `cname` (String): Customer's name.
  - `phn` (String): Customer's phone number.
  - `email` (String): Customer's email address.
  - `location` (String): Customer's location.
  - `registerDate` (Date): The date when the customer registered.
  - `plan` (Plan): Reference to the `Plan` entity.

- **Methods:**
  - `getCid()`, `setCid(Integer cid)`: Getter and Setter for `cid`.
  - `getCname()`, `setCname(String cname)`: Getter and Setter for `cname`.
  - `getPhn()`, `setPhn(String phn)`: Getter and Setter for `phn`.
  - `getEmail()`, `setEmail(String email)`: Getter and Setter for `email`.
  - `getLocation()`, `setLocation(String location)`: Getter and Setter for `location`.
  - `getRegisterDate()`, `setRegisterDate(Date registerDate)`: Getter and Setter for `registerDate`.
  - `getPlan()`, `setPlan(Plan plan)`: Getter and Setter for `plan`.

#### Plan
Represents a telecommunication plan.

- **Fields:**
  - `pid` (Integer): Unique identifier for the plan.
  - `pname` (String): Plan name.
  - `validity` (Integer): Plan validity in days.
  - `duration_in_mins` (Integer): Duration of the plan in minutes.
  - `cost` (Float): Cost of the plan.

- **Methods:**
  - `getPid()`, `setPid(Integer pid)`: Getter and Setter for `pid`.
  - `getPname()`, `setPname(String pname)`: Getter and Setter for `pname`.
  - `getValidity()`, `setValidity(Integer validity)`: Getter and Setter for `validity`.
  - `getDurationInMins()`, `setDurationInMins(Integer duration_in_mins)`: Getter and Setter for `duration_in_mins`.
  - `getCost()`, `setCost(Float cost)`: Getter and Setter for `cost`.

### Services

#### CallService
Provides business logic and operations for managing `Call` records.

- **Methods:**
  - `getCallRecords()`: Retrieves all call records.
  - `getCallsByCustomerId(Integer cid)`: Retrieves all calls for a specific customer.
  - `getCallsByCustomerIdAndDuration(Integer cid, Integer duration)`: Retrieves calls for a customer where the duration is greater than the specified value.
  - `getTotalCallDurationByCustomerId(Integer cid)`: Calculates the total call duration for a customer.
  - `getCustomersByPlanId(Integer pid)`: Retrieves customers associated with a specific plan.
  - `getAverageCallDurationByPlanId(Integer pid)`: Calculates the average call duration for a specific plan.
  - `deleteCall(Integer callId)`: Deletes a call record by ID.
  - `deleteByDuration(Integer callId)`: Deletes a call record if its duration exceeds 1000 minutes.
  - `updateCall(Integer callId, Integer duration)`: Updates the duration of a call record.
  - `calculateRemainingORExceededDuration(Integer cid)`: Calculates the remaining or exceeded duration of a customer's plan and associated charges.

#### CustomerService
Provides business logic and operations for managing `Customer` records.

- **Methods:**
  - `getCustomers(Integer cid)`: Retrieves a customer by ID.
  - `getCustomers()`: Retrieves all customers.
  - `getCustomersRegisteredBetween(Date startDate, Date endDate)`: Retrieves customers registered between specified dates.
  - `getCustomersByPlan(Integer pid)`: Retrieves customers associated with a specific plan.

#### PlanService
Provides business logic and operations for managing `Plan` records.

- **Methods:**
  - `getPlan(Integer pid)`: Retrieves a plan by ID.
  - `getPlans()`: Retrieves all plans.
  - `getPlanBelowThisCost(Float cost)`: Retrieves plans with costs below a specified value.
  - `getPlansByCostRangeAndValidity(Float minCost, Float maxCost, Integer validity)`: Retrieves plans within a cost range and with a specified validity.
  - `getPlansByValidity(Integer validity)`: Retrieves plans with a specified validity.

### Controllers

#### CallController
Handles HTTP requests related to `Call` entities.

- **Endpoints:**
  - `GET /calls`: Retrieves all call records.
  - `GET /customer/{cid}/`: Retrieves calls for a specific customer.
  - `GET /customer/{cid}/total-duration`: Retrieves the total call duration for a customer.
  - `GET /plan/{pid}/customers`: Retrieves customers associated with a specific plan.
  - `GET /plan/{pid}/average-duration`: Retrieves the average call duration for a specific plan.
  - `DELETE /calls/{callId}`: Deletes a call record by ID.
  - `DELETE /call/{callId}`: Deletes a call record if its duration exceeds 1000 minutes.
  - `PUT /calls/{callId}/{duration}`: Updates the duration of a call record.
  - `GET /calculateDuration/{cid}`: Calculates the remaining or exceeded duration of a customer's plan and associated charges.

#### CustomerController
Handles HTTP requests related to `Customer` entities.

- **Endpoints:**
  - `GET /customers`: Retrieves all customers.
  - `GET /customer/{cid}`: Retrieves a customer by ID.
  - `GET /customers/{startDate}/{endDate}`: Retrieves customers registered between specified dates.
  - `GET /customers/{pid}`: Retrieves customers associated with a specific plan.

#### PlanController
Handles HTTP requests related to `Plan` entities.

- **Endpoints:**
  - `GET /plans`: Retrieves all plans.
  - `GET /plan/{pid}`: Retrieves a plan by ID.
  - `GET /plan/{cost}/plans`: Retrieves plans with costs below a specified value.
  - `GET /cost/{minCost}/{maxCost}/validity/{validity}`: Retrieves plans within a cost range and with a specified validity.
  - `GET /validity/{validity}`: Retrieves plans with a specified validity.

### Exceptions

- **CallNotFoundException**: Thrown when a call record is not found.
- **InvalidValidityException**: Thrown when validity-related conditions are not met.

