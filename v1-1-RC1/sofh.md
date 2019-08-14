![](media/image1.jpg)

# FIX Simple Open Framing Header Technical Specification

Version 1.1 Release Candidate 1

July 2019

**THIS DOCUMENT IS A RELEASE CANDIDATE FOR A PROPOSED FIX TECHNICAL
STANDARD. A RELEASE CANDIDATE HAS BEEN APPROVED BY THE GLOBAL TECHNICAL
COMMITTEE AS AN INITIAL STEP IN CREATING A NEW FIX TECHNICAL STANDARD.
POTENTIAL ADOPTERS ARE STRONGLY ENCOURAGED TO BEGIN WORKING WITH THE
RELEASE CANDIDATE AND TO PROVIDE FEEDBACK TO THE GLOBAL TECHNICAL
COMMITTEE AND THE WORKING GROUP THAT SUBMITTED THE PROPOSAL. THE
FEEDBACK TO THE RELEASE CANDIDATE WILL DETERMINE IF ANOTHER REVISION AND
RELEASE CANDIDATE IS NECESSARY OR IF THE RELEASE CANDIDATE CAN BE
PROMOTED TO BECOME A FIX TECHNICAL STANDARD DRAFT.**

DISCLAIMER

THE INFORMATION CONTAINED HEREIN AND THE FINANCIAL INFORMATION EXCHANGE
PROTOCOL (COLLECTIVELY, THE "FIX PROTOCOL") ARE PROVIDED "AS IS" AND NO
PERSON OR ENTITY ASSOCIATED WITH THE FIX PROTOCOL MAKES ANY
REPRESENTATION OR WARRANTY, EXPRESS OR IMPLIED, AS TO THE FIX PROTOCOL
(OR THE RESULTS TO BE OBTAINED BY THE USE THEREOF) OR ANY OTHER MATTER
AND EACH SUCH PERSON AND ENTITY SPECIFICALLY DISCLAIMS ANY WARRANTY OF
ORIGINALITY, ACCURACY, COMPLETENESS, MERCHANTABILITY OR FITNESS FOR A
PARTICULAR PURPOSE. SUCH PERSONS AND ENTITIES DO NOT WARRANT THAT THE
FIX PROTOCOL WILL CONFORM TO ANY DESCRIPTION THEREOF OR BE FREE OF
ERRORS. THE ENTIRE RISK OF ANY USE OF THE FIX PROTOCOL IS ASSUMED BY THE
USER.

NO PERSON OR ENTITY ASSOCIATED WITH THE FIX PROTOCOL SHALL HAVE ANY
LIABILITY FOR DAMAGES OF ANY KIND ARISING IN ANY MANNER OUT OF OR IN
CONNECTION WITH ANY USER'S USE OF (OR ANY INABILITY TO USE) THE FIX
PROTOCOL, WHETHER DIRECT, INDIRECT, INCIDENTAL, SPECIAL OR CONSEQUENTIAL
(INCLUDING, WITHOUT LIMITATION, LOSS OF DATA, LOSS OF USE, CLAIMS OF
THIRD PARTIES OR LOST PROFITS OR REVENUES OR OTHER ECONOMIC LOSS),
WHETHER IN TORT (INCLUDING NEGLIGENCE AND STRICT LIABILITY), CONTRACT OR
OTHERWISE, WHETHER OR NOT ANY SUCH PERSON OR ENTITY HAS BEEN ADVISED OF,
OR OTHERWISE MIGHT HAVE ANTICIPATED THE POSSIBILITY OF, SUCH DAMAGES.

**DRAFT OR NOT RATIFIED PROPOSALS** (REFER TO PROPOSAL STATUS AND/OR
SUBMISSION STATUS ON COVER PAGE) ARE PROVIDED "AS IS" TO INTERESTED
PARTIES FOR DISCUSSION ONLY. PARTIES THAT CHOOSE TO IMPLEMENT THIS DRAFT
PROPOSAL DO SO AT THEIR OWN RISK. IT IS A DRAFT DOCUMENT AND MAY BE
UPDATED, REPLACED, OR MADE OBSOLETE BY OTHER DOCUMENTS AT ANY TIME. THE
FIX GLOBAL TECHNICAL COMMITTEE WILL NOT ALLOW EARLY IMPLEMENTATION TO
CONSTRAIN ITS ABILITY TO MAKE CHANGES TO THIS SPECIFICATION PRIOR TO
FINAL RELEASE. IT IS INAPPROPRIATE TO USE FIX WORKING DRAFTS AS
REFERENCE MATERIAL OR TO CITE THEM AS OTHER THAN “WORKS IN PROGRESS”.
THE FIX GLOBAL TECHNICAL COMMITTEE WILL ISSUE, UPON COMPLETION OF REVIEW
AND RATIFICATION, AN OFFICIAL STATUS ("APPROVED") OF/FOR THE PROPOSAL
AND A RELEASE NUMBER.

No proprietary or ownership interest of any kind is granted with respect
to the FIX Protocol (or any rights therein).

Copyright 2014-2019 FIX Protocol Ltd., all rights reserved.

<a rel="license" href="http://creativecommons.org/licenses/by-nd/4.0/"><img alt="Creative Commons License" style="border-width:0" src="https://i.creativecommons.org/l/by-nd/4.0/88x31.png" /></a><br /><span xmlns:dct="http://purl.org/dc/terms/" href="http://purl.org/dc/dcmitype/Text" property="dct:title" rel="dct:type">FIX Simple Open Framing Header Technical Specification</span> by <a xmlns:cc="http://creativecommons.org/ns#" href="http://www.fixtradingcommunity.org/" property="cc:attributionName" rel="cc:attributionURL">FIX Protocol Ltd.</a> is licensed under a <a rel="license" href="http://creativecommons.org/licenses/by-nd/4.0/">Creative Commons Attribution-NoDerivatives 4.0 International License</a>.<br />Based on a work at <a xmlns:dct="http://purl.org/dc/terms/" href="https://github.com/FIXTradingCommunity/fix-simple-open-framing-header" rel="dct:source">https://github.com/FIXTradingCommunity/fix-simple-open-framing-header</a>.

Introduction
============

The FIX High Performance Working Group set about defining a set of additional concrete encodings. The intent of these encodings was to efficiently communicate the FIX trading protocol. A decision was taken early on that none of these encodings be bound in and of themselves solely to the use of FIX Protocol. A problem and a requirement arose during the development of these additional encodings. What mechanism could be provided that would permit message processors, such as network protocol analyzers and heterogeneous communication gateways, to determine an application message boundary and the encoding of that message. After considerable deliberation, an approach was selected to create a simple and primitive message framing header that would communicate two pieces of information, the length of a message and the encoding type of that message. Additional requirements were identified. The goal was to make the framing header open and available to support existing and future encoding types and have the ability to reserve a set of encoding types to permit user defined encodings. The FIX Simple Open Framing Header (“the SOF Header”) we believe meets these requirements.

Authors
-------

| **Name**           | **Affiliation**                   | **Role**       |
|--------------------|-----------------------------------|----------------|
| Northey, Jim       | The LaSalle Technology Group, LLC | Author, Editor |
| Furuhed, Anders    | Pantor Engineering                | Author         |
| Mendelson, Don     | Silver Flash LLC                  | Author, Editor |
| Kapur, Aditya      | CME Group, Inc.                   | Contributor    |
| Malatestinic, Greg | Jordan & Jordan                   | Contributor    |
| Malabre, Fred      | CME Group, Inc.                   | Contributor    |
| Klein, Hanno       | Deutsche Boerse Group             | Contributor    |
| Andersson, Rolf    | Pantor Engineering                | Contributor    |

Requirements
============

Business Requirements
---------------------

Solution shall be open to support existing and future encoding types.

Solution shall permit identification of new versions of encodings.

Solution shall support FIX and non-FIX encodings.

Technical Requirements
----------------------

Provide a simple mechanism for message processing application to identify the length of a message.

Provide a simple mechanism for message processing applications to identify the encoding of the message.

Provide a mechanism to inventory and publish a list of encoding types.

Issues and Discussion Points
============================

NONE

Relevant and Related Standards
==============================

| **Related Standard** | **Version**      | **Reference location** | **Relationship**                                     | **Normative** 
|----------------------|------------------|------------------------|------------------------------------------------------|---------------|
| SBE                  | 1.0              |                        | SOF Header can be used with SBE                      |               |
| FIX GPB              | 1.0              |                        | SOF Header can be used with FIX encoding using GPB   |               |
| FIX                  | 4.2, 4.4, 5.0SP2 |                        | SOF Header can be used with FIX Tag=value encodings  |               |
| FAST                 | 1.0, 1.1, 1.2    |                        | SOF Header can be used with FIX encoding using FAST  |               |
| FIX ASN.1            | 1.0              |                        | SOF Header can be used with FIX encoding using ASN.1 |               |
| XML                  |                  |                        | SOF Header can be used with XML                      |               |
| FIX JSON             | 1.0              |                        |Header can be used with FIX encoding using JSON         |               |

Intellectual Property Disclosure
================================

No disclosures required.

Definitions
===========

| **Term**           | **Definition**                                                                 |
|--------------------|--------------------------------------------------------------------------------|
| CODEC              | Encoder / Decoder – a processor that can encode and decode encoded messages.   |
| Little-Endian Byte Order     | Encodes the least significant byte first and the most significant byte last |
| Message            | A stream of 1..n bytes of information of known length and identified encoding. |
| Network Byte Order | Integer values encoding using Big-Endian byte order. Encodes the most significant byte first and the least significant byte last |

Simple Open Framing Header
==========================

The Simple Open Framing Header is six octets in length consisting of two fields, the Message\_Length and Encoding\_Type. The purpose of the Simple Open Framing Header will provide a simple mechanism to process messages from a stream that can have multiple encodings. Message processors are then able to skip over (ignore) any messages for which a CODEC is unavailable.

Simple Open Framing Header Fields
---------------------------------

The Message Framing Header shall consist of two fields.

The Simple Open Framing Header is defined to contain the following information:

### Message\_Length field

The Message\_Length shall be defined to be the length in octets (i.e. bytes) of a message inclusive of the length of the Simple Open Framing Header.

The Message\_Length field shall be the first field in the Simple Open Framing Header.

The Message\_Length field shall be four octets in length, permitting a maximum message size of 2^32.

### Encoding\_Type field

The Encoding\_Type field shall be defined to be an integral enumeration whose value range shall be managed by the FIX Trading Community. The Encoding\_Type shall include well known encodings. The Encoding\_Type shall reserve a range of values for user defined encodings.

The Encoding\_Type field shall be the second field in the Simple Open Framing Header.

The Encoding\_Type field shall be two octets in length, permitting the identification of 2^16 distinct encoding types.

The following encoding types are defined initially as part of the standard. Future encoding types will be defined as part of the standards process.

**Simple Open Framing Header – Encoding\_Types** 

| **Encoding\_Type**                               | **Values**            |
|--------------------------------------------------|-----------------------|
| Private User Defined                             | 0x0001 through 0x00FF
| FIX SBE Version 1.0 Big-Endian                   | 0x5BE0
| FIX SBE Version 1.0 Little-Endian                | 0xEB50
| FIX GPB Version 1.0                              | 0x4700
| FIX ASN.1 PER Version 1.0                        | 0xA500
| FIX ASN.1 BER Version 1.0                        | 0xA501
| FIX ASN.1 OER Version 1.0                        | 0xA502
| FIXTV                                            | 0xF000
| FIXML SCHEMA Version 1.0                         | 0XF100
| FIX FAST                                         | 0xFA01 – 0xFAFF
| FIX JSON                                         | 0xF500

### Use of Private User Defined Encoding\_Types

User defined values shall not be published.

User defined values shall not be considered to be unique and are to be implemented by counterparty agreement.

### Registration of additional Encoding\_Types

Encoding\_Types will be reviewed and approved by the FIX Global Technical Committee. The intent of this standard is to provide open registration. The registration shall not be limited to only FIX encodings.

Encoding of the Simple Open Framing Header
------------------------------------------

By default, the Simple Open Framing Header shall be encoded using unsigned binary integer values in Network Byte Order (big-endian). However, by bilateral agreement between counterparties, little-endian byte order may be used.

Visibility of Framing Header values
-----------------------------------

The Message\_Length and Encoding\_Type shall be made available to the CODEC.

This is a required section where the sub-committee or working group can provide whole or fragments of example FIX messages with actual or dummy data. These examples are useful for illustrating usage or rules specific to the business domain covered in the proposal.

NONE

The technical standard must include some plan for measuring compliance with the standard. This will either be test suites, a validation tool (such as an XML Schema document as an example).

NONE

# Appendix

*This section is informational*

## Simple Binary Encoding (SBE)

The following composite type may be added to an SBE message schema to represent the encoding of Simple Open Framing Header using SBE encoder/decoder mechanisms. Byte order would be controlled by the `byteOrder` attribute of the `<messageSchema>` element.

```xml
<composite name="sofh">
	<type name="messageLength" primitiveType="uint32"/>
	<type name="encodingType" primitiveType="uint16"/>
</composite>
```