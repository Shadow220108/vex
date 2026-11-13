<h1 align="center">
<br>
<img width="700" alt="vex" src="images/render_angle.png" />
<br>
Vex
<br>
</h1>

<h3 align="center">

A round 7 port USB hub :D

</h3>

<div align="center">
  <img width="420" alt="top" src="images/render_top.png" />
  <img width="300" alt="zine" src="images/zine.png" />
</div>

Vex is a USB 2.0 hub built around the FE2.1 chip. You plug it into your laptop with one USB-C cable and it gives you 7 ports around the edge, 3 USB-C and 4 USB-A. The board is a 70 mm circle with 4 layers, cause I didn't want another boring rectangle hub.

The whole design process is in [JOURNAL.md](JOURNAL.md), it took me around 39 hours.

## Features

- FE2.1 USB 2.0 hub chip with 7 downstream ports
- 1 USB-C upstream port, 3 USB-C and 4 USB-A downstream ports
- Ports split into 2 power groups, each with its own polyfuse (2A and 1.5A) and an AO3401A power switch controlled by the hub
- Overcurrent sensing, so the hub knows if a port shorts
- SMAJ5.0A TVS diode and reverse current protection on the input
- 47uF cap on every downstream port so plugging something in doesn't dip the others
- 56k CC pullups on the USB-C downstream ports so phones and other USB-C devices get power
- Blue power LED and red hub active LED
- Bus powered, all ports share what the laptop port gives

## Ports

| Port | Type | Power group |
| --- | --- | --- |
| Upstream | USB-C | Input from laptop |
| 1 to 4 | Downstream | Group A, 2A fuse |
| 5 to 7 | Downstream | Group B, 1.5A fuse |

## Schematic

| Full schematic |
| --- |
| <img width="900" alt="schematic" src="images/full_schematic.png" /> |

| Upstream port | Hub chip |
| --- | --- |
| <img width="450" alt="upstream" src="images/upstream_usb_c.png" /> | <img width="450" alt="fe2.1" src="images/fe21_wired.png" /> |

## PCB

| Routed | Ground pour |
| --- | --- |
| <img width="400" alt="routed" src="images/routed.png" /> | <img width="400" alt="pour" src="images/ground_pour.png" /> |

The FE2.1 sits in the middle so the USB lines to every port are about the same length. Top and bottom have ground fills, inner 1 is a ground plane and inner 2 is a 3.3V plane. The power traces are 0.8 mm and there are 107 vias stitching it all together.

## Firmware 

Since the USB HUB uses, plug and play IC, this project requires no firmware

| Back |
| --- |
| <img width="550" alt="back" src="images/render_back.png" /> |



## Why was it made?

My laptop only has 2 USB ports and I'm always running out. So I made my own hub, and made it round so it actually looks cool on my desk :D

## BOM

| Item | Qty | Price ($) | Vendor |
| --- | --- | --- | --- |
| PCBA (2 boards) | 1 | 35.70 | JLCPCB |
| Total | | 35.70 | |


## Here is the full bom of LCSC parts from KiCAD 

|Designator         |Footprint                                              |Quantity|Value                      |LCSC Part #|Part Name                                    |Unit Price (USD)|Ext Price (USD)|Price Tier|
|-------------------|-------------------------------------------------------|--------|---------------------------|-----------|---------------------------------------------|----------------|---------------|----------|
|C1, C15, C16       |1210                                                   |3       |100uF                      |C49066     |Samsung CL32A107MQVNNNE (6.3V)               |0.1241          |0.3723         |2+        |
|C10, C11, C14, C4, C6, C7, C8|0603                                                   |7       |100nF                      |C14663     |Yageo CC0603KRX7R9BB104                      |0.0025          |0.0175         |1+        |
|C12, C13           |0603                                                   |2       |18pF                       |C1647      |Samsung CL10C180JB8NNNC                      |0.0159          |0.0318         |100+      |
|C17, C18, C19, C20, C21, C22, C23|1206                                                   |7       |47uF                       |C96123     |Samsung CL31A476MPHNNNE (10V)                |0.0705          |0.4935         |10+       |
|C2, C3, C5, C9     |0805                                                   |4       |10uF                       |C15850     |Samsung CL21A106KAYNNNE                      |0.0856          |0.3424         |20+       |
|D1                 |D_SMA                                                  |1       |SMAJ5.0A                   |C113952    |MDD SMAJ5.0A                                 |0.0344          |0.0344         |20+       |
|D2                 |0603                                                   |1       |Power-Blue                 |C72041     |Everlight 19-217/BHC-ZL1M2RY/3T              |0.0172          |0.0172         |20+       |
|D3                 |0603                                                   |1       |Hub-Active Red             |C2286      |Hubei KENTO KT-0603R                         |0.0065          |0.0065         |100+      |
|F1                 |1812                                                   |1       |2A hold (1812)             |C49073033  |BORN SMD1812-200/16N (PTC 16V)               |0.0272          |0.0272         |10+       |
|F2                 |1812                                                   |1       |1.5A hold (1812)           |C46641160  |R+O SMD1812-150-16 (PTC 16V)                 |0.0634          |0.0634         |10+       |
|J1, J2, J3, J4     |USB_C_Receptacle_HRO_TYPE-C-31-M-12                    |4       |USB_C_Receptacle_USB2.0_16P|C165948    |Korean Hroparts TYPE-C-31-M-12               |0.1750          |0.7000         |5+        |
|J5, J6, J7, J8     |USB_A_Molex_67643_Horizontal                           |4       |USB_A                      |C564920    |Molex 676432910                              |0.9326          |3.7304         |1+        |
|Q1, Q2, Q3         |SOT-23                                                 |3       |AO3401A                    |C15127     |AOS AO3401A                                  |0.0629          |0.1887         |10+       |
|R1, R2             |0603                                                   |2       |5.1K                       |C23186     |UNI-ROYAL 0603WAF5101T5E                     |0.0012          |0.0024         |100+      |
|R10, R11, R12, R13, R14, R15|0603                                                   |6       |56K                        |C23206     |UNI-ROYAL 0603WAF5602T5E                     |0.0020          |0.0120         |100+      |
|R3, R8             |0603                                                   |2       |1K                         |C21190     |UNI-ROYAL 0603WAF1001T5E                     |0.0010          |0.0020         |100+      |
|R4, R5             |0603                                                   |2       |100K                       |C25803     |UNI-ROYAL 0603WAF1003T5E                     |0.0015          |0.0030         |100+      |
|R6                 |0603                                                   |1       |2.7K 1%                    |C13167     |UNI-ROYAL 0603WAF2701T5E                     |0.0010          |0.0010         |100+      |
|R7, R9             |0603                                                   |2       |10K                        |C25804     |UNI-ROYAL 0603WAF1002T5E                     |0.0010          |0.0020         |100+      |
|U1                 |LQFP-48_L7.0-W7.0-P0.50-LS9.0-BL                       |1       |FE2.1                      |C39693     |Terminus FE2.1-CQFP48A                       |1.7038          |1.7038         |1+        |
|Y1                 |Crystal_SMD_3225-4Pin_3.2x2.5mm                        |1       |12MHz                      |C70565     |YXC X322512MOB4SI (12pF load)                |0.0974          |0.0974         |5+        |
