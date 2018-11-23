# UHD Specification

## Generic design

DRAFT  
Author: Keith Millar  
Date: 01/10/2018   
Version: 0.1  



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

## 3.1. Video Encapsulation

The Video frames shall be encapsulated using PES per Frame, with the start of a video frame starting in a new PES packet. 

## 3.2. PSI

The MPEG2-TS shall signal the Video component within the PMT by setting the “stream type” to  0x027 and including a “HEVC_video_decsriptor” (See ETSI TS 101 154 v.2.3.1, clause 4.1.8.19a) with the component declaration.


## 4. Video Encoding

The Video shall be encoding using HEVC (H265) using the “HEVC Main 10 Profile, Main Tier, Level 5.1” profile. The encoding shall be conformant to that defined by DVB in ETSI TS 101 154 v.2.3.1

## 4.1. Signaling Transfer Characteristics

HLG10 allows the signaling of “transfer characteristics” to enhance the picture quality. However if this feature is used the picture is unable to be rendered on a standard UHD TV. Therefore to support the maximum number of devices, “transfer characteristics” shall not be used.

Note:  In the case of Mezzanine streams do we want to use “transfer Characteristics” as we can control the receiving device, performing the transcode. We should be trying to deliver the highest quality video we can.


## 5. Audio Encoding

The Audio shall be encoded as 5.1 Surround sound using AC3 audio.


## 6. Subtitles



## 7. Distribution

The following delivery mechanisms are being considered:

## 7.1. Zixi
## 7.2  IP Multicast





>> include multiple


([SMPTE.ST2010.2008](https://doi.org/10.5594/SMPTE.ST2010.2008) - multi-operation message).
