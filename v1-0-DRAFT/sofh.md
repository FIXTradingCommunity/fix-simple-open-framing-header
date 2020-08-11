Introduction
============

The FIX High Performance Working Group set about defining a set of additional concrete encodings. The intent of these encodings was to efficiently communicate the FIX trading protocol. A decision was taken early on that none of these encodings be bound in and of themselves solely to the use of FIX Protocol. A problem and a requirement arose during the development of these additional encodings. What mechanism could be provided that would permit message processors, such as network protocol analyzers and heterogeneous communication gateways, to determine an application message boundary and the encoding of that message. After considerable deliberation, an approach was selected to create a simple and primitive message framing header that would communicate two pieces of information, the length of a message and the encoding type of that message. Additional requirements were identified. The goal was to make the framing header open and available to support existing and future encoding types and have the ability to reserve a set of encoding types to permit user defined encodings. The FIX Simple Open Framing Header (“the SOF Header”) we believe meets these requirements.

Authors
-------

| **Name**           | **Affiliation**                   | **Role**       |
|--------------------|-----------------------------------|----------------|
| Northey, Jim       | The LaSalle Technology Group, LLC | Author, Editor |
| Furuhed, Anders    | Pantor Engineering                | Author         |
| Mendelson, Don     | CME Group, Inc.                   | Author         |
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
| FIX JSON             |                  |                        | FIX plans a FIX standard encoding for JSON           |               |
| FIX BSON             |                  |                        | FIX plans a FIX standard encoding for BSON           |               |

Intellectual Property Disclosure
================================

No disclosures required.

Definitions
===========

| **Term**           | **Definition**                                                                 |
|--------------------|--------------------------------------------------------------------------------|
| CODEC              | Encoder / Decoder – a processor that can encode and decode encoded messages.   |
| Message            | A stream of 1..n bytes of information of known length and identified encoding. |
| Network Byte Order | Integer values encoding using Big Ending byte order.                           |

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
| FIX SBE Version 1.0 Big Endian                   | 0x5BE0
| FIX SBE Version 1.0 Little Endian                | 0xEB50
| FIX GPB Version 1.0                              | 0x4700
| FIX ASN.1 PER Version 1.0                        | 0xA500
| FIX ASN.1 BER Version 1.0                        | 0xA501
| FIX ASN.1 OER Version 1.0                        | 0xA502
| FIXTV                                            | 0xF000
| FIXML SCHEMA Version 1.0                         | 0XF100
| FIX FAST                                         | 0xFA01 – 0xFAFF
| FIX JSON                                         | 0xF500
| FIX BSON                                         | 0xFB00

### Use of Private User Defined Encoding\_Types

User defined values shall not be published.

User defined values shall not be considered to be unique and are to be implemented by counterparty agreement.

### Registration of additional Encoding\_Types

Encoding\_Types will be reviewed and approved by the FIX Global Technical Committee. The intent of this standard is to provide open registration. The registration shall not be limited to only FIX encodings.

Encoding of the Simple Open Framing Header
------------------------------------------

The Simple Open Framing Header shall be encoded using unsigned binary integer values in Network Byte Order.

Visibility of Framing Header values
-----------------------------------

The Message\_Length and Encoding\_Type shall be made available to the CODEC.

This is a required section where the sub-committee or working group can provide whole or fragments of example FIX messages with actual or dummy data. These examples are useful for illustrating usage or rules specific to the business domain covered in the proposal.

NONE

The technical standard must include some plan for measuring compliance with the standard. This will either be test suites, a validation tool (such as an XML Schema document as an example).

NONE
