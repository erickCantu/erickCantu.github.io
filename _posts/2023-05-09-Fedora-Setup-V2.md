---
title: "Fedora 38 Setup - Part II - Workstation Version" 
categories: 
    - Fedora 38
    - Worksation Version
    - Work Station Setup
tags: 
    - Fedora 38
    - Work Station
    - Computer Setup
    - Root Expansion
    - Data Science Workstation Setup

last_modified_at: 2023-05-09T23:00:00-01:00
image: /assets/images/posts/fedora38_KDE/ecantu_Create_an_abstract_paint_that_illustrates_the_fusion_of__0af24d51-1ddd-4b05-99e1-fb2ef32ee269.png
---

WELL.. The KDE server version did not work well. The computer reboot when streaming while the CPU got temperatures around 61&deg;C. Installing NVIDIA drivers did not resolved the issue. Black screens came after booting.. A possiblity could be, missing the configuration in the boot setup to use the nvidia driver instead of the nouveau divers. Additionally there was mouse freezing, which could be fixed by using the solaar package. Bud did not had the oportunity to test it. I tried the KDE ISO version whit the same results than using the server version. 



So, I am trying GNOME.  After installing the Workstation ISO and seting up as in the previous post, the rebooting problem remains. It seems that is a recurring problem with the nouveau drivers ([ABRT Analytics - Report #617657 - xorg-x11-drv-nouveau in gf100_gr_reset](https://retrace.fedoraproject.org/faf/reports/617657/)). This means that NVIDIA drivers are required; atleast is what I pressume. While using Ubuntu and loading the proprietary NVIDIA drivers, the workstation woked without any issues. In this post I am documenting how to install them. 



*The post image was created with midjourney. Prompt: /imagine Create an abstract paint that illustrates the fusion of engineering and innovation with Data Science, navigating the crossroads of expertise to create sustainable and efficient solutions using oil as the medium, with the impasto technique, emphasizing depth and contrast, and featuring a stunning midnight blue color palette. --no Letters, Text, Signature, Watermark, Logo, Stamp, Branding, Trademark, Copyright, Registered Trademark, Human, Person, People. --aspect 7:4 --s 750 --v 5 --q 2*  

---

### Fix the Logitech drivers

```bash
sudo dnf update
sudo dnf install solaar 
```
