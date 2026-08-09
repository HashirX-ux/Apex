# Project Journal

**Project Name:** Apex  
**Start Date:** 2026-01-08  
**Status:** In Progress

## Overview
Apex is a wireless mechanical keyboard built for productivity and daily tasks.

## Recent Entries

### 2026-01-08 - First Journal Entry

**What I did today:**

So This is my first time creating a keyboard. I have created a macropad before so I thought why not built a full keyboard of my own. So I did it duhh.. it was difficult but somehow I did it.. 
<br>

I am gonna start my research now.. Gonna start with the number of keys that i am gonna use: 
<img width="1146" height="826" alt="image" src="https://github.com/user-attachments/assets/4bc534e8-78e6-4dc6-8470-9e561a60fb4e" />
<br>
Guess I am gonna use standard keyboard keys which are 104 for the US/Canada type: 
<img width="874" height="319" alt="image" src="https://github.com/user-attachments/assets/8e49005d-463f-45f3-aa9a-e47f455d5cef" />
<br>
So I researched a not for the MCU that I wass gonna use for my keybord and I found the nicennao v2 the best for that as it already contains built in crystal oscillator and voltage regulator which us gonna help me manage my schematic and make it less complexx..
<br>
So here are my main components that I am gonna use for my keyboard: 
<br>

1- MCU: nicenano! v2
<img width="811" height="668" alt="image" src="https://github.com/user-attachments/assets/d1ed7ff5-c239-4fb7-ab0b-31ff37b14e74" />
<br>

2- 104-standard keys
<img width="578" height="560" alt="image" src="https://github.com/user-attachments/assets/b4bff966-d0a3-4e3f-96c3-5c9e9afd8d61" />
<br>

3- OLED 0.91 inch
<img width="791" height="378" alt="image" src="https://github.com/user-attachments/assets/ca5fb79e-bab9-4f92-b570-9d1abce0dfe8" />
<br>

4- RotaryEncoder
<img width="449" height="439" alt="image" src="https://github.com/user-attachments/assets/1661b7cc-5ccc-4ee1-b79b-0ee8df900e3f" />
<br>

5- Buzzer
<img width="436" height="236" alt="image" src="https://github.com/user-attachments/assets/bf576351-0752-4a62-887f-3f763af392a3" />

5- Diodes
<img width="587" height="554" alt="image" src="https://github.com/user-attachments/assets/20cb6bb7-d962-40d3-af81-3c8e614e1da0" />
<br>

6- DeCoupling Caps
<img width="717" height="518" alt="image" src="https://github.com/user-attachments/assets/03a8a0ff-8536-45e6-abee-89e55095fb64" />
<br>

7- Reset Swtich
<br>

Now I gotta understand all of the datasheeeets.. Lets start by nicennao.. Wish me luck gngng..I am gonna use the official nicennao doc for this research: 
<br>
https://nicekeyboards.com/docs/nice-nano/
<br>
Found this keyboard config guide: https://www.nextpcb.com/blog/how-to-design-mechanical-keyboard-pcbs-with-kicad
<img width="1047" height="506" alt="image" src="https://github.com/user-attachments/assets/58e9b140-1ae1-48ea-bfce-d7a53232b9d1" />
<br>
One of the best guide I found out there gng .. 
<br>
https://www.modmusings.com/how-to-build-a-mechanical-keyboard
<br>
Thanks again the og documentation.. This is gonna help alot
<img width="1212" height="835" alt="image" src="https://github.com/user-attachments/assets/0ae09b64-4409-4e99-a061-736c0829dd5c" />
<br>
So this is the schematic for the OLED i am gonna use its OLED 0.91: 
<img width="858" height="575" alt="image" src="https://github.com/user-attachments/assets/45ab2a71-4039-4b8d-84fb-1f816c120f60" />
<br>
Didnt expected my rotary encoder to look like this under the hood: 
<img width="800" height="631" alt="image" src="https://github.com/user-attachments/assets/045d8c6d-ac0a-4945-b912-8e3cd67298d1" />
<br>
This would really help in designing the 3D cover case for my keyboard.. 
<img width="1201" height="709" alt="image" src="https://github.com/user-attachments/assets/2ba200f8-90b2-452b-b4ac-22423e49b47e" />
<br>
YOOO gng i think I just found a goldmine thank god i was looking for this: 
https://www.masterzen.fr/2020/05/03/designing-a-keyboard-part-1/
So Now I am Done with the research I am gonna start building the shcmeatic of my keyvaord and then The Final PCB design.. Wish me luck boisss.. 
<br>
### 2026-02-08 - First Journal Entry

**What I did today:**
So Today I am gonna start building the shcematic of my keyboard.. I am gonna use the official guide from PCBWay and JLCPCB for their keyboard design guide: 
<br>
https://jlcpcb.com/blog/pcb-keyboards-design-guide
<br>
So I am gonna build the schematic using this layout: 
<img width="615" height="342" alt="image" src="https://github.com/user-attachments/assets/27d35a95-1f77-43a8-ae66-ce40552cf058" />
<br>
The MCU looks good.. its nice and nano nicenano!!!
<img width="568" height="664" alt="image" src="https://github.com/user-attachments/assets/dae8b7e3-c009-4554-9fa7-bdba6b9d961e" />
<br>
So this is my first key and I have to compleye like 112 of them.. wish me luck gng: 
<img width="547" height="393" alt="image" src="https://github.com/user-attachments/assets/7b4b30f2-5739-4781-9986-5498e67606a2" />
<br>
So far so good gng yayay: 
<img width="862" height="500" alt="image" src="https://github.com/user-attachments/assets/09e50d82-f166-48fe-b86c-fdafd9d43f70" />
Looks good gng.. i need to structure it: 
<img width="1132" height="455" alt="image" src="https://github.com/user-attachments/assets/04d1773a-0d1f-4489-a6cf-ab2cd4e925e2" />
<br>
Done with the key matrix.. Loooks finne gng: 
<img width="966" height="380" alt="image" src="https://github.com/user-attachments/assets/775f3dfd-5e93-4e2b-a4ab-09041afd61ba" />
<br>
So I just realised that my mcu has shorter pins to the number of pins I need so i gotta look up for some other mcu :(.. So i found ESP-S3 for my keyboard as it has 45! gp pins and nicennao only has .. LAME NICENNAO: 
<img width="505" height="394" alt="image" src="https://github.com/user-attachments/assets/9000aa51-4619-42f4-ae74-d825e770704a" />
<br>
<img width="1053" height="656" alt="image" src="https://github.com/user-attachments/assets/02a8a113-569f-46c3-a161-5f854fa8d9d8" />
<br>
The schematic is massive gng 
<img width="600" height="765" alt="image" src="https://github.com/user-attachments/assets/d7009cbd-4b0a-4fb6-8f63-a0ec183cbd03" />
<br>
Now I am gonna start building the crystal oscillator using this guide: 
<br>
https://forum.kicad.info/t/solved-what-is-a-proper-way-to-model-xtal-in-kicad/22954
<img width="608" height="691" alt="image" src="https://github.com/user-attachments/assets/24bb06d2-5f5a-46ce-8dd1-14a54f55f283" />
<br>
Looks good But u still gotta make some tweaks.... 
<img width="821" height="767" alt="image" src="https://github.com/user-attachments/assets/57afeaaa-6977-4d2f-91f3-5ee4e3f4ae52" />
<br>
CHANGE IN PLAN I REPEAT CHANGE IN PLAN!!.. I just found that I can just use Nordic nRF52840.. Gosh my 2 braincells cant figure ts out.. 
<img width="571" height="350" alt="image" src="https://github.com/user-attachments/assets/8696f91b-d506-4387-9076-dea87f172c59" />
<br>
So Now I gonna finish my rotary encoder
<img width="958" height="508" alt="image" src="https://github.com/user-attachments/assets/909aa819-8635-4b11-9778-c339ed23b8c4" />
<br>
Now Gotta build the charger: 
<img width="731" height="486" alt="image" src="https://github.com/user-attachments/assets/b3df7638-bede-49d4-b24b-fe79a536f595" />
<br>
The LED voltage regulator looks good.. 
<img width="909" height="529" alt="image" src="https://github.com/user-attachments/assets/bb2a5cf2-c8b1-4d2a-b87b-a3129a2f6ffa" />
<br>











