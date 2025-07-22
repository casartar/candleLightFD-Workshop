## Original Projekt
### Hardware
[https://github.com/linux-automation/candleLightFD]()

### Firmware
[https://github.com/linux-automation/candleLight_fw/tree/topic/candleLightFD]()

## ibom
[ibom_mainboard.html](https://html-preview.github.io/?url=https://github.com/linux-automation/candleLightFD/blob/main/release/candlelightfd-S01-R01/candlelightfd-S01-R01-V01/candlelightfd-S01-R01_BOM.html)
- "Front only" (F) einstellen
- Setting - Highlight first pin - selected
- C11, C9, P1, P2, R7, R8, U4 wird nicht bestückt

## BOM mit LCSC Bestellnummern
Anzahl   | Reference           | Part number        | LCSC     | Bemerkung
-------- | --------            | --------           | -------- | --------
5        | C3, C4, C5, C8, C10 | 100nF              | C6119867 | 
2        | C6, C7              | 10uF               | C2959727 | 
2        | C1, C2              | 6,2pF              | C37474   | 
1        | D3                  | KPT-1608EC         | C598355  | 
2        | D2, D1              | KPT-1608SGC        | C5443993 | 
1        | R6                  | 10k                | C4226066 | 
3        | R3, R4, R5          | 1k                 | C5220830 | 
2        | R1, R2              | 5k1                | C218090  | 
1        | U1                  | STM32G0B1CBT       | C2847904 | 
1        | X2                  |                    |          | DB9
1        | U2                  | MCP1754ST-3302E/MB | C632035  | 
1        | U3                  | TJA1051T/3         | C38695   | 
1        | X3                  |                    |          | Tag connect
1        | X1                  | 629722000214       | C2927039 | alternative zu Würth
1        | Y1                  | 830108313809       | C7294546 | alternative zu Würth

## Gehäuse
- STLs: https://github.com/linux-automation/candleLight/blob/master/case/case_upper.stl
- 2x Schraube M3x8 
- 2x Mutter M3 

Weil ich kein Fan mehr von 3D-gedruckten Gehäusen bin, nutze ich wenn möglich nur noch transparenten Schrumpfschlauch.

## Flashen

### Prüfen ob Bootloader aktiv

Ist der Controller leer, zeigt lsusb:

```
Bus 001 Device 026: ID 0483:df11 STMicroelectronics STM Device in DFU Mode
```

Der Boot-Pin versetzt den Chip nicht zuverlässig in den Bootloader mode. Um in den Bootloader zu gelangen muss per SWD der Chip gelöscht werden.

### Firmware bauen

siehe [make flash-candleLightFD_fw]()

### Firmware flashen

im build Ordner:
```
make flash-candleLightFD_fw
```
### Reboot

Stecker ziehen und wieder einstecken.

### Prüfen ob Firmware aktiv

lsusb sollte zeigen:

```
Bus 001 Device 015: ID 1d50:6018 OpenMoko, Inc. Black Magic Debug Probe (Application)
```

## Testen

Siehe hier: [https://linux-automation.com/en/products/candlelight-fd.html]() im Kapitel "First Steps"

```
sudo ip link set dev can0 up type can bitrate 500000 dbitrate 2000000 fd on
```

### Sender
```
cansend can0 213\#\#111223344
```

### Empfänger
```
cansend can0 213\#\#111223344
```
