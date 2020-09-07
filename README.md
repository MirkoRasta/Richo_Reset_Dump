# Richo_Reset_Dump
Here is the way to reset the toner counter of Ricoh C232 and similar model (C231, C311, C311, C312, C320, C242, C342 and SPC231).

Inside the toner cartridge you can find a 24C02 EEPROM,
you can read it with a programmer (i've used a TL866A)
or even with an arduino, it works with I2C protocol,
you can find a video in the last lines which explain
how to do this.

Today i've read the dump of my Yellow Cartridge:


A8	00	01	03	32	04	01	FF	00	00	34	30	36	34	38	32       ¨ 2ÿ  406482  
09	09	41	42	19	00	03	48	00	00	00	00	00	00	00	00         AB H  
53	36	31	39	39	31	30	30	30	34	37	00	00	45	00	00       S6199100047  E  
00	00	0C	8B	00	00	02	7D	00	00	14	2D	00	00	0E	E6        ‹  }  -  æ  j  
00	00	0C	6A	00	00	00	00	00	00	00	00	00	00	00	00  
00	00	00	00	00	00	00	00	00	00	00	00	00	00	00	00  
00	01	02	A6	E0	3F	EC	3F	00	60	98	3E	32	00	00	04            ¦à ì    2  
47	A5	BB	0F	21	0A	CA	07	1F	1F	1F	1F	00	60	98	3E        G¥» ! Ê  
FF	FF	FF	FF	FF	FF	FF	FF	FF	FF	FF	FF	FF	FF	FF	FF       ÿÿÿÿÿÿÿÿÿÿÿÿÿÿÿÿÿ  
FF	FF	FF	FF	FF	FF	FF	FF	FF	FF	FF	FF	FF	FF	FF	FF       ÿÿÿÿÿÿÿÿÿÿÿÿÿÿÿÿÿ  
FF	FF	FF	FF	FF	FF	FF	FF	FF	FF	FF	FF	FF	FF	FF	FF       ÿÿÿÿÿÿÿÿÿÿÿÿÿÿÿÿÿ  
FF	FF	FF	FF	FF	FF	FF	FF	FF	FF	FF	FF	FF	FF	FF	FF       ÿÿÿÿÿÿÿÿÿÿÿÿÿÿÿÿÿ  
FF	FF	FF	FF	FF	FF	FF	FF	FF	FF	FF	FF	FF	FF	FF	FF       ÿÿÿÿÿÿÿÿÿÿÿÿÿÿÿÿÿ  
FF	FF	FF	FF	FF	FF	FF	FF	FF	FF	FF	FF	FF	FF	FF	FF       ÿÿÿÿÿÿÿÿÿÿÿÿÿÿÿÿÿ  
FF	FF	FF	FF	FF	FF	FF	FF	FF	FF	FF	FF	FF	FF	FF	FF       ÿÿÿÿÿÿÿÿÿÿÿÿÿÿÿÿÿ  
FF	FF	FF	FF	FF	FF	FF	FF	FF	FF	FF	FF	FF	FF	FF	FF       ÿÿÿÿÿÿÿÿÿÿÿÿÿÿÿÿÿ


I can only understand the dump in the 3rd row, that contains the
serial of the printer. If you delete this, the printer will
automatically re-write the serial in the eeprom so you can put all
these numbers to 0 (from "53" to "37"). I have only one printer
so i don't know if it will overwrite whit its serial
even if there is something other than 0 but i think it will.

The most important lines are the two final before all the FF:


A8	00	01	03	32	04	01	FF	00	00	34	30	36	34	38	32  
09	09	41	42	19	00	03	48	00	00	00	00	00	00	00	00  
53	36	31	39	39	31	30	30	30	34	37	00	00	45	00	00  
00	00	0C	8B	00	00	02	7D	00	00	14	2D	00	00	0E	E6  
00	00	0C	6A	00	00	00	00	00	00	00	00	00	00	00	00  
00	00	00	00	00	00	00	00	00	00	00	00	00	00	00	00  
00	01	02	A6	E0	3F	EC	3F	00	60	98	3E	32	00	00	00  
00	00	00	00	00	00	00	00	1F	1F	1F	1F	00	00	00	00  
FF	FF	FF	FF	FF	FF	FF	FF	FF	FF	FF	FF	FF	FF	FF	FF  
FF	FF	FF	FF	FF	FF	FF	FF	FF	FF	FF	FF	FF	FF	FF	FF  
FF	FF	FF	FF	FF	FF	FF	FF	FF	FF	FF	FF	FF	FF	FF	FF  
FF	FF	FF	FF	FF	FF	FF	FF	FF	FF	FF	FF	FF	FF	FF	FF  
FF	FF	FF	FF	FF	FF	FF	FF	FF	FF	FF	FF	FF	FF	FF	FF  
FF	FF	FF	FF	FF	FF	FF	FF	FF	FF	FF	FF	FF	FF	FF	FF  
FF	FF	FF	FF	FF	FF	FF	FF	FF	FF	FF	FF	FF	FF	FF	FF  
FF	FF	FF	FF	FF	FF	FF	FF	FF	FF	FF	FF	FF	FF	FF	FF


If you write four "0" after the four "1F" in the last line
(with last i mean the last before the "FF" area) and after the
"32" in the previous line, until the four "1F" you will reset
the copy counter. 


I've tried it only one time with my yellow toner but i think
it will work also with other colours.

I was inspired by a video on YouTube:
(https://www.youtube.com/watch?v=Wwd5UCi9Huw)
about these cartridge but it was a little different from mine,
so i had done this with the good old-fashioned bruteforce by 
reprogramming the eeprom several times until it works. 
In the future i will read the other colour and analyze the
yellow one afer few copies.
