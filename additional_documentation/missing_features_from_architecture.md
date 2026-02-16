# Missing Features in draft-wullink-rpp-core.md Based on Architecture Document

This document lists features described in `draft-ietf-rpp-architecture-01.adoc` that are missing from `draft-wullink-rpp-core.md`.

Generated: 2026-02-16

## HTTP Transport Layer Issues

### Issue 1: Transport Security Requirements
**Priority: High**
**Architecture Reference:** Section 5.1.1 (Transport Security)

**Missing:**
- Mandatory TLS/HTTPS requirement for all RPP communication
- Security considerations for data in transit
- Protection against eavesdropping, tampering, and MITM attacks
- Reference to TLS standards and best practices

**Recommendation:**
Add a section in Security Considerations specifying that:
- All RPP communication MUST use HTTPS with TLS
- Specific TLS version requirements
- Reference to current TLS best practices

---

### Issue 2: Authentication and Authorization Framework
**Priority: High**
**Architecture Reference:** Section 5.1.2 (Authentication and Authorisation)

**Missing:**
- OAuth 2.0 support and framework
- HTTP Basic Authentication specification for EPP compatibility
- Authorization scopes (e.g., rpp:read, rpp:write)
- Fine-grained authorization beyond simple auth-codes
- Relationship between login credentials and RPP client context
- Object-level authorization mechanisms beyond basic authinfo
- Support for multiple credentials per RPP client
- OAuth scope parameter for client context binding

**Recommendation:**
Add sections covering:
1. Authentication Methods
   - OAuth 2.0 Bearer Token authentication
   - HTTP Basic Authentication for backward compatibility
   - Future authentication scheme support
2. Authorization Scopes
   - Define standard scopes (rpp:read, rpp:write, resource-specific scopes)
   - Scope syntax and semantics
3. Fine-Grained Authorization
   - Operation-based authorization
   - Resource-based authorization
   - Attribute-based authorization
4. Client-Credential Relationships
   - One credential to one RPP client binding
   - Multiple credentials per RPP client support
   - OAuth scope-based client context selection

---

### Issue 3: Resource Addressing Details
**Priority: Medium**
**Architecture Reference:** Section 5.1.3 (Resource Addressing)

**Missing:**
- Internationalized Domain Names (IDN) handling in URLs
- UTF-8 encoding vs. IDN encoding in resource URLs
- Redirects to canonical URLs or "see-also" linking for IDN alternatives
- Relative URL support and discovery
- Resource relationship links in responses
- URL determinism requirements

**Recommendation:**
Add section on:
1. IDN Handling
   - URL encoding requirements (UTF-8 vs. Punycode)
   - Canonical URL approach (redirect vs. see-also links)
   - Examples of IDN domain resource URLs
2. URL Structure
   - Relative vs. absolute URLs
   - Link headers for related resources
   - URL stability guarantees

---

### Issue 4: Complete HTTP Verb Mapping
**Priority: High**
**Architecture Reference:** Section 5.1.4 (Mapping of basic operations)

**Missing:**
- HEAD method semantics and usage
- OPTIONS method and CORS pre-flight considerations
- PUT method for full resource replacement
- Distinction between PUT (full replacement) and PATCH (partial update)
- Clarification that HEAD should not be overloaded with EPP check semantics
- Guidance on avoiding HEAD for availability checks

**Recommendation:**
Add detailed specifications for:
1. HEAD Method
   - Retrieve metadata without body
   - Same headers as GET
   - Not equivalent to EPP check command
2. OPTIONS Method
   - CORS pre-flight handling
   - Capability discovery per resource
3. PUT Method
   - Full resource replacement semantics
   - Difference from PATCH (partial update)
   - Use cases and examples

---

### Issue 5: HTTP Caching Support
**Priority: Medium**
**Architecture Reference:** Section 5.1.7 (Caching)

**Missing:**
- HTTP caching mechanisms and policies
- Cache-Control headers usage
- ETag support for conditional requests
- Caching policies for different resource types and operations
- Versioning through ETags

**Recommendation:**
Add section on HTTP Caching:
1. Cache-Control directives for different endpoints
2. ETag generation and validation
3. Conditional requests (If-None-Match, If-Match)
4. Resource-specific caching policies
5. Examples of cacheable vs. non-cacheable operations

---

### Issue 6: Language Negotiation
**Priority: Low**
**Architecture Reference:** Section 5.1.8 (Language negotiation)

**Missing:**
- Detailed Accept-Language header usage beyond examples
- Server multi-language support requirements
- Default language specification
- Mechanisms for indicating supported languages (OPTIONS, HEAD)
- Multi-language representation support in application/rpp+json
- Language handling for write operations with user-provided content

**Recommendation:**
Add section covering:
1. Language Negotiation
   - Accept-Language header syntax and semantics
   - Server language support discovery
   - Default language behavior
2. Multi-Language Representations
   - Structure for multi-language content in JSON
   - Language-specific validations

---

### Issue 7: Client Signaling for Response Verbosity
**Priority: Medium**
**Architecture Reference:** Section 5.1.9 (Client Signalling for Response Verbosity)

**Missing:**
- Prefer header with "return" preference
- return=minimal for reduced payloads
- return=representation for full responses
- Default behavior without Prefer header
- Custom preference for dereferenced related objects
- IANA HTTP Preferences registry registration

**Recommendation:**
Add section on Response Verbosity Control:
1. Prefer Header Usage
   - return=minimal for lightweight responses
   - return=representation (default) for full resource data
2. Custom Preferences
   - Dereferencing related objects in responses
   - Preference syntax and registration
3. Examples showing different verbosity levels

---

### Issue 8: Client Signaling for Request Validation
**Priority: Medium**
**Architecture Reference:** Section 5.1.10 (Client Signalling for Request Validation)

**Missing:**
- Prefer header for validation mode
- Strict validation mode (reject unknown properties)
- Lenient validation mode (ignore unknown properties)
- Default validation behavior
- Extensibility implications

**Recommendation:**
Add section on Request Validation Preferences:
1. Strict Mode (default)
   - Reject requests with unknown properties
   - Ensures forward compatibility
2. Lenient Mode
   - Ignore unknown properties
   - Allows graceful degradation
3. Prefer header syntax and examples

---

### Issue 9: Asynchronous Operation Processing Details
**Priority: Medium**
**Architecture Reference:** Section 5.1.11 (Asynchronous Operation Processing)

**Missing:**
- Comprehensive asynchronous operation pattern beyond basic processes
- HTTP 202 Accepted status code usage
- Status resource lifecycle and retention policies
- Expected completion time signaling
- Progress indication for long-running operations
- Multiple granularity levels of status information
- Different status resource patterns (dedicated, subresource, queue)
- Explicit vs. implicit resource lifetime management

**Recommendation:**
Enhance the Processes section with:
1. Asynchronous Patterns
   - HTTP 202 Accepted response pattern
   - Status resource design options
2. Status Information
   - Progress indication
   - Estimated completion time
   - Intermediate vs. final status
3. Resource Lifecycle
   - Automatic vs. manual status resource deletion
   - Retention policies

---

### Issue 10: Transaction Tracing and Idempotency
**Priority: High**
**Architecture Reference:** Section 5.1.13 (Transaction tracing and idempotency)

**Missing:**
- Idempotency mechanisms for safe request retries
- Client-provided identifier lifetime and uniqueness requirements
- Server transaction identifier generation for all operations
- Idempotency-Key header or similar mechanism
- Duplicate request detection and handling
- Transaction correlation across asynchronous operations

**Recommendation:**
Add section on Transaction Management:
1. Transaction Identifiers
   - Server-generated unique IDs for all transactions
   - Client transaction ID (already have RPP-Cltrid)
2. Idempotency
   - Idempotency-Key header introduction
   - Duplicate detection window
   - Safe retry mechanisms
   - Examples of idempotent operations

---

### Issue 11: Protocol Versioning
**Priority: High**
**Architecture Reference:** Section 5.1.14 (Protocol Versioning)

**Missing:**
- Protocol versioning schema (e.g., Semantic Versioning)
- Extension versioning
- Profile versioning
- Version negotiation mechanism
- Media type parameters for version signaling
- Backward compatibility requirements
- Breaking vs. non-breaking changes

**Recommendation:**
Add section on Versioning:
1. Versioning Schema
   - Semantic Versioning for protocol, extensions, profiles
   - Version format and semantics
2. Version Signaling
   - Media type parameters (e.g., application/rpp+json;version=1.0)
   - Version negotiation during capability discovery
3. Compatibility
   - Forward and backward compatibility rules
   - Handling version mismatches

---

### Issue 12: Profile Support
**Priority: Medium**
**Architecture Reference:** Section 5.1.15 (Profiles)

**Missing:**
- Profile concept and definition
- Profile as a set of protocol version + extensions + versions
- Profile versioning
- Profile IANA registry
- Machine-readable profile definitions
- Profile signaling via media type parameters
- Use cases for profiles (operational requirements, external policies)

**Recommendation:**
Add section on Profiles:
1. Profile Definition
   - What constitutes a profile
   - Profile components (protocol version, extensions, features)
2. Profile Registration
   - IANA registry for standard profiles
   - Profile identifier format
3. Profile Signaling
   - Media type parameters
   - Service discovery
4. Profile Compliance
   - Client and server profile support
   - Profile selection and negotiation

---

### Issue 13: Service Discovery Mechanisms
**Priority: High**
**Architecture Reference:** Section 5.1.18 (Service discovery mechanisms)

**Missing:**
- Well-known URI for service discovery (/.well-known/rpp-capabilities)
- Bootstrap mechanism for locating RPP server (IANA bootstrap, DNS TXT)
- Service discovery document structure and content
- Advertising:
  - Supported protocol versions
  - Available extensions
  - Resource types
  - Authentication methods
  - IDN policies
  - Supported features
  - Maintenance notices
- URI Templates for resource navigation
- Distributed service discovery per resource type
- Static vs. dynamic configuration principle

**Recommendation:**
Add major section on Service Discovery:
1. Bootstrap Mechanisms
   - IANA bootstrap service registry
   - DNS TXT records for service location
2. Discovery Document
   - /.well-known/rpp-capabilities endpoint
   - Document structure and schema
   - Required vs. optional fields
3. Capabilities Advertising
   - Protocol and extension versions
   - Supported resource types
   - Authentication methods
   - Features and profiles
4. URI Templates
   - Template-based resource navigation
   - Reducing hard-coded URLs
5. Examples of discovery document

---

### Issue 14: Scalability Considerations
**Priority: Low**
**Architecture Reference:** Section 5.1.19 (Scalability)

**Missing:**
- Leveraging HTTP for scalability (load balancing, horizontal scaling)
- Distributed caching support
- Stateless interaction benefits
- DoS attack mitigation design
- Standard web security mechanisms

**Recommendation:**
Add section in Architecture or Design Considerations:
1. Scalability Through HTTP
   - Load balancer compatibility
   - Horizontal scaling approach
   - CDN and caching integration
2. Security Scalability
   - DoS mitigation strategies
   - Rate limiting (future consideration)

---

### Issue 15: Special Resources and Metadata Endpoints
**Priority: Low**
**Architecture Reference:** Section 5.1.17 (Definition of special resources)

**Missing:**
- Metadata endpoints for protocol-level information
- OpenAPI definition endpoints for documentation and code generation
- Schema information endpoints
- Distinction between service discovery and metadata resources

**Recommendation:**
Add section on Special Endpoints:
1. Metadata Endpoints
   - Schema retrieval
   - OpenAPI specification endpoint
   - Machine-readable documentation
2. Purpose and usage of special resources
3. Examples

---

## Data Representation Layer Issues

### Issue 16: Data Structure Options
**Priority: Medium**
**Architecture Reference:** Section 5.2.1 (Data structure)

**Missing:**
- Definition of RPP data structure as default
- Potential support for EPP structure adaptation
- Potential support for JSContact structure
- Potential support for Verifiable Credentials structure
- Abstraction between data structure and transport format
- Structure versioning

**Recommendation:**
Add section on Data Structures:
1. Default RPP Structure
   - Define the native RPP data structure
   - Schema definition approach
2. Alternative Structures (Future)
   - EPP compatibility structure
   - JSContact for contact data
   - Verifiable Credentials for identity
3. Structure Selection
   - How clients request different structures
   - Backward compatibility

---

### Issue 17: Data Format Support
**Priority: Low**
**Architecture Reference:** Section 5.2.2 (Data format)

**Missing:**
- Primary JSON format specification
- Potential XML support (EPP compatibility)
- Potential JWT encapsulation for signed data
- Potential JWT-SD for selective disclosure
- Potential CBOR for binary encoding
- Encapsulation vs. structure distinction
- Format negotiation via Content-Type

**Recommendation:**
Add section on Data Formats:
1. Primary Format: JSON
   - JSON encoding requirements
   - application/rpp+json media type
2. Future Format Support
   - XML (application/rpp+xml)
   - JWT encapsulation
   - CBOR for compact representation
3. Format Negotiation
   - Content-Type and Accept headers
   - Format capabilities discovery

---

### Issue 18: Data Validation and Schema
**Priority: Medium**
**Architecture Reference:** Section 5.2.4 (Data Validation)

**Missing:**
- Schema language specification (JSON Schema, OpenAPI, CDDL)
- Data validation requirements for clients and servers
- Strict vs. lenient processing modes
- Extensibility support in schemas
- Schema publication and versioning

**Recommendation:**
Add section on Data Validation:
1. Schema Definition
   - JSON Schema as primary schema language
   - OpenAPI specification integration
2. Validation Modes
   - Strict: reject unknown properties
   - Lenient: ignore unknown properties
3. Schema Availability
   - Where clients can retrieve schemas
   - Schema versioning
4. Extensibility
   - Extension points in schemas
   - Additional properties handling

---

### Issue 19: Media Type Definition and Parameters
**Priority: High**
**Architecture Reference:** Section 5.2.5 (Media Type definition)

**Missing:**
- Complete application/rpp+json media type specification
- Media type parameters for:
  - Version signaling
  - Profile selection
  - Structure specification
- Alternative media types (application/epp+xml, etc.)
- Media type registration requirements
- Content negotiation details

**Recommendation:**
Add section on Media Types:
1. Primary Media Type: application/rpp+json
   - MIME type registration
   - Parameters: version, profile, structure
2. Alternative Media Types
   - application/epp+xml for EPP compatibility
   - Future media types
3. Content Negotiation
   - Accept header usage
   - Quality values
   - Default media type
4. Examples with media type parameters

---

## Resource Definition Layer Issues

### Issue 20: Data Elements Abstraction
**Priority: Medium**
**Architecture Reference:** Section 5.3.1 (Data Elements)

**Missing:**
- Logical data element definitions independent of representation
- Data element IANA registry
- Data element identification (stable identifiers)
- Data element constraints (type, length, allowed values)
- Data element reuse across resource types
- Extensibility mechanisms for data elements

**Recommendation:**
Add section on Data Elements:
1. Data Element Abstraction
   - Logical vs. representational separation
   - Stable identifiers for data elements
2. Data Element Definition
   - Format and schema for primitive elements
   - References to other resource types
   - Constraints specification
3. IANA Registry
   - Registration process
   - Machine-readable format
4. Reusability
   - Shared data elements across resources

---

### Issue 21: Mapping Layer
**Priority: Medium**
**Architecture Reference:** Section 5.3.2 (Mapping)

**Missing:**
- Mapping between logical data elements and media type representations
- JSON Patch or similar mechanisms for defining mappings
- Support for external data formats (JSContact, VC)
- Mapping versioning and evolution
- IANA registry for mappings

**Recommendation:**
Add section on Data Element Mapping:
1. Mapping Definition
   - Logical to representational mapping
   - Mapping specification format
2. External Format Integration
   - Mapping RPP elements to JSContact
   - Mapping to Verifiable Credentials
3. Mapping Registry
   - IANA registration
   - Machine-readable mapping definitions
4. Examples of mappings

---

### Issue 22: Operations Abstraction and Registry
**Priority: Low**
**Architecture Reference:** Section 5.3.3 (Operations)

**Missing:**
- Abstract operation definitions per resource type
- Operation constraints and requirements
- Operations IANA registry
- Machine-readable operation definitions
- Extensibility for new operations

**Recommendation:**
Add section on Operations:
1. Operation Definition
   - Supported operations per resource type
   - Operation parameters and constraints
2. IANA Registry
   - Registration process
   - Machine-readable format
3. Custom Operations
   - Defining new operations
   - Extension operation registration

---

## Extension Framework Issues

### Issue 23: Comprehensive Extension Mechanisms
**Priority: High**
**Architecture Reference:** Section 5.4 (Extension mechanisms)

**Missing:**
- Layered extension approach
- IANA registries for all extension elements
- Resource type extensions
- Data element extensions
- Operation extensions
- Status code extensions
- Profile-based compatibility
- Discovery and negotiation of extensions
- Extension versioning

**Recommendation:**
Add major section on Extension Framework:
1. Extension Principles
   - Layered design for extensions
   - Independent evolution of layers
2. Extension Types
   - Resource type extensions
   - Data element extensions
   - Operation extensions
   - Status code extensions
3. Extension Registration
   - IANA registry requirements
   - Machine-readable formats
4. Extension Discovery
   - Service discovery integration
   - Client negotiation
5. Examples of extensions

---

### Issue 24: Name Management and Collision Avoidance
**Priority: Medium**
**Architecture Reference:** Section 5.4.1 (Name Management)

**Missing:**
- Unique naming requirements for extensions
- IANA registry for standardized extensions
- Private extension naming conventions (reverse domain notation)
- Collision avoidance mechanisms
- Naming in resource identifiers, data elements, and URL paths

**Recommendation:**
Add section on Extension Naming:
1. Naming Requirements
   - Unique names for all extension elements
   - Consistent usage across identifiers
2. Standardized Extensions
   - IANA registration requirement
   - Global uniqueness guarantees
3. Private Extensions
   - Reverse domain notation (org.example.rpp)
   - Development and deployment without IANA
4. Collision Prevention
   - Name reservation process
   - Conflict resolution

---

### Issue 25: Extension Security
**Priority: High**
**Architecture Reference:** Section 5.4.2 (Extension Security)

**Missing:**
- Security framework for extensions
- Requirements that extensions use core security mechanisms
- Prohibition on bypassing authentication/authorization
- Uniform security application across core and extensions

**Recommendation:**
Add section on Extension Security:
1. Security Framework
   - Extensions MUST use core security mechanisms
   - No separate authentication channels
2. Security Review
   - Extension security validation
   - Common security vulnerabilities
3. Guidelines
   - Secure extension development
   - Authorization scope extensions

---

### Issue 26: Extension Review Process
**Priority: Medium**
**Architecture Reference:** Section 5.4.3 (Extension Review)

**Missing:**
- Expert review requirement for IANA registration
- Review criteria
- Security consideration verification
- Integration validation
- Reference to RFC 8126 BCP for IANA considerations

**Recommendation:**
Add section on Extension Review:
1. Review Process
   - Expert review requirement
   - Review criteria checklist
2. Security Verification
   - Security framework compliance
   - Vulnerability assessment
3. IANA Considerations
   - Registration requirements
   - Documentation standards
   - Reference to RFC 8126

---

## Summary Statistics

**Total Issues Identified:** 26

**By Priority:**
- High: 10 issues
- Medium: 12 issues
- Low: 4 issues

**By Category:**
- HTTP Transport Layer: 15 issues
- Data Representation Layer: 4 issues
- Resource Definition Layer: 3 issues
- Extension Framework: 4 issues

---

## Recommended Action Plan

### Phase 1 (Critical - Address First)
1. Issue 1: Transport Security Requirements
2. Issue 2: Authentication and Authorization Framework
3. Issue 4: Complete HTTP Verb Mapping
4. Issue 10: Transaction Tracing and Idempotency
5. Issue 11: Protocol Versioning
6. Issue 13: Service Discovery Mechanisms
7. Issue 19: Media Type Definition and Parameters
8. Issue 23: Comprehensive Extension Mechanisms
9. Issue 25: Extension Security

### Phase 2 (Important - Address Second)
1. Issue 3: Resource Addressing Details
2. Issue 5: HTTP Caching Support
3. Issue 7: Client Signaling for Response Verbosity
4. Issue 8: Client Signaling for Request Validation
5. Issue 9: Asynchronous Operation Processing Details
6. Issue 12: Profile Support
7. Issue 16: Data Structure Options
8. Issue 18: Data Validation and Schema
9. Issue 20: Data Elements Abstraction
10. Issue 21: Mapping Layer
11. Issue 24: Name Management and Collision Avoidance
12. Issue 26: Extension Review Process

### Phase 3 (Nice to Have - Address Later)
1. Issue 6: Language Negotiation
2. Issue 14: Scalability Considerations
3. Issue 15: Special Resources and Metadata Endpoints
4. Issue 17: Data Format Support
5. Issue 22: Operations Abstraction and Registry

---

## Notes

- This analysis compares draft-ietf-rpp-architecture-01.adoc (dated 2025-11-06) with draft-wullink-rpp-core-03.md
- The core document currently focuses on endpoint definitions and basic HTTP operations
- The architecture document provides comprehensive guidance that should be reflected in the protocol specification
- Many architectural decisions need to be translated into concrete protocol requirements
- Consider whether some items belong in the core document or in separate companion documents (e.g., security, discovery)

---

## References

- Architecture Document: /Users/maarten/sidn/development/git/RPP-architecture/draft-ietf-rpp-architecture-01.adoc
- Core API Document: /Users/maarten/sidn/development/git/ietf-rpp-core/src/draft-wullink-rpp-core.md
- RPP Requirements: draft-ietf-rpp-requirements-03
