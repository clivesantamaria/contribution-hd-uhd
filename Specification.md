# HD and UHD Contribution Specification

## Generic design

DRAFT  
Author: Keith Millar  
Date: 24/10/2018   
Version: 0.1  

Formating update: Clive Santamaria
Date: 23/11/2018   
Version: 0.2  

Converted from original internal document 
https://docs.google.com/document/d/1IRstCMCU3iLHEv_rMMy__LTXxAiHVwKPcE1GUjurrYM/edit#


## 1. Introduction
This document defines the Mezzanine stream format for the contribution delivery of 
UHD content.

Within a distribution system a single broadcast contribution feed can be used to
support multiple broadcast feeds. For example a single feed could support a
simulcast IPTV service, DTT Service and a DTH service, where each broadcast
service requires a different set of markers.


## 2. Mezzainine Format
The UHD content shall be as follows:

### 2.1. High Dynamic Range

Signalled as HLG10

### 2.2. Resolution

3840 x 2160

### 2.3. Bit Depth

10 bit

### 2.4. Chroma Subsampling

4:2:2

### 2.5. Frame

Intra frame

### 2.6. Frame Rate

50 Hz, Progressive

### 2.7. Colorimetry

BT.2020 non-constant luminance

### 2.8. Transfer Characteristics

BT.2100

### 2.9. Video range

Narrow range only


## 3. Encapsulation

The AV data shall be encapsulated as an MPEG2 Single Program Transport Stream with a maximum bitrate of 100Mbits/s. 

### 3.1. Video Encapsulation

The Video frames shall be encapsulated using PES per Frame, with the start of a video frame starting in a new PES packet. 

### 3.2. PSI

The MPEG2-TS shall signal the Video component within the PMT by setting the “stream type” to  0x027 and including a “HEVC_video_decsriptor” (See ETSI TS 101 154 v.2.3.1, clause 4.1.8.19a) with the component declaration.


## 4. Video Encoding

The Video shall be encoding using HEVC (H265) using the “HEVC Main 10 Profile, Main Tier, Level 5.1” profile. The encoding shall be conformant to that defined by DVB in ETSI TS 101 154 v.2.3.1

### 4.1. Signaling Transfer Characteristics

HLG10 allows the signaling of “transfer characteristics” to enhance the picture quality. However if this feature is used the picture is unable to be rendered on a standard UHD TV. Therefore to support the maximum number of devices, “transfer characteristics” shall not be used.

Note:  In the case of Mezzanine streams do we want to use “transfer Characteristics” as we can control the receiving device, performing the transcode. We should be trying to deliver the highest quality video we can.


## 5. Audio Encoding

The Audio shall be encoded as 5.1 Surround sound using AC3 audio.


## 6. Subtitles

Subtitles if provided shall be represented as DVB-TTML (ETSI EN 303 560 v1.1.1), and delivered as a separate components
within the Transport Stream. 


## 7. Distribution

The following delivery mechanisms are being considered:

#### 7.1. Zixi
#### 7.2  IP Multicast


- - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - 


## 8. HD Mezzanine Distribution

Original Document : Simulcast Delivery Over IP v1
![Figure 1 https://docs.google.com/presentation/d/1wxBFwKbxcUJg-gIKDacQQ9rA-JISyvyYd0lfxgaci3Q/edit#slide=id.ge8cd77181_0_127


#### 8.1. Origination

The channels will originate at hosting sites in a pair of redundant racks on ‘red and blue’ paths. The streams are encoded 
to a mezzanine HD transport stream format at 25Mbps. This will ensure sufficient quality for the subsequent transcoding. 


#### 8.2. Distribution

The HD streams will be transported as multicast and distributed over a private network to the data centres acting as points of
presence. The network is self-healing and will re-route streams in the event of circuit or equipment failure.


#### 8.3. Hand-off

The streams will be presented on nominated IP addresses and ports. The client will be required to provision
connectivity to access the streams.


#### 8.4. Video

Resolution: 1920 x 1080
Codec: H.264
Profile/Level: HP@4.0
Bitrate: 25 Mbps CBR
Frame Rate: 25
GOP: 50 frames
Colour: 4:2:0 

#### 8.5.  Audio

Codec: AAC-LC
Bitrate: 256 Kbps

#### 8.6.  Transport

MPEG 2 TS over Multicast UDP/RTP

