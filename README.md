# 1. Introduction
The mission of the Nuts community is to provide the healthcare sector with a public utility (in Dutch: "Nutsvoorziening") to improve information sharing in healthcare and support optimal collaboration. This public utility consists of open specifications and an open-source software reference implementation in the form of a Nuts-node. Because the function of the Nuts-network formed by the Nuts-nodes is limited to the realization of a generic trust layer, it is suitable for many different applications.

In the pioneering phase of the Nuts community, the Nuts and Bolts metaphor was used to describe the generic Nuts specification (then “Nuts”) and the specific applications (then “Bolts”). The term “Bolt” has been replaced by “Application on Nuts”. This term clarifies the separation between the specific applications and the generic trust layer and emphasizes the resulting scalability.

An 'application on Nuts' is a specific application that uses the generic Nuts-specification and for which parties have agreed additional public requirements and specifications.
The application on Nuts "TA Notified Pull on Nuts" sets out these additional requirements and specifications for the Twiin (functional) exchange pattern 'Notified Pull' ([elaboration in Dutch by Twiin](https://twiin-afsprakenstelsel.scrollhelp.site/ta12/10-1-4-uitwisselpatroon-notified-pull-versturen-no)) and the Twiin 'Technical Agreement FHIR Notified Pull' ([TTA FHIR - Notified pull](https://twiin-afsprakenstelsel.scrollhelp.site/ta12/10-2-3-tta-fhir-notified-pull)).

The application on Nuts "TA Notified Pull on Nuts" has been prepared by the collaborating software suppliers in the Nuts community. It clearly specifies how the Twiin 'Technical Agreement FHIR Notified Pull' will take place in terms of process and technology, using the Nuts specification and other open standards.

This document is primarily intended for software suppliers who are starting an implementation process. This document provides them with the necessary insights. In addition, this document aims to be readable for healthcare organizations involved, so that it becomes clear whether the process described here meets their wishes.

This document is not complete. It is currently a living document to reach working agreements and technical solutions between suppliers. So some things will change in the coming months. In addition, this document is also an index: in many places it will refer to existing standards and other documentation. In this way we keep this document concise and readable, and we can also reuse the documentation we refer to for other Applications on Nuts.

We hope you enjoy reading it, and if this document raises any questions, we would be happy to [answer](https://nuts.nl/contact/)https://nuts.nl/contact/ them.

## 1.1 Use cases
The application on Nuts "TA Notified Pull on Nuts" is generic in nature and offers support for multiple use cases. Examples of supported use cases are medical specialist referral (BgZ-referral), medication prescription and other cross-organizational workflow requests. Applying the application on Nuts "TA Notified Pull on Nuts" to a specific use case takes place on the basis of a use-case-profile. The use-case-profile is documented separately and describes, among other things, the governance, the information standards, the permitted authentication means, the permitted legal bases and the access policy of the use case. 

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
  HL7 has described a FHIR workflow management communication pattern in which a Task-resource is created on the placer's system. TA Notified Pull on Nuts complies to this pattern and provides an implementation guide for the digital interactions between actor Placer and actor Filler.

## 1.3 Key differences with TTA FHIR - Notified pull
- All references to TTA FHIR - Authentication & Authorization have to be ignored and replaced by the information provided in this document
- All references to TTA FHIR - Addressing have to be ignored and replaced by the information provided in this document
- In TTA FHIR - Notified pull the presence of the "Workflow Task" is optional. In TA Notified Pull on Nuts the presence of the "Workflow Task" is mandatory.

## 1.4 Glossary
- Placer: The professional that has a request. The requester is referred to as the "placer" and the performer is referred to as the "filler", which are often seen as order-specific terms. However, in this context, the terms hold whether the request is expressed as a proposal, plan or full-blown order.
- Filler: The professional that is requested to perform an action. The requester is referred to as the "placer" and the performer is referred to as the "filler", which are often seen as order-specific terms. However, in this context, the terms hold whether the request is expressed as a proposal, plan or full-blown order.
- Nuts: A partnership of parties in healthcare to create a broadly supported, open, decentralized infrastructure for the exchange of data in healthcare and the medical domain. See www.nuts.nl.
- Application on Nuts — A practical application of the Nuts philosophy and open technology to enable a tangible use case in healthcare (formerly called "Bolt").
- Data holder / Placer organization: The healthcare institution from which the patient is referred. From the perspective of the BgZ referral, the organization that has patient data that needs to be transferred.
- Placer system: The software system that manages the data holder's data.
- Patient: The patient that is subject of the request
- Data user / Filler organization: The healthcare institution that receives the request, and therefore has an information need for data from the data holder.
- Filler System — The software system that manages the recipient organization's data.
- Legal base — A legal base for being allowed to break the professional secrecy of the data holder.

# 2. Proces description
## 2.1 Exchange of workflow information
The generic process of exchanging workflow information is described in paragraph "[steps](https://www.hl7.org/fhir/workflow-management.html#12.12.1.1)" of HL7's Workflow Management Communication Patterns option F. Following

## 2.2 Exchange of medical record data
The filler may need medical record data stored at the filler to perform the request.

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

The GDPR (Article 9(1) of the GDPR and Article 22(1) of the UAVG) stats that personal data and special (medical) personal data may not simply be processed. This concerns both the placer (data holder) and the filler (data user). The GDPR lists 6 grounds for processing:
1. consent of the person concerned (patient)
2. execution of an agreement
3. legal obligation
4. vital interests of the person concerned (patient)
5. performing a public law task
6. legitimate interest of the organization
The placer (data holder) is subject to legal obligation, which is included in the WGBO. Things are a little less simple for the filler (data user).
If there is agreement as to who will be the filler or filler organization, and the patient has already given consent for the request from placer to filler, the WGBO applies.
The WGBO states that a care provider may assume a patient's consent (implicit consent) to provide his or her patient data when that care provider sends the patient to another care provider for a current care need and provides patient data for this purpose (more details can be found in the report "[Implementatie van de WGBO Deel 4](https://www.knmg.nl/download/implementatie-van-de-wgbo-deel-4-toegang-tot-patientengegevens#:~:text=wet%20naar%20praktijk.-,Implementatie%20van%20de%20WGBO.,king%20met%20het%20NICTIZ%20ontwikkeld.)", chapter chapter 2.2.5.

## 3.3 Security and trust
to do



