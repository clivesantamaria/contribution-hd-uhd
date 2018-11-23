# SCTE-104/35 Signalling

## Generic design

DRAFT  
Author: Keith Millar  
Date: 01/05/2018   
Version: 0.1  

- [Introduction](./SCTE%20104-35%20Signalling%20Generic%20design.md#1-introduction)
- [High Level Requirements](./SCTE%20104-35%20Signalling%20Generic%20design.md#2-high-level-requirements)
   - [Generic Requirements](./SCTE%20104-35%20Signalling%20Generic%20design.md#21-generic-requirements)
   - [Carriage within (H)SDI](./SCTE%20104-35%20Signalling%20Generic%20design.md#22-carriage-within-hsdi)
   - [SCTE-104 over TCP/IP connection to inserter (encoder)](./SCTE%20104-35%20Signalling%20Generic%20design.md#23-scte-104-over-tcpip-connection-to-inserter-encoder)
   - [Inserter requirements](./SCTE%20104-35%20Signalling%20Generic%20design.md#24-inserter-requirements)
- [Marker Solution Overview](./SCTE%20104-35%20Signalling%20Generic%20design.md#3-marker-solution-overview)
   - [SCTE-104](./SCTE%20104-35%20Signalling%20Generic%20design.md#31-scte-104)
   - [Multiple message flows](./SCTE%20104-35%20Signalling%20Generic%20design.md#311-multiple-message-flows)
      - [Splice Insert Messages](./SCTE%20104-35%20Signalling%20Generic%20design.md#312-splice-insert-messages)
      - [Multiple Segmentation Descriptors](./SCTE%20104-35%20Signalling%20Generic%20design.md#313-multiple-segmentation-descriptors)
   - [SCTE-104 over VANC](./SCTE%20104-35%20Signalling%20Generic%20design.md#32-scte-104-over-vanc)
      - [Multiple Segmentation Descriptors](./SCTE%20104-35%20Signalling%20Generic%20design.md#321-multiple-segmentation-descriptors)
      - [Single message per frame](./SCTE%20104-35%20Signalling%20Generic%20design.md#322-single-message-per-frame)
   - [SCTE-104 over TCP/IP](./SCTE%20104-35%20Signalling%20Generic%20design.md#33-scte-104-over-tcpip)
- [Generic capabilities](./SCTE%20104-35%20Signalling%20Generic%20design.md#4-generic-capabilities)
   - [PID mapping](./SCTE%20104-35%20Signalling%20Generic%20design.md#41-pid-mapping)
   - [Message Aggregation](./SCTE%20104-35%20Signalling%20Generic%20design.md#42-message-aggregation)
   - [SCTE-104 processing configurations](./SCTE%20104-35%20Signalling%20Generic%20design.md#43-scte-104-processing-configurations)
- [SCTE-104/35 Message Types](./SCTE%20104-35%20Signalling%20Generic%20design.md#5-scte-10435-message-types)
   - [Splice_Insert](./SCTE%20104-35%20Signalling%20Generic%20design.md#51-splice_insert)
   - [Time_Signal](./SCTE%20104-35%20Signalling%20Generic%20design.md#52-time_signal)
   - [Splice_Null Messages](./SCTE%20104-35%20Signalling%20Generic%20design.md#53-splice_null-messages)


## 1. Introduction
This document defines the Mezzanine stream format for the contribution delivery of 
UHD content.

Within a distribution system a single broadcast contribution feed can be used to
support multiple broadcast feeds. For example a single feed could support a
simulcast IPTV service, DTT Service and a DTH service, where each broadcast
service requires a different set of markers.

![Figure 1](https://github.com/ITV/SCTE-Signalling/blob/master/images/Signalling-with-multiple-end-platforms.png)


## 2. Mezzainine Format
The UHD content shall be as follows:

### 2.1. High Dynamic Range

Signalled as HLG10

### 2.2. Resolution

3840 x 2160

### 2.3. Bit Depth

10 bit

### 2.4. Inserter requirements
- Carriage of markers of different types (e.g. Splice Insert, Programme,
Chapter, etc), on separate MPEG-PIDs within a service. Using
PDI_PID_index of SCTE-104 to map to MPEG-PIDs.
- Support for signalling if inserter (encoder) should perform stream
conditioning for a given SCTE-104 messages.
- Support for signalling if inserter (encoder) should process an SCTE
message.

## 3. Marker Solution Overview

![Figure 2](https://github.com/ITV/SCTE-Signalling/blob/master/images/Example-scte-timeline.png)


## 3.1. SCTE-104



>> include multiple

- The maximum size of a single SCTE-104 message is 2000 bytes in length
([SMPTE.ST2010.2008](https://doi.org/10.5594/SMPTE.ST2010.2008) - multi-operation message). This may in the long
term be limiting, if all markers had to be in one SCTE-104 message.



## 4.3. SCTE-104 processing configurations
The design shall allow an Inserter (encoder) to be configured with the set of
SCTE-104 messages that it should process and also how it should process them.

| Ignore Signal | Generate SCTE-35 | Stream Condition | Comments |  
| ------------- | ---------------- | ---------------- | -------- |
| No | No | Yes | Encoder will perform stream conditioning but will not insert an SCTE-35 Splice_insert message. |  
| Yes | NA | NA | No action by encoder |
| No | Yes | Yes | Encoder will perform stream conditioning and will insert an SCTE-35 Splice_insert message. |
| No | Yes | No | Encoder will not perform stream conditioning, but will insert an SCTE-104 message. |
| No | No | No | Encoder may perform some internal action, but will not generate an SCTE-35 message. (e.g. Modify Subtitle delay) |
