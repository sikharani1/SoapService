# SoapService
Implemented a SOAP service that returns XML Strings written in Java for the description for the appointment process in a patient management system.
Use Case 1 below (has Business Layer rules) plus the SOAP service with the following methods (Sample output is included at the end):
"	initialize() - Initialize the database (this may require a server restart after running if you get server errors).
"	getAllAppointments() -Return a list of all appointments and related information.
"	getAppointment(String appointNumber) - Return a specific appointment and related information.
"	addAppointment(String xmlStyle) - Create a new appointment providing the required information in XML and receiving XML or error message.
"	The XML strings you produce and consume MUST MATCH the samples included at the end.
"	You must use the provided Data Layer (includes an embedded database).  There is a test class provided in the zip file that has an example of how to use the Data Layer and what jar files are to be imported into your classes. Also in that zip file is a folder containing html documentation on the model classes used in the data layer.  Valid table names for use with the Data Layer are (watch the capitalization): Appointment, AppointmentLabTest, PSC, Patient, Physician, Phlebotomist, LabTest, Diagnosis.

Use Case Number: 1 

Use Case Name: Set an Appointment
Primary Actor: Patient
Secondary Actor: Appointment Specialist
Description:
A patient schedules an appointment for a laboratory test ordered by an attending physician.

Pre-Condition:
1.	The patient is registered with Cellular One, i.e., exists in the system. 
2.	The patient's physician is valid and exists in the system. 
3.	The ordered lab test is valid and exists in the system. 
4.	The requested clinician (phlebotomist) is valid and exists in the system. 
Post-Condition:	
1.	The appointment has been registered in the system.
Normal Course of Action:
1.	The Patient requests a laboratory appointment. 
2.	The Appointment Specialist requests [patient first & last name, date of birth, mailing address, tests ordered (by test number), desired phlebotomist, DSMIII diagnosis code, desired patient service center, requested appointment date and time].
3.	The Patient provides information requested. 
4.	The Appointment Specialist selects the correct Patient from the system [patient's first & last name, date of birth]
5.	The System displays patient information [patient identifier, patient's first & last name, date of birth, insurance (y/n), physician name].
6.	The Appointment Specialist confirms correct patient has been selected.
7.	The Appointment Specialist requests appointment [patient requested: date, time, phlebotomist, patient service center].
8.	The System checks availability based upon appointment requirements. 
9.	The System creates a unique appointment number (not the data component).
10.	The System determines the cost of each test and calculates the total cost (the cost of each test is stored by the data component).
11.	The System reserves the appointment [appointment number, date, time, phlebotomist, patient service center, patient id, test number].
12.	The System displays the appointment number, date, time, phlebotomist, tests ordered, and total cost of testing, and requests confirmation. 
13.	The Appointment Specialist commits appointment.
14.	The Appointment Specialist confirms appointment with patient and provides the appointment number. 
Extensions:
9.	The System displays "phlebotomist, and/or patient service center not available at that time" conflict message.
10.	The System determines the next available date and time for the phlebotomist and patient service center requested. 
11.	The System displays next available [date, time] for the requested phlebotomist and patient service center.
12.	The Appointment Specialist requests that the patient accept the available date, time.
13.	If Patient accepts, then return to step 10 in the normal course, otherwise terminate use case. 

Assumptions: 
The duration for each appointment is 15 minutes. 
Appointments can be made from 8am to 5pm.
It takes a phlebotomist 30 minutes to get from one PSC to another and be ready for an appointment after the end of another appointment.  The phlebotomist can be at any PSC at 8am, however, if their next appointment is at another PSC, they need 30 minutes from 8:15am to get to that next PSC.  The phlebotomist will remain at the PSC of their appointment unless they are requested at another PSC for their next appointment (within 30 minutes).
