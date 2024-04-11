# Colofon

|Version|1.00|
|Authors|Christian Spruijt (SDB Groep), Jorrit Spee (Tenzinger, Santeon)|

# 1. Introduction

The mission of the Nuts community is to provide the healthcare sector with a public utility (in Dutch: "Nutsvoorziening") to improve information sharing in healthcare and support optimal collaboration. This public utility consists of open specifications and an open-source software reference implementation in the form of a Nuts-node. Because the function of the Nuts-network formed by the Nuts-nodes is limited to the realization of a generic trust layer, it is suitable for many different applications.

In the pioneering phase of the Nuts community, the Nuts and Bolts metaphor was used to describe the generic Nuts specification (then “Nuts”) and the specific applications (then “Bolts”). The term “Bolt” has been replaced by “Application on Nuts”. This term clarifies the separation between the specific applications and the generic trust layer and emphasizes the resulting scalability.

An 'application on Nuts' is a specific application that uses the generic Nuts-specification and for which parties have agreed additional public requirements and specifications.
The application on Nuts "Notified Pull" sets out these additional requirements and specifications for the Twiin (functional) exchange pattern 'Notified Pull' ([elaboration in Dutch by Twiin](https://twiin-afsprakenstelsel.scrollhelp.site/ta12/10-1-4-uitwisselpatroon-notified-pull-versturen-no)) and the Twiin 'Technical Agreement FHIR Notified Pull' ([TTA FHIR - Notified pull](https://twiin-afsprakenstelsel.scrollhelp.site/ta12/10-2-3-tta-fhir-notified-pull)).

The application on Nuts "Notified Pull" has been prepared by the collaborating software suppliers in the Nuts community. It clearly specifies how the Twiin 'Technical Agreement FHIR Notified Pull' will take place in terms of process and technology, using the Nuts specification and other open standards.

This document is primarily intended for software suppliers who are starting an implementation process. This document provides them with the necessary insights. In addition, this document aims to be readable for healthcare organizations involved, so that it becomes clear whether the process described here meets their wishes.

This document is not complete. It is currently a living document to reach working agreements and technical solutions between suppliers. So some things will change in the coming months. In addition, this document is also an index: in many places it will refer to existing standards and other documentation. In this way we keep this document concise and readable, and we can also reuse the documentation we refer to for other Applications on Nuts.

We hope you enjoy reading it, and if this document raises any questions, we would be happy to [answer](https://nuts.nl/contact/) them.

## 1.1 Use cases

The application on Nuts "Notified Pull" is generic in nature and offers support for multiple use cases. Examples of supported use cases are medical specialist referral (BgZ-referral), medication prescription and other cross-organizational workflow requests. Applying the application on Nuts "Notified Pull" to a specific use case takes place on the basis of a use-case-profile. The use-case-profile is documented separately and describes, among other things, the governance, the information standards, the permitted authentication means, the permitted legal bases and the access policy of the use case. 

E.g. the Nuts-use-case-profile "[bgz-referral](https://github.com/jorritspee/nuts-use-case-profile-bgz-referral/blob/main/README.md)" describes how to use this specification in the context of a medical specialist referral (commonly reffered to in Dutch as a BgZ-verwijzing).

## 1.2 Relation to other documents

- *Twiin Technical Agreement FHIR Notified Pull* (abbreviated as TTA FHIR - Notified pull): https://twiin-afsprakenstelsel.scrollhelp.site/ta12/10-2-3-tta-fhir-notified-pull
  TTA FHIR - Notified pull offers clear specifications for the use of FHIR at the data layer. However, TTA FHIR - Notified pull also describes specifications for the generic functions 'authentication' and 'authorization'. These specifications are not compatible with Trust over IP based infrastructures such as Nuts. In addition, TTA FHIR - Notified pull does not describe specifications for the generic function 'addressing'. This means that additional agreements are required for each implementation. The goal of TA-Notified-Pull-on-Nuts is to achieve scalability by expanding Twiin Technical Agreement FHIR Notified Pull with an unambiguous and Trust over IP compliant specfication use of the above generic functions.
- *Twiin Technical Agreement FHIR - Authentication & Authorization* (abbreviated as TTA FHIR - Authentication & Authorization): https://twiin-afsprakenstelsel.scrollhelp.site/ta12/10-2-5-tta-fhir-authentication-authorization
  TTA FHIR - Authentication & Authorization specifies the generic functions 'authentication' & 'authorization'. The abovementioned TTA FHIR - Notified pull refers to this specification.  TA-Notified-Pull-on-Nuts replaces TTA FHIR - Authentication & Authorization for a specfication that is aligned with the Nuts-specifications.
- *Twiin Technical Agreement FHIR - Addressing* (abbreviated as TTA FHIR - Addressing): https://twiin-afsprakenstelsel.scrollhelp.site/ta12/10-2-8-tta-addressing
  TTA FHIR - Addressing specifies the generic functions 'addressing'. The abovementioned TTA FHIR - Notified pull refers to this specification.  TA-Notified-Pull-on-Nuts replaces TTA FHIR - Addressing for a specfication that is aligned with the Nuts-specifications.
- *Nuts-use-case-profile "bgz-referral"*: https://github.com/jorritspee/nuts-use-case-profile-bgz-referral/blob/main/README.md
  The Nuts-use-case-profile "bgz-referral" describes how to use the specification 'TA-Notified-Pull-on-Nuts' in the context of a medical specialist referral (commonly reffered to in Dutch as a BgZ-verwijzing).
- *HL7 FHIR Workflow Management Communication Pattern F*: https://www.hl7.org/fhir/workflow-management.html#optionf
  HL7 has described a FHIR workflow management communication pattern in which a Task-resource is created on the placer's system. The application on Nuts Notified Pull complies to this pattern and provides an implementation guide for the digital interactions between actor Placer and actor Filler. The actor Placer corresponds to "Sending Organization". The actor Filler corresponds to "Receiving Organization".
- *Application-on-Nuts Zorginzage 2022*: https://nuts-foundation.gitbook.io/bolts/zorginzage/zorginzage-2022
  This application-on-Nuts specifies how to implement cross organzational medical data requests. It describes the "pull" part of "notified pull".

## 1.3 Key differences with TTA FHIR - Notified pull

- All references to TTA FHIR - Authentication & Authorization have to be ignored and replaced by the information provided in this document
- All references to TTA FHIR - Addressing have to be ignored and replaced by the information provided in this document
- In TTA FHIR - Notified pull the presence of the "Workflow Task" is optional. In application on Nuts Notified Pull the presence of the "Workflow Task" is mandatory.
- The application on Nuts Notified Pull has some additional requirements for the Notification-Task as specified in TTA FHIR - Notified pull

## 1.4 Glossary

- Nuts: A partnership of parties in healthcare to create a broadly supported, open, decentralized infrastructure for the exchange of data in healthcare and the medical domain. See www.nuts.nl.
- Application on Nuts — A practical application of the Nuts philosophy and open technology to enable a tangible use case in healthcare (formerly called "Bolt").
- Sending Organization: The healthcare institution from which the patient is referred. From the perspective of the BgZ referral, the organization that has patient data that needs to be transferred.
- Sending System: The software system that manages the data holder's data.
- Patient: The patient that is subject of the request
- Receiving Organization: The healthcare institution that receives the request, and therefore has an information need for data from the data holder.
- Receiving System — The software system that manages the recipient organization's data.
- Legal base — A legal base for being allowed to break the professional secrecy of the data holder.

# 2. Proces description

## 2.1 Exchange of workflow information

The generic process of exchanging workflow information is described in paragraph "[steps](https://www.hl7.org/fhir/workflow-management.html#12.12.1.1)" of HL7's Workflow Management Communication Patterns option F. Following

## 2.2 Exchange of medical record data

The Receiving Organization may need medical record data stored at the Sending Organization to perform the request.

# 3. Architecture

The paragraphs below provide an architectural solution for the process described in the previous chapter. We use the Nuts manifesto as a guideline.

## 3.1 Notified pull

This Application on Nuts uses the notified pull exchange pattern. This means that data is not actively sent to the data user (push) and that the data user system does not randomly retrieve data (pull). Instead, the data holder system sends a notification to the data user system that specific data is ready to be retrieved. Only in response to that notification does the data user system retrieve the necessary data.

The advantage of this approach over push is that the data user system only needs to retrieve data when the data user organization actually needs this data. In this way, the requirement for data minimization can be better met. It is also easier for the data holder to determine that the person retrieving data is the correct person, and to comply with the NEN 7513 and GDPR obligation to log which person has viewed the data. Compare a personal e-mail inbox where you log in to retrieve your e-mail with a fax machine in the department that anyone who walks by can access.

The advantage of a notified-pull mechanism over just a pull mechanism is timing and simplicity of security. If the data user system does not receive a notification, it must pull periodically to see whether new data is waiting at the data holder. Analogous to constantly reloading a web page. This causes a lot of unnecessary extra network traffic and delays in receiving messages. The data holder system must also compare the request with a complex rights structure with each pull to discover whether the recipient is allowed to retrieve the requested data.

The concept of notified pull is therefore the most effective and efficient way to support all requested functionality, guarantee privacy and apply auditing correctly. It prevents unnecessary copying of data between systems and the data holder retains full control over who gets access to data.

The notification can be used by the data user organization to immediately notify a user or initiate other processes. The notification must be as “thin” as possible and not contain any personal and/or medical data, in order to be useful at different stages of the process and because of the legal framework that we will describe in the next paragraph.

## 3.2 Legislation

The applicable legal texts can change per use case but in general these are:
- the WGBO (medical treatment agreement law);
- the Wabvpz (supplementary provisions on the processing of personal data in healthcare);
- the GDPR (General Data Protection Regulation) and the UAVG;
- Wegiz (Electronic Data Exchange in Healthcare Act).
The WDO is not relevant to this application as it governs patient identification. In the context of the BgZ referral, we only deal with identifying healthcare practitioners and healthcare organizations.

The GDPR (Article 9(1) of the GDPR and Article 22(1) of the UAVG) stats that personal data and special (medical) personal data may not simply be processed. This concerns both the Sending Organization and the Receiving Organization. The GDPR lists 6 grounds for processing:
1. consent of the person concerned (patient)
2. execution of an agreement
3. legal obligation
4. vital interests of the person concerned (patient)
5. performing a public law task
6. legitimate interest of the organization
The Sending Organization is subject to legal obligation, which is included in the WGBO. Things are a little less simple for the Receiving Organization.
If there is agreement as to who will be the Receiving Organization, and the patient has already given consent for the request from Sending Organization to Receiving Organization, the WGBO applies.
The WGBO states that a care provider may assume a patient's consent (implicit consent) to provide his or her patient data when that care provider sends the patient to another care provider for a current care need and provides patient data for this purpose (more details can be found in the report "[Implementatie van de WGBO Deel 4](https://www.knmg.nl/download/implementatie-van-de-wgbo-deel-4-toegang-tot-patientengegevens#:~:text=wet%20naar%20praktijk.-,Implementatie%20van%20de%20WGBO.,king%20met%20het%20NICTIZ%20ontwikkeld.)", chapter chapter 2.2.5.

## 3.3 Security and trust

In the notified pull scenario, the Receiving Organization (data user) retrieves data from the data holder. Upon receiving a request the data holder, as data controller, must ensure that the requesting organization (data user) is indeed allowed to access the data.

In addition to the requesting organization, the request also involves a specific user and the customer system. It is the Receiving System that, technically speaking, retrieves the data and shows it to the user. It is the user who actually gets access to the data. To prevent unauthorized persons from retrieving and viewing the data, the Sending System must be able to check the following:
1. Which Receiving System connects
2. That the Receiving System acts as a processor for the data user organization
3. On behalf of which natural person the Receiving System connects
4. That this person represents the data user organization
Assuming that there is a need for a solution that is as open as possible, where each party is given equal opportunities in the market and where security is of a very high level, the use of cryptographic proofs is necessary. Each of the above checks must be able to be performed using a cryptographic signature. After all, any solution that would use an active trusted third party for these controls would allow that party to influence or “lock down” the market, and would constitute a security hotspot and single point of failure in the design. [RFC002 §7](https://nuts-foundation.gitbook.io/drafts/rfc/rfc002-authentication-token#7.-supported-means) specifies which means should be accepted for personal authentication. Resources necessary for the authentication of organizations are still under development.

## 3.4 Separtaion of process and authorization

Nuts' ambition is to create a widely applicable and flexible infrastructure for data exchanges in healthcare, the medical domain and related domains. This requires us to ask ourselves the question again for every Application on Nuts: which parts of this process are unique to this use case and which are generally reusable?

This Application on Nuts specifies how to implement a Notified Pull mechanism. A Notified Pull mechanism can be used for all kinds of processes. The exact process to be supported, e.g. a referral, handoff of croos-organization worfklow, is describes in the use-case-profile.

In general when we look at the Notified Pull mechanism, there are three aspects to which an answer must be formulated: 
1. how do we organize the process of notification and workflow
2. how do we organize making medical record data available?

The second point is specified in the Application on Nuts [Zorginzage 2022](https://nuts-foundation.gitbook.io/bolts/zorginzage/zorginzage-2022)https://nuts-foundation.gitbook.io/bolts/zorginzage/zorginzage-2022. The generic parts of point 1 are specified in this Application on Nuts. Use case specific agreements are part of use-case-profiles.

## 3.5 Open and inclusive

In the design of this Application on Nuts, we opt for open standards, according to the principle of comply or explain. Aligned with [DIZRA](https://dizra.gitbook.io/dizra/), no obligations are made to use certain services or software. Each party is free to choose whether to use support services as long as these services do not impose requirements or restrictions on other parties. Basically, this means that a distributed solution is assumed, where each party is equal and where two parties can directly exchange data with each other regarding the Notified Pull mechanism without the intervention of third parties.

# 4 Specifications

The exchange of data in the notified pull mechanism can be divided into two major parts: 
1. process-tracking: the process-related part, and
2. the retrieval of the data.
In this chapter we will further elaborate on both aspects of the exchange. As much as possible, broadly applicable and standardized solutions are assumed that can also be used outside the notified pull mechanism.

The application on Nuts Notified Pull can be used in various healthcare applications. Specific agreements apply to a number of topics for each healthcare use case:
1. Identifier of the healthcare application
2. Governance
3. Information standards
4. Permitted means of authentication
5. Permitted legal bases and evidence
6. Availability
7. The access policy to be applied
These specific agreements are recorded per healthcare use case in the use case profile. Each use case profile describes agreements that are additional to the content of the Application on Nuts Notified Pull. For agreements about information and data, reference is made where possible to Nictiz information standards. See below for an overview of healthcare use cases, identifiers and healthcare use case profiles. This overview can easily be expanded with other healthcare use cases.

| Use case                                  | Use case identifier           | Use case profile                                                                  |
|-------------------------------------------|-------------------------------|-----------------------------------------------------------------------------------|
| Medical specialist referral (BgZ referral)| bgz-referral                  | [link](https://github.com/jorritspee/nuts-use-case-profile-bgz-referral/tree/main)|
| Shared Care Planning                      | t.b.d                         | t.b.d.                                                                            |

## 4.1 Process tracking

The correct Receiving System must be notified, so that the Receiving Organization knows that a workflow request is made to the organization. The purpose of the notification is to notify the Receiving Organization that workflow data is available. It is also necessary to be able to monitor the progress of the workflow process. Every workflow must therefore have a status: is the workflow being processed, has it been cancelled, is it ready?

### 4.1.1 Workflow Task
The [Workflow-Task resource](https://www.hl7.org/fhir/task.html) is used to track the progress of the worfklow. The Sending Organization (data holder) is responsible for setting out the Workflow-task. If the data holder wants to send a workflow request to a Receiving Organization, a workflow task must be created for this. Because of this responsibility and because of the principle of data at the source, the Workflow task will be stored in the data holder system (Sending System). The Receiving System (data user system) is notified and can retrieve the Workflow task. For every change in the Workflow task, the data holder system will send a notification. 

TTA FHIR - Notified pull does not describe the elements of the generic workflow task. In the technical design for the nursing handover, the Workflow Task resource is specified in §3.4. For the sake of reusability, this Application to Nuts uses the latter Workflow-Task specification as a generic basis. 

In terms of data, the Workflow task can contain references to the various (FHIR-)resources relevant to the execution of the Workflow-task.

The application on Nuts Notified Pull uses the following generic specifications. In each use case profile the exact contents of the Worfklow-Task for that use case are specified.

| Attribute                        | Card.           | Description                                                                                                                                         |
|----------------------------------|-----------------|-----------------------------------------------------------------------------------------------------------------------------------------------------|
| intent                           | 1..1 (unchanged)| Fixed value: "order" (unchanged)                                                                                                                    |
| owner.identifier                 | 1..1 (unchanged)| did of Receiving Organization   ??DID or FHIR-ref??                                                                                                    |
| for                              | 1..1 (unchanged)| Reference to FHIR Patient-resource. It is not allowed to include a BSN (or other information that can be linked to an individual) in the workflow-Task when it is accessed without a personal authentication contract|
| status                           | 1..1 (unchanged)| Fixed value: "requested" (unchanged)                                                                                                                |
| identifier                       | 1..1 (unchanged)| uuid/logical id of the Workflow-Task, Tip: Fill with groupIdentifier-field of the Notification Task with the same value                             |
| code.coding                      | 1..1 (unchanged)| The use case profile MUST specify the correct (SNOMED-)code(s) to use heren(unchanged)                                                              |    
| restriction.period               | 0..1 (unchanged)| This period information should be aligned to validity of the issued Nuts Authorization Credentials. Period information in NutsAuthzCred (based on expiration date) is leading. |
| requester.agent.identifier       | 1..1 (unchanged)| \<did of Sending Organization\>/serviceEndpoint?type=fhir          |
| requester.onBehalfOf.identifier  | 1..1 (unchanged)| did of Sending Organization                                                                                                                          |
| owner.identifier                 | 1..1 (unchanged)| did of Receiving organization                                                                                                                          |
| input                            | 0..0            | a list of references to and/or search-queries for resources containing the Patient's personal information that is releveant for handling the workfow-Task. The use case profile MUST specify the allowed read- and search-requests|
| input:authorization-base         | 0..1 (unchanged)| did of NutsAuthorizationCredential for access to personal FHIR-resources (i.e. the Patient resource in the for-element and all resources in the input-element. Please note: Notified Pull makes use of two NutsAuthorizationCredentials: one for authorizing access to personal FHIR-resources and one for authorizing access to the Workflow Task-resource. Constraints (e.g. system and code) follow Twiin TA Notified Pull|

An informative template for the Workflow Task can be found here: https://github.com/jorritspee/Application-on-Nuts-Notified-Pull/blob/main/Workflow-Task-Template.json.

### 4.1.2 Organization endpoint discovery

The Sending Organization is responsible for notifying the correct Receiving Organization. When selecting that Receiving Organization, a number of challenges arise:
1. Does the intended Receiving Organization have a Receiving System that supports the workflow request/ worfklow use case?
2. What is the technical address of this Receiving System?
3. Can the Receiving System be trusted? In other words: is the supplier of the Receiving System actually a processor of the Receiving Organization?

The Nuts register according to [RFC006](https://nuts-foundation.gitbook.io/drafts/rfc/rfc006-distributed-registry) of the Nuts specification is used to find the Receiving Organization. To support the workflow use case, both the Sending Organization and the Receiving Organization must register a service in the register.

Services can be registered per supplier and/or per organization according to the [service specification](https://nuts-foundation.gitbook.io/drafts/rfc/rfc006-distributed-registry#4.-services)https://nuts-foundation.gitbook.io/drafts/rfc/rfc006-distributed-registry#4.-services. 

Please use the compoundService.serviceEndpoint.keys to query endpoint url’s

#### 4.1.2.1 Sending Organization
A service must be registered for the Sending Organization:

```json
{
  "id": "did:nuts:organization_identifier#xyz",
  "type": "<<use case specific Sending Organization service name>>", 
  "serviceEndpoint": {
    "oauth": "did:nuts:vendor_identifier/serviceEndpoint?type=production-oauth",
    "fhir": "did:nuts:vendor_identifier/serviceEndpoint?type=<<use case specific Sending Organization service name>>-fhir"
  }
}
```

The value for 'type' is specified in the use case profile. The 'serviceEndpoint' must contain the 'oauth' and 'fhir' fields. Both values must have a dynamic reference to an endpoint as specified in RFC006. The endpoint referenced from the fhir field must have a serviceEndpoint that points to the fhir basepath without trailing slash (/). The endpoint referenced from the oauth field must have a serviceEndpoint that points to the access token endpoint of an OAuth authentication server. The type in the query field may be chosen by the supplier himself. For example, the dynamic references in the example refer to the endpoints that the supplier has registered:

```json
{
    "id": "did:nuts:vendor_identifier#xyz",
    "type": "<<use case specific Sending Organization service name>>-fhir", 
    "serviceEndpoint": "https://fhir.example.com/base"
}

{
    "id": "did:nuts:vendor_identifier#xyz",
    "type": "production-oauth",
    "serviceEndpoint": "https://nuts.example.com/n2n/auth/v1/accesstoken"
}
```

#### 4.1.2.2 Receiving Organization

A service must be registered for the Receiving Organization:

```json
{
    "id": "did:nuts:organization_identifier#abc",
    "type": "<<use case specific Receiving Organization service name>>", 
    "serviceEndpoint": {
        "oauth": "did:nuts:vendor_identifier/serviceEndpoint?type=production-oauth",
        "notification": "did:nuts:vendor_identifier/serviceEndpoint?type=<<use case specific Receiving Organization service name>>-notify"
    }
}
```
With endpoints:

```json
{
    "id": "did:nuts:vendor_identifier#abc",
    "type": "<<use case specific Receiving Organization service name>>-notify",
    "serviceEndpoint": "https://notify.example.com/specific/path"
}

{
    "id": "did:nuts:vendor_identifier#abc",
    "type": "production-oauth",
    "serviceEndpoint": "https://nuts.example.com/n2n/auth/v1/accesstoken"
}
```

This <<use case specific Receiving Organization service name>>-notify endpoint should be the basepath on which notifications can be received regarding the Workflow-Task resource. The notification endpoint URL should not be registered with a / at the end. The next section describes the notification mechanism. This is therefore a notification that a new (or changed) Workflow-Task resource is ready at the Sending Organization. 

### 4.1.3 Notification protocol

When a Workflow task is added, the Sending System will send a notification to the previously registered endpoint of the Receiving System. This notification is structured using a FHIR Task-resource (in short: "Notification-Task") in accordance with the below specs. The application on Nuts reuses the [specification of the Notfication-Task](https://vzvz.atlassian.net/wiki/spaces/Twiincon/pages/331847512/10.3.1+Twiin-01+Send+Notification+Task#Request-message) that is part of TTA FHIR Notified Pull, with the following changes:

| Attribute                        | Card.           | Description                                                                                                                                         |
|----------------------------------|-----------------|-----------------------------------------------------------------------------------------------------------------------------------------------------|
| basedOn                          | 1..1            | Mandatory reference to the Workflow-Task.   No leading slash                                                                                |
| groupIdentifier                  | 1..1 (unchanged)| Tip: Fill with uuid/logical id of the Workflow-Task                                                                                                 |
| identifier                       | 1..1 (unchanged)| (unchanged)                                                                                                                                         |
| status                           | 1..1 (unchanged)| Fixed value: "requested" (unchanged)                                                                                                                |
| intent                           | 1..1 (unchanged)| Fixed value: "proposal" (unchanged)                                                                                                                 |
| code.coding                      | 1..1 (unchanged)| (unchanged)                                                                                                                                         |    
| restriction.period               | 0..1 (unchanged)| This period information should be aligned to validity of the issued Nuts Authorization Credentials. Period information in NutsAuthzCred (based on expiration date) is leading. |
| requester.agent.identifier       | 1..1 (unchanged)| <did of Sending Organization>/serviceEndpoint?type=fhir                                                                                            |
| requester.onBehalfOf.identifier  | 1..1 (unchanged)| <did of Sending Organization>             |
| owner.identifier                 | 1..1 (unchanged)| <did of Receiving Organization>                                                                                                                     |
| input:authorization-base         | 0..1 (unchanged)| did:nuts of NutsAuthorizationCredential for access to Workflow-Task (that is referenced in the basedOn-element). Please note: Notified Pull makes use of two NutsAuthorizationCredentials: one for authorizing access to personal FHIR-resources and one for authorizing access to the Workflow Task-resource. Constraints (e.g. system and code) follow Twiin TA Notified Pull|                                     |
| input:get-workflow-task          | 1..1            | Fixed value: true. Constraints (e.g. system and code) follow Twiin TA Notified Pull       |
| input: read-available-resource   | 0..0            |                                                                                                                                                     |
| input: query-available-resources | 0..0            |                                                                                                                                                     |

An informative template for the Notification Task can be found here: https://github.com/jorritspee/Application-on-Nuts-Notified-Pull/blob/main/Notification-Task-Template.json.


## 4.2 Data exchange

As described in §3.4, we separate the process tracking on the one hand from the data access authorization on the other. This means that in addition to the Workflow-task and Notfication-task that manage the process, there must also be a mechanism that controls access to data. The generic mechanism that controls access to data is described in [chapter 4](https://nuts-foundation.gitbook.io/bolts/zorginzage/zorginzage-2022#id-4.-specificaties) of the application on Nuts "Zorginzage 2022". Use case specific agreements about access control are described in the access policy section of the appropriate use case profile. When using a notified pull mechanism, different states of the Workflow-task resource can lead to different accesses rights.

## 4.3 BSN availability
This paragrah describes the availability of bsn's in the sequence that is used in this Application on Nuts. It is a summary of information that is already present in other parts of this specification and is therfore informal.
|artefact|bsn availability|reference to authorization credential|
|--------|----------------|-------------------------------------|
| notification task| no bsn| authorization credential that authorizes access to workflow task: "workflow task authorization credential"|
| workflow task authorization credential|no bsn|n/a|
| workflow task|no bsn| authorization credential that authorizes that authorizes access to personal resources: "bgz authorization credential"|
| bgz authorization credential| bsn | n/a|

# 5 Implementation

## 5.1 Register authorizations
![Register authorizations](https://www.plantuml.com/plantuml/png/RL8zRzmm3DtrAnvkQeShWWHT3WSt3T0r3PeKNRhm92OLR8k6FgvnVtqbE2SxXXT18X_VUwHu6oBvcFfEKOhYKdzYhq9htK2UUZpafDLs81SVo1ZhNd1pjSZVoUibVdsbL7xYaPt9703fA1vVEwivluQP2Ri9WySnHEvte31NBN5Jy5uCgtp3ILwB0dwmPdjUeskuuDU2KwxOd3LhGVLw9wSgf5wyf06xduEXoFWbldtkv2yYXNQdKB3OxvjASe2MVkWuyaHdpxbiAV76zysPGQoBe1J_YBV_A5fnXH4LZMCcdfi_833ZywUR3Cf1jG1Mt05fPVGf6yNnI5fp24_IickQfRKwyUc2bUIPEbi85HPXx6V1p7rfWGqy1qa-IpND1kLXScCTjag-R5JKVafXpQyc_hra36zDUxifpsTf-Vte4GKz6wkfGrOa_7OVI6lnPQjBCWM6fdnCeyGWdTNZn-t1L5kBNFLSltDq-hs9C2_8lKJxF4uBKRke19TTkAwxO7ZzfIL-cu_KT_y1)

Informative suggestion: Add a delay of 10 seconds between registering the authorizations and sending the notification to counter the race condition that authorization credentials have to be synced to the Nuts node of the Receiving System before the Receiving System can request an access token for retrieving the Workflow-Task.

## 5.2 Send notification
![Send notification](https://www.plantuml.com/plantuml/png/ZL5DZzem4BtxLunoWaCarDvG556azWW8KEyJUugcIUniRBFmxzTAl5cJ_T1UeioyZ_T6tbY7lVDj8z0xetrRKIzipRh37biu190bTwZT0PLYVO6VgmJVcjlh_iTAY332YRGA7W0edUdXLyEImjIzEK4sSk1qjuxQ3D1EgfGNbpkZI8G_gCnjI3YI9BxEsN4T-RF04GiraymeIBfkJJK5YKjlV0VPpZZ-Tyy29vREowJN6lvm49pHrg079WIiCnn25ttq1rPB0OaAyiba3KNnEohAyjEK8prviWvGIhBsR6hIiD06XbUmK954RmawNpKifmhpr3AU_9LhKVn_TlcbnzWdLK3-M2kGKobhsG0hi0CZkMQc_ROkRRo6yILWSTYVpkF04XqRdJkqzJBf-lxIlzYmGaUFoHyTc2RkwmHF3eY88fIEhy4sxaNuYatu-BPv0G00)

## 5.3 Retrieve Workflow-task
![Retrieve workflow task](https://www.plantuml.com/plantuml/png/VL8zRy8m4DtpAqvCT8Y4sWr54I11suKYGEriueEwIUpKTlZWr_UiDCO4n1RxtiTxEO-CPThMPH6nsYfPbnlKaSc5h9Xc9IneA39HCMaNZ7CXT_0o2EOJTMpldmTHH4TOeUIa0S0ogpIC2v4XdQgB4lGQ3AnEncBP0sOkh13NNCuLnuY-OAEEpW6McA7OTz7-sk6xXisCOWQUdk2pJjJ66qKxhUhACQqMk4VuKZhV5ke0QsRo7d7-0LF9AoN8XDNsMsbnPbOewG3W7I1Eh-8DOIR8P_RslWHi-NtJ_1N1dnpPPH9xPZ7C2LSo40UwGqYIDakQFhQdqs-Dnf97XiQiLOuI-gx06JHcIbE4MxFKBoIK60SIIV9piF5EipP2m82ucuBWWNz3UDol2oVnw4Bn2GdxEbtxZSLkOtVO3RRRwvCLWZEBzmbXcTRh8_UpcyI7zjLOoa0YrsdfmGrXhgpOdboNsg0c1CVRrRkc8mSfYpy0)

## 5.4 Retrieve medical record data
Please see chapter 4.9 of Zorginzage 2022 (https://nuts-foundation.gitbook.io/bolts/zorginzage/zorginzage-2022#id-4.9-sequenties).

## 5.5 Update Workflow-task
![Update workflow task](https://www.plantuml.com/plantuml/png/RL8zRzmm3DtrAnvkQeShWWHT3WSt3T0r3PeKNRhm92OLR8k6FgvnVtqbE2SxXXT18X_VUwHu6oBvcFfEKOhYKdzYhq9htK2UUZpafDLs81SVo1ZhNd1pjSZVoUibVdsbL7xYaPt9703fA1vVEwivluQP2Ri9WySnHEvte31NBN5Jy5uCgtp3ILwB0dwmPdjUeskuuDU2KwxOd3LhGVLw9wSgf5wyf06xduEXoFWbldtkv2yYXNQdKB3OxvjASe2MVkWuyaHdpxbiAV76zysPGQoBe1J_YBV_A5fnXH4LZMCcdfi_833ZywUR3Cf1jG1Mt05fPVGf6yNnI5fp24_IickQfRKwyUc2bUIPEbi85HPXx6V1p7rfWGqy1qa-IpND1kLXScCTjag-R5JKVafXpQyc_hra36zDUxifpsTf-Vte4GKz6wkfGrOa_7OVI6lnPQjBCWM6fdnCeyGWdTNZn-t1L5kBNFLSltDq-hs9C2_8lKJxF4uBKRke19TTkAwxO7ZzfIL-cu_KT_y1)

# 6 Access Policy
The access policy is described in the use case profile. Chapter 5 of Zorginzage 2022 (https://nuts-foundation.gitbook.io/bolts/zorginzage/zorginzage-2022#id-5.-access-policy) describes the minimum requrements of an access policy.
