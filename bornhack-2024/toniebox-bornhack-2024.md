---
marp: true
paginate: true
theme: einstein
header: ""
footer: "![height:70px](assets/bornhack-2024-logo-l-transparent.png)"
author: Moritz
title: Toniebox 101
description:  An audio player not only for kids.
---
<style>   

   .cite-author {     
      text-align        : right; 
   }
   .cite-author:after {
      color             : orangered;
      font-size         : 145%;
      /* font-style        : italic; */
      font-weight       : bold;
      font-family: 'Fira Sans Condensed', sans-serif; 
      padding-right     : 130px;
   }
   .cite-author[data-text]:after {
      content           : " - "attr(data-text) " - ";      
   }

   .cite-author p {
      padding-bottom : 40px
   }

</style>

<!-- _class: titlepage -->
![bg left:33% brightness:0.9](assets/Toniebox-with-figure.jpg)

<div class="title"         > Toniebox 101                    </div>
<div class="subtitle"      > An audio player not only for kids           </div>
<div class="author"        > Moritz                                     </div>
<div class="organization"  > BornHack 2024         </div>

---

# Disclaimer

- there was an entertaining German talk at **37C3** https://media.ccc.de/v/37c3-11993-toniebox_reverse_engineering
- who saw this: no news here

---

# What is it?

<div class="columns">
<div>

- a cube-shaped digital audio device designed for children
- NFC figures used for the content
- no display
- ears for volume control
- simple and easy to use for kids
- currently available in DE, AT, CH, UK, IR, US, FR, CA 
- rest of Europe online

  </div>
<div>

<center>

![h:550px](assets/Toniebox-with-figure.jpg)

</center>
</div>
</div>

---

# Why?

<div class="columns">
<div>

- curiosity
- dependency on yet another cloud service
- walled garden 
- nosiness of the manufacturer 
- technical reasons
  - works only with original figures
  - artificial 90m limit for own content
  - own content only with expensive creative tonies
  
  </div>
<div>

<center>

![w:33%](assets/i-void-warranties.jpg)

</center>
</div>
</div>

---

# Components

<div class="columns">
<div>

- speaker
- battery pack (NiMH)
- PCB
- ears with integrated buttons
- antenna
  
  </div>
<div>

<center>

![w:75%](assets/parts.jpg)

</center>
</div>
</div>
  


---

# Toniebox PCB



- four layers
- components only on top layer
- 82 testpoints
- WiFi antenna
  

---

<div class="columns-center">
<div>


![h:520px](assets/pcb-front.jpg)

</div> 
<div>

![h:520px](assets/pcb-back.jpg)

</div>
</div>
  
---



![bg w:100%](assets/pcb-components.png)

---

# Toniebox Hardware


- three different uC over the years
  - TI CC3200
  - TI CC3235 (US)
  - Espressif ESP32-S3

---

# CC3200

<div class="columns">
<div>

- pretty widespread, mostly older boxes
- debug interface: tag connect
- flash is unencrypted and unsigned
- `cc3200tool` for reading and writing with tag connect adapter
- custom firmware (Hackiebox)
- custom bootloader (HackieboxNG)

</div>
<div>
<center>

![w:200px](assets/cc3200.png)

</center>

</div>
</div>

---



# CC3235

<div class="columns">
<div>

- for US market
- rare in Europe
- debug interface: tag connect, but likely locked
- access to flash possible, but needs SOP8 clamps
- content partially encrypted 
  - certificates unencrypted
  - firmware signed and encrypted
- `cc32tool` for manipulating the flash dump

</div>
<div>
<center>

![w:200px](assets/cc3235.jpg)

</center>

</div>
</div>


---

# ESP32

<div class="columns">
<div>

- latest version, new boxes
- debug interface `UART`, common for esp32
- accessible with `esptool`
- flash unencrypted and unsigned
- custom firmware (PoC)
  - Hackiebox ESPuino port
  - TeddyBox
</div>
<div>
<center>

![w:200px](assets/esp32.jpg)

</center>

</div>
</div>


---

![bg h:100%](assets/toniebox-esp32-front.jpg)



---

# Schematic/Block Diagram


<div class="columns">
<div>

- basic KiCad schematic available on GitHub
- testpoint table https://github.com/toniebox-reverse-engineering/toniebox-pcb#testpoints
- 82 testpoints
  -  at least connections specified
  -  50 commented

</div>
<div>
<center> 

![w:100%](assets/testpointtable.png)

</center>

</div>
</div>


---

<!-- footer: "" -->

![bg h:100%](assets/blockdiagram.jpg)


---

<!-- footer: "![height:70px](assets/bornhack-2024-logo-l-transparent.png)" -->

# How does it all work?

<div class="columns">
<div>

- put the Tonie on top
- read the `UID` from tag
- if there is no related content on the SD card
  - read tag memory
  - get audio content from cloud
  - write content to SD card
- play audio content

</div>
<div>
<center> 

![w:100%](assets/function.png)

</center>

</div>
</div>

---


# NFC



- NXP SLIX-L / ISO 15693
- privacy mode, will not reveal data, except `GET RANDOM NUMBER` and `SET PASSWORD`
- antenna made of coiled wire
- fake tags and clone tags exist
- custom tags are working
- Flipper Zero and Proxmark3 SLIX-L unlock and emulator added 
- see https://www.g3gg0.de/rf/flipper-zero-got-iso15693-nfc-v-support for details (»this was some serious journey«)


---
<!-- footer: "" -->
![bg w:100%](assets/unlock-rfid.png)



---

<!-- footer: "![height:70px](assets/bornhack-2024-logo-l-transparent.png)" -->


![bg width:400px](assets/nfc1.jpg)
![bg width:400px](assets/nfc2.jpg)
![bg width:400px](assets/nfc3.png)

---

# How does the SD card content work?


- content filed in directories
- opus files with padding and `protobuf` header

---
<!-- footer: "" -->

![bg w:100%](assets/sd-card-function.png)


---




![bg w:100%](assets/unlock-sdcard.png)



---

<!-- footer: "![height:70px](assets/bornhack-2024-logo-l-transparent.png)" -->

# Teddybench (level: easy)

<div class="columns">
<div>

- software for manage content on the SD card
- converts MP3 to OPUS
- displays content of SD card based on a list of 1100 tonies (`tonies.json`) 
- cons:
  - box needs to be offline mode
  - custom tags are difficult to obtain

</div>
<div>

<center>

![width:100%](assets/teddybench.jpg)

</center>

</div>
</div>

---

# tonies.json

<div class="columns-center">
<div>         
 
![drop-shadow:4px,5px,15px,#010101](assets/tonies-json.png)

   
</div> 
<div>

![drop-shadow:4px,5px,15px,#010101](assets/tonie-json.png)


</div>
</div>


---

# Removing the SD card

<div class="columns-center">
<div>         
<center>

[![Remove the SD card](https://img.youtube.com/vi/GOZRjaEhrcQ/0.jpg)](http://www.youtube.com/watch?v=GOZRjaEhrcQ "Remove the SD card")

</center>

</div>
</div>

---



<!-- footer: "" -->

![bg w:100%](assets/modding-diy.png)


---

![bg w:100%](assets/modding-diy1.png)


---



<!-- footer: "![height:70px](assets/bornhack-2024-logo-l-transparent.png)" -->



# How does the cloud work

- we put some effort into figuring out how the cloud works
- result in our wiki on GitHub:  https://toniebox-reverse-engineering.github.io/docs/wiki/general/protocol-analysis/

---

<!-- footer: "" -->


![bg w:100%](assets/cloud-api.png)


---

![bg w:100%](assets/unlock-all-the-things.png)


---

<!-- footer: "![height:70px](assets/bornhack-2024-logo-l-transparent.png)" -->

# TeddyCloud  (level: hard)

<div class="columns">
<div>

- written in C, few dependencies, portable (Linux, Windows, Docker)
- Box usable without the cloud
- works for all box variants (replacing certificates)
- own content via TeddyBench or web interface
- download of firmware and original tonies
- ESP32 patch via webinterface

</div>
<div>

<center>

![height:500px](assets/teddycloud.jpg)

</center>

</div>
</div>

--- 

# Home Assistant Integration

<div class="columns">
<div>

- by analyzing the debug log sent to manufacturer home assistant integration is possible

</div>
<div>

<center>

[![Home Assistant](https://img.youtube.com/vi/WqVnnrtgd6k/0.jpg)](http://www.youtube.com/watch?v=WqVnnrtgd6k "Home Assistant")

</center>

</div>
</div>

---

# Privacy

- sends all user interaction to manufacturer cloud 
  - volume changes
  - skipping
  - tonie 
  - SSIDs in vicinity
- changed privacy statement that they removed SSID transmission

---

# Custom Firmware Hackiebox 

## CC3200

- PoC Custom Firmware
- File up-/download (to flash or SD card)
- usable for hardware testing

## ESP32

- PoC Custom Firmware (Teddybox)
  
---

# Custom Bootloader HackieboxNG (CC3200)

- two stages 
- allows booting the OFW and CFW
- patches OFW on startup
  - disable privacy mode
  - enabling other SLI* tags
  - cloud blocking
  - replacing cloud URLs and CA

---

# Summary

- decent hardware to play with
- hacker friendly
- own content on the SD card 
- prices of used Tonieboxes skyrocketed due to documentation for repairs

---

# Modding


<div class="columns-center">
<div>         
 
![drop-shadow:4px,5px,15px,#010101](assets/bt.png)

   
</div> 
<div>

![drop-shadow:4px,5px,15px,#010101](assets/modding5.jpg)


</div>
</div>




---

<!-- footer: "" -->

![bg](assets/modding-diy2.png)


---



<!-- footer: "![height:70px](assets/bornhack-2024-logo-l-transparent.png)" -->

# Contact us

- GitHub: https://github.com/toniebox-reverse-engineering
- Forum: https://forum.revvox.de/
- Telegram: https://t.me/toniebox_reverse_engineering
- Moritz 
  - [moritz23.42 on Signal](https://signal.me/#eu/c5Ap7ONrInf9_IjfT4P3mcAzr5DS5cvmAOx4xH9IK9yoUlb2hJJCW5GZk7sNm2-S)
  - [@elgolfo@chaos.social on Mastodon](https://chaos.social/@elgolfo)

---

# Images

- https://en.wikipedia.org/wiki/Tonies_(company)#/media/File:Toniebox.jpg
- https://www.redbubble.com/i/sticker/I-VOID-WARRANTIES-WITH-PRIDE-LGBTI-by-jillesdotcom/121258026.EJUG5