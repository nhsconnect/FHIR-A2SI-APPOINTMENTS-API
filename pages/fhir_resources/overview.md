---
title: Resources Overview
keywords: getcarerecord, structured, rest, resource
sidebar: foundations_sidebar
permalink: resources_overview.html
summary: "This page provides an overview of the FHIR STU3 Resources that are required to build the required API messaging. Each link will take you to the resource page detail with a link to the StructureDefinitions of each resource."
---

{% include important.html content="This site is under development by NHS Digital, it is advised not to develop against these specifications until a formal announcement has been made." %}

## Background ##

- A service would need to have been identified prior to initialising the booking system.
- Where the selected service offers appointment Booking, it will include an value.
- The ASID is used <a href='process.html#find-endpoint'>to locate the FHIR endpoint</a> to be queried.
- A FHIR RESTful <a href='search_free_slots.html'>Search request is sent</a> to the FHIR endpoint for Slots that meet the time constraints, the appropriate service id (e.g. from DoS) is passed as a constraint on the HealthcareService ID.
- The specified HealthcareService may run zero to many Schedules.
- Each Schedule may contain zero to many Slots.
- The Slots are filtered using the Time constraints before being returned in a <a href='http://hl7.org/fhir/stu3/bundle.html#searchset'>searchset Bundle</a>.


*The diagram below illustrates the resources required for managing the appointment slots. The Slot resource is used to manage a slot of time for an appointment. The Slot always references a Schedule resource which acts as a container for the slots of time. Each Schedule will also reference additional resources to determine who the schedule is for.*

<img src="images/UEC-Appointments/ClassDiagram.png">

## Appointment structure ##

- The Appointment resource is <a href='book_an_appointment.html'>POSTed to the FHIR endpoint</a> in a FHIR RESTful Create.
- The Appointment resource contains a Slot retrieved above.
- The Appointment resource contains a Patient resource.
- The Appointment resource contains a DocumentReference resource.

<img src="images/UEC-Appointments/Appointment1.png">


| Resource | Description | Profile |
| --- | --- | --- |
| <a href='appointment.html'>Appointment</a> | The appointment that is booked, linking a specific Patient into a specific Slot | <a href='https://fhir.hl7.org.uk/STU3/StructureDefinition/CareConnect-Appointment-1'>CareConnect-Appointment-1</a> |
| <a href='slot.html'>Slot</a> | A free time period, into which an appointment with a specific Patient can be booked | <a href='https://fhir.hl7.org.uk/STU3/StructureDefinition/CareConnect-Slot-1'>CareConnect-Slot-1</a> |
| <a href='schedule.html'>Schedule</a> | A grouping of Slots, used to link them to the HealthcareService which the slots are provided as part of | <a href='https://fhir.hl7.org.uk/STU3/StructureDefinition/CareConnect-Schedule-1'>CareConnect-Schedule-1</a> |
| <a href='healthcare_service.html'>HealthcareService</a> | A HealthcareService which has been selected from the DoS, and delivers one or more Schedules | <a href='https://fhir.hl7.org.uk/STU3/StructureDefinition/CareConnect-HealthcareService-1'>CareConnect-HealthcareService-1</a> |
| <a href='organisation.html'>Organization</a> | An Organisation which delivers one or more HealthcareServices | <a href='https://fhir.hl7.org.uk/STU3/StructureDefinition/CareConnect-Organization-1'>CareConnect-Organization-1</a> |
| <a href='location.html'>Location</a> | A Location at which an Organisation delivers one or more HealthcareServices | <a href='https://fhir.hl7.org.uk/STU3/StructureDefinition/CareConnect-Location-1'>CareConnect-Location-1</a> |
| <a href='patient.html'>Patient</a> | A Patient for whom an appointment is being booked | <a href='https://fhir.hl7.org.uk/STU3/StructureDefinition/CareConnect-Patient-1'>CareConnect-Patient-1</a> |
| <a href='document_reference.html'>DocumentReference</a> | A DocumentReference which points to a document which gives information supporting the Appointment | <a href='https://fhir.hl7.org.uk/STU3/StructureDefinition/CareConnect-DocumentReference-1'>CareConnect-DocumentReference-1</a> |

