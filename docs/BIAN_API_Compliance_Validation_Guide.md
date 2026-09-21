BIAN API Compliance Validation Guide & Checklist

This document serves as a comprehensive framework and checklist for evaluating Application Programming Interfaces (APIs) against the Banking Industry Architecture Network (BIAN) standards. Ensuring BIAN compliance enables modular modernization, aligns with the Coreless Banking initiative, and establishes a standardized semantic language across financial services.

1. Architectural Alignment & Service Domains

The foundation of any BIAN-compliant API is its strict adherence to the BIAN Service Landscape. BIAN breaks down banking capabilities into discrete, mutually exclusive Service Domains. To be compliant, an API must not blur the boundaries between these domains.





1:1 Mapping: The API must be scoped to exactly one BIAN Service Domain (e.g., Customer Offer, Payment Execution, or Consumer Loan).



No Overlap: The API cannot expose functionalities or alter states that belong to the Control Record of a different Service Domain.



Decoupled Integration: Cross-domain communication must happen via standardized API calls or event streaming, not via direct database integration.



2. Semantic Structure: Control Records and Action Terms

BIAN APIs are semantic—they describe what banking activities must accomplish, independent of underlying legacy technologies. This is achieved through the Control Record (CR) and standard Action Terms.





Control Record (CR): The core state entity managed by the Service Domain. The API must center around lifecycle operations on this CR.



Behavior Qualifiers (BQs): Optional sub-components or specific features of the Control Record that can be accessed or modified independently.



Action Term to HTTP Method Mapping

BIAN standardizes the functional verbs (Action Terms) applied to a Control Record. A compliant API maps these semantic terms directly to RESTful HTTP methods.







BIAN Action Term



HTTP Method



Semantic Definition





Initiate



POST



Instantiates a new Control Record instance.





Update



PUT / PATCH



Modifies an existing Control Record or Behavior Qualifier.





Retrieve



GET



Fetches the current state/details of a Control Record.





Execute



POST



Triggers an automated action or calculation within the domain.





Request



POST / PUT



Submits a request for a service or authorization.





Control



PUT



Alters the processing status or governing rules of a CR.



3. Data Payload and Business Object Model (BOM)

To pass compliance, the API's JSON schemas must align with the BIAN Business Object Model (BOM). The BOM defines the standardized information structures required for every Service Domain. When applicable, the BIAN BOM incorporates industry-wide data structures like ISO 20022.

4. Security and FAPI Alignment

While BIAN focuses on business semantics, modern adoption—especially within Open Banking—requires strict security compliance. A BIAN API implementation should conform to Financial-grade API (FAPI) standards. This provides a secure model for user authentication via JSON Web Tokens (JWT) and closes security loopholes associated with standard OAuth 2.0 requests.

5. BIAN API Compliance Master Checklist

Use the following checklist during the API design review (or automated linting process) to verify full BIAN semantic compliance.







Check ID



Category



Validation Criteria



Audit Status





CHK-001



Architecture



API is mapped exclusively to one specific BIAN Service Domain.



[ ] Pass [ ] Fail





CHK-002



Architecture



API does not expose or mutate data belonging to another Service Domain's Control Record.



[ ] Pass [ ] Fail





CHK-003



Semantics



Endpoint URIs accurately reflect the Control Record (CR) and optional Behavior Qualifiers (BQ).



[ ] Pass [ ] Fail





CHK-004



Semantics



HTTP methods match official BIAN Action Terms (e.g., POST for Initiate/Execute, GET for Retrieve).



[ ] Pass [ ] Fail





CHK-005



Data Model



Request and Response JSON payloads are derived directly from the BIAN Business Object Model (BOM).



[ ] Pass [ ] Fail





CHK-006



Standardization



API is documented using OpenAPI Specification (OAS) 3.0 or higher.



[ ] Pass [ ] Fail





CHK-007



Security



API endpoints are secured according to FAPI and Open Banking standards (JWT, mutual TLS).



[ ] Pass [ ] Fail



6. Example: Structuring a Compliant Endpoint URI

According to BIAN design principles, a URI should logically reflect the Domain, Control Record, and Behavior Qualifier. Consider a Consumer Loan domain.

// Pattern: /{Service-Domain}/{Control-Record}/{cr-reference-id}/{Behavior-Qualifier}/{bq-reference-id}

// 1. INITIATE a new Consumer Loan (Action Term: Initiate -> POST)
POST /consumer-loan/loan-arrangement

// 2. RETRIEVE the loan details (Action Term: Retrieve -> GET)
GET /consumer-loan/loan-arrangement/{loan-id}

// 3. UPDATE collateral details on the loan (Action Term: Update -> PUT)
PUT /consumer-loan/loan-arrangement/{loan-id}/collateral/{collateral-id}

Note: This checklist serves as an architectural governance tool. Teams should continuously reference the latest definitions in the BIAN Service Landscape and GitHub API repositories to ensure ongoing synchronization with global standards.
