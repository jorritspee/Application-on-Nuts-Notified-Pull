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
 
- *Nuts-use-case-profile "bgz-referral"*
  The Nuts-use-case-profile "bgz-referral" describes how to use the specification 'TA-Notified-Pull-on-Nuts' in the context of a medical specialist referral (commonly reffered to in Dutch as a BgZ-verwijzing).

## 1.3 Key differences with TTA FHIR - Notified pull
- All references to TTA FHIR - Authentication & Authorization have to be ignored and replaced by the information provided in this document
- All references to TTA FHIR - Addressing have to be ignored and replaced by the information provided in this document
- In TTA FHIR - Notified pull the presence of the "Workflow Task" is optional. In TA Notified Pull on Nuts the presence of the "Workflow Task" is mandatory.


