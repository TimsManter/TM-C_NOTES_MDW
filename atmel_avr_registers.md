# Atmel AVR Registers

## Overview

* @Author: TimsManter
* @AuthorSite: [TimsManter.NET](http://timsmanter.net/)
* @CreationDate: 2017-02

> TODO: Finish formatting

<!-- TOC -->

1. [Overview](#overview)
2. [TIMER 0/2](#timer-02)
  1. [TCNTn - timer counter r/w](#tcntn---timer-counter-rw)
  2. [TCCRn - timer settings (n == 0 or 2):](#tccrn---timer-settings-n--0-or-2)
3. [TIMER 1](#timer-1)
  1. [TCCR1A & TCCR1B](#tccr1a--tccr1b)
  2. [ATMEGA32:](#atmega32)
4. [Common for Timers](#common-for-timers)
  1. [TIMSK - enable timers interrupts:](#timsk---enable-timers-interrupts)
  2. [TIFR - timers interrupt flags, bits related to corresponding bits in TIMSK:](#tifr---timers-interrupt-flags-bits-related-to-corresponding-bits-in-timsk)
5. [INT0/1](#int01)
6. [INT0](#int0)
  1. [GICR](#gicr)
7. [Interrupt Vectors Table](#interrupt-vectors-table)
8. [Instructions](#instructions)

<!-- /TOC -->

## TIMER 0/2

### TCNTn - timer counter r/w

### TCCRn - timer settings (n == 0 or 2):

|		7			|		6			|		5			|		4			|		3		|		2		|		1		|		0		|
|	:---:		|	:---:		|	:---:		|	:---:		|	:---:	|	:---:	|	:---:	|	:---:	|
|	FOCn		|	WGMn0		|	COMn1		|	COMn0		|	WGMn1	|	CSn2	|	CSn1	|	CSn0	|


CSn2	|	CSn1	|	CSn0	|	Description
:---: | :---: | :---: | :---
0 | 0 | 0 | No clock
0 | 0 | 1 | No prescaler
0 | 1 | 0 | Prescaler 8
0 | 1 | 1 | Prescaler 64
1 | 0 | 0 | Prescaler 256
1 | 0 | 1 | Prescaler 1024
1 | 1 | 0 | External clock, failing edge
1 | 1 | 1 | External clock, rising edge


WGMn1 | WGMn0 | Mode
:---: | :---: | :---
0 | 0 | Normal
0 | 1 | PWM
1 | 0 | CTC, count to OCRn
1 | 1 | Fast PWM


ATMEGA32:
PB3 - OC0
PD7 - OC2


COMn1 | COMn0 | Mode
:---: | :---: | :---
0 | 0 | Normal port
0 | 1 | Toggle OCn on compate match
1 | 0 | Low OCn on compate match
1 | 1 | High OCn on compate match

## TIMER 1

### TCCR1A & TCCR1B

|		7			|		6			|		5			|		4			|		3		|		2		|		1		|		0		|
|	:---:		|	:---:		|	:---:		|	:---:		|	:---:	|	:---:	|	:---:	|	:---:	|
|	COM1A1	|	COM1A0	|	COM1B1	|	COM1B0	|	FOC1A	|	FOC1B	|	WGM11	|	WGM1	|
|	ICNC1		|	ICES1		|		-			|	WGM13		|	WGM12	|	CS12	|	CS11	|	CS10	|


|	WGM13	|	WGM12	|	WGM11	|	WGM10	|	Mode	|
|	:---:	|	:---:	|	:---:	|	:---:	|	:---	|
|		0		|		0		|		0		|		0		|	Normal
|		0		|		1		|		0		|		0		|	CTC, count to OCR1A


|	COM1(A/B)1	|	COM1(A/B)0	|	Mode	|
|			:---:		|			:---:		|	:---	|
|			0				|			0				|	Normal port
|			0				|			1				|	Toggle OC1(A/B) on compate match
|			1				|			0				|	Low OC1(A/B) on compate match
|			1				|			1				|	High OC1(A/B) on compate match

### ATMEGA32:
PD4 - OC1B
PD5 - OC1A

OCR1A & OCR1B - compare values in CTC (16 bit each)

## Common for Timers

### TIMSK - enable timers interrupts:

|		7			|		6			|		5			|		4			|		3			|		2		|		1		|		0		|
|	:---:		|	:---:		|	:---:		|	:---:		|	:---:		|	:---:	|	:---:	|	:---:	|
|	OCIE2		|	TOIE2		|	TICIE1	|	OCIE1A	|	OCIE1B	|	TOIE1	|	OCIE0	|	TOIE0	|


|		Bit		|	Timer	|	Type	|
|	:---		|	:---:	|	:---	|
|	TOIE0		|		0		|	Overflow
|	OCIE0		|		0		|	Compare
|	TOIE1		|		1		|	Overflow
|	OCIE1B	|		1		|	Comapre B
|	OCIE1A	|		1		|	Compare A
|	TICIE1	|		1		|	
|	TOIE2		|		2		|	Overflow
|	OCIE2		|		2		|	Compare

### TIFR - timers interrupt flags, bits related to corresponding bits in TIMSK:
```
OCF2 | TOV2 | ICF1 | OCF1A | OCF1B | TOV1 | OCF0 | TOV0
```

## INT0/1

MCUCR - INT0/1 settings
```
SE | SM2 | SM1 | SM0 | ICS11 | ICS10 | ICS01 | ICS00
```

## INT0
ISC01	ISC00	Trigger
0		0		Low
0		1		Toggle
1		0		High -> Low
1		1		Low -> High

### GICR
```
INT1 | INT0 | - | - | - | - | IVSEL | IVCE
```

## Interrupt Vectors Table

|	Address	|	Operation				|	Description	|
|	:---:		|	:---						|	:---	|
|	$000		|	RJMP INIT				|	Reset
|	$002		|	RJMP INT0				|	INT0
|	$004		|	RJMP INT1				|	INT1
|	$006		|	RJMP INT2				|	INT2
|	$008		|	RJMP TIM2_COMP	|	Timer2 Compare	
|	$00A		|	RJMP TIM2_OVF		|	Timer2 Overflow
|	$00C		|	RJMP TIM1_CAPT	|	Timer1 Capture	
|	$00E		|	RJMP TIM1_COMPA	|	Timer1 Compare A	
|	$010		|	RJMP TIM1_COMPB	|	Timer1 Compare B	
|	$012		|	RJMP TIM1_OVF		|	Timer1 Overflow	
|	$014		|	RJMP TIM0_COMP	|	Timer0 Compare	
|	$016		|	RJMP TIM0_OVF		|	Timer0 Overflow

## Instructions

Mnemonic	Description			Operation
INC Rd		Increment			Rd = Rd + 1
DEC Rd		Decrement			Rd = Rd - 1
CLR Rd		Clear				Rd = 0
SER Rd		Set				Rd = 0xFF
LSL Rd		Shift left
LSR Rd		Shift right

RJMP label	Jump to label (+- 2K)		GOTO label
RETI		Return from interrupt

CALL label
RET

SBR Rd, K	Set bits K in Rd		RdN = 1
CBR Rd, K	Clear bits K in RD		RdN = 0

SBRC Rd, N	Skip next if RdN clear	
SBRS Rd, N	Skip next if RdN set
CPSE Rd, Rr	Skip next if Rd == Rr		if Rd == Rr skip 1 instruction

CP Rd, Rr	Compare Rd and Rr
CPI Rd, K	Compare Rd and K	
BREQ label	Go to label if equal	
BRNE label	Go to label if not equal
BRGE label	Go to label if gr. or eq.
BRLO label	Go to label if lower
BRLT label	Go to label if lo. or eq.

SBI P, N	Set PortN
CBI P, N	Clear PortN

SBIC IO, n	Skip next if IOn clear
SBIS IO, n	Skip next if IOn set

LDI Rd, K	Load K to Rd			Rd = K
IN Rd, P	Load Port to Rd			Rd = P
OUT P, Rd	Load Rd to Port			P = Rd

LDS Rd, K	Load from SRAM to Rd		Rd = $K
STS K, Rd	Store Rd in SRAM		$K = Rd
