


## **CRU**  
- Simplified Block Diagram 
![alt text](IMG/image_2.png)

### **Clock**
![alt text](IMG/image_22.png)
![alt text](IMG/image_1.png)
![alt text](IMG/image.png)
![alt text](IMG/image_20.png)
### **PCIe DMA**

Основной поток данных передаётся через интерфейс DMA для перемещения данных от FEE (Front-End Electronics) в память FLP (First Level Processor).   

CRU использует PCIe Gen 3 × 16 интерфейс для связи с FLP. 
    Используются два BAR интерфейса: BAR0 и BAR2.
    BAR0 занимается DMA-операциями, передаёт дескрипторы страниц и следит за статусом сбора данных.
    BAR2 используется для настройки конфигурации и мониторинга других компонентов прошивки.
## 🟢 05 - LTU - CRU
[alt text](https://indico.cern.ch/event/863071/contributions/3738822/attachments/2044868/3425551/Alice_TTCPON_for_ACES_2020.pdf)
[text](https://twiki.cern.ch/twiki/pub/ALICE/CruHwFwSwDev/CRU_Specification_v0.7.pdf)

![alt text](IMG/image_21.png)


### 🟢 02 - GBT



У нас есть два типа рамек 
![alt text](IMG/image_5.png)
![alt text](IMG/image_6.png) 

![alt text](IMG/image_7.png) 

Как это работает?
Детекторы передают данные к CRU (Central Readout Unit).
Если isdatasel = 1, передаются физические события.
Если isdatasel = 0, CRU определяет управляющие команды по старшим битам данных.
CRU извлекает SWT и отправляет его в FIFO, доступный для системы управления DCS.


![аа](IMG/image_8.png) 
Физические данные обозначены флагом isdatasel = 1, а управляющие команды (IDLE, SOP, EOP, SWT) имеют флаг isdatasel = 0 и содержат другой заголовок, который хранится в поле данных GBT.
The CRU extracts the SWT information from the data stream before it reaches the DMA engine
and stores it in a dedicated FIFO which is accessed by DCS.

??? Header success
    ![аа](IMG/image_9.png) 

??? Frame detection
    ![аа](IMG/image_10.png)

??? is data 
    ![аа](IMG/image_11.png)

#### 🟢 02.1 Data Frame & Encodings
??? success
    ![аа](IMG/image_13.png) 
    ![аа](IMG/image_19.png)
#### 🟢 02.2 Usual Latency
??? success
    ![аа](IMG/image_14.png)
    ![аа](IMG/image_17.png)
    ![аа](IMG/image_18.png)
#### 🟢 02.3 GBT Tx GBT Rx
??? success
    ![аа](IMG/image_15.png) 
#### 🟢 02.4 Single-Link Example Design
??? success
    ![аа](IMG/image_16.png) 
    Tx (передатчик) подключается к Pattern Generator, который создаёт тестовый сигнал.
    Rx (приёмник) подключается к Pattern Checker, который проверяет правильность передачи.


#### 🟢 03.1 - GBT-SWT (Single Word Transfer)
Основа:

- Используется только в ALICE для передачи одиночного слова конфигурации. 
- Позволяет передавать конфигурационные команды намного быстрее, чем GBT-EC.
- Использует канал GBT-DATA, который может передавать данные со скоростью 3200 Мбит/с (80*40Mhz) (в 40 раз быстрее, чем GBT-EC).

Как работает:

- FPGA на детекторе формирует команду SWT (0x3).
- CRU получает поток данных и выделяет из него команды управления.
- CRU сохраняет полученные команды в FIFO, где они становятся доступными для DCS (детекторной системы управления).

Как выглядит пакает:

![alt text](IMG/image_4.png)
#### 🟢 03.2 - FLP - FE
[text](https://twiki.cern.ch/twiki/pub/ALICE/CruHwFwSwDev/CRU_Specification_v0.7.pdf) 
SOP (Start of Packet)
??? XXXX 
    ![аа](IMG/image_25.png)













### 🟢 05 - LTU - CTP 
![alt text](IMG/image_24.png)
[text](https://indico.cern.ch/event/863071/contributions/3738822/attachments/2044868/3425551/Alice_TTCPON_for_ACES_2020.pdf)

#### BYSY 
CRU Говорить что мы пхаем уже много данных
![alt text](IMG/image_26.png)

### 🟢 Heart Beat Frames (inside fpl - cru)
![alt text](IMG/image_23.png)

### 🟢 999 - ToDo

- **В конуе ознакомиться с етим документом:** https://physics.bu.edu/~hazen/GLIB/gbt_fpga/tags/gbt_fpga_3_0_0/doc/GBT_FPGA%20_User_Guide_v1_0.pdf

## 🟢 00 - links

- [📄Implementing CERN GBT and lpGBTlink arrays in Intel Arria 10 FPGA](../ALL_PDF_CERN/Implem_CERN_GBT_and_lpGBTlink_Intel_Arria_10.pdf)
- [📄CRU](../ALL_PDF_CERN/CRU.pdf)
- [📄Sebastian indico (SWT)](../ALL_PDF_CERN/Sebastian_indico.pdf)
- [📄GBT FPGA User Guide v1_0](../ALL_PDF_CERN/GBT_FPGA_User_Guide_v1_0.pdf)
- [📄GBTx](../ALL_PDF_CERN/gbtxManual.pdf)
- [📄GBT-SCA](../ALL_PDF_CERN/GBT-SCA.pdf)


- 🔗[gitlab-alice-cru](https://gitlab.cern.ch/alice-cru/)
- 🔗[GitHub VictorPierozak - IPbus](https://github.com/VictorPierozak/IPbus)  
- 🔗[GitHub VictorPierozak - IpbusSWT](https://github.com/VictorPierozak/IpbusSWT/tree/master)  
- 🔗[GitHub VictorPierozak - ALFIPbu](https://github.com/VictorPierozak/ALFIPbus)
- 🔗[gbtproject](https://gbtproject.web.cern.ch/gbtproject/)