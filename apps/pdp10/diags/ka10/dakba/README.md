---
layout: page
title: PDP-10 KA10 Basic Instruction Reliability Test #1
permalink: /apps/pdp10/diags/ka10/dakba/
machines:
  - id: testka10
    type: pdp10
    config: /devices/pdp10/machine/ka10/test/debugger/machine.xml
    debugger: true
    commands: a DAKBA.MAC
---

PDP-10 KA10 Basic Instruction Reliability Test #1
-------------------------------------------------

The *PDP-10 KA10 Basic Instruction Reliability Test #1* (MAINDEC-10-DAKBA) test code has been extracted from
[DAKBAM.MAC](DAKBAM.MAC.txt) [[original](http://pdp-10.trailing-edge.com/klad_sources/01/klad.sources/dakbam.mac.html)] and
[DAKBAT.MAC](DAKBAT.MAC.txt) [[original](http://pdp-10.trailing-edge.com/klad_sources/01/klad.sources/dakbat.mac.html)]
for use with the [PDP-10 Test Machine with Debugger](/devices/pdp10/machine/ka10/test/debugger/) below.

This test exercises "COMPARES, SKIPS, EXCHANGES, BOOLE, ROTATES, TESTS."

Information regarding this test includes:

- [Instructions](#dakbatxt)
- [History](#dakbahst)
- [Source Code](#dakbamac)
- [MACRO-10 Listing](DAKBA.LST.txt)
- [Additional Information](https://s3-us-west-2.amazonaws.com/archive.pcjs.org/apps/pdp10/diags/ka10/dakba/DAKBA.SEQ.txt)

{% include machine.html id="testka10" %}

The Debugger's assemble ("a") command can be used to test the new built-in
[MACRO-10 Mini-Assembler](/modules/pdp10/lib/macro10.js), which supports a subset
of the [MACRO-10](https://s3-us-west-2.amazonaws.com/archive.pcjs.org/pubs/dec/pdp10/tops10/02_1973AsmRef_macro.pdf) assembly language.
This command:

	a DAKBA.MAC

will automatically read the [DAKBA.MAC](DAKBA.MAC.txt) source file (a slightly modified copy of [DAKBAM.MAC](DAKBAM.MAC.txt)),
assemble it, and then load the binary image at the location specified in the file.

---

DAKBA.TXT
---------

```
MAINDEC-10-DAKBA.TXT






 
			IDENTIFICATION
			--------------

	PRODUCT CODE:   MAINDEC-10-DAKBA-B-D

	PRODUCT NAME:   DECSYSTEM10 PDP-10 KA10 BASIC
	                INSTRUCTION RELIABILITY TEST (1)

	FUNCTION:       COMPARES, SKIPS, EXCHANGES, BOOLE, ROTATES, TESTS

	VERSION:        0.2

	DATE RELEASED:  JANUARY 1977

	MAINTAINED BY:  DIAGNOSTIC ENGINEERING GROUP

	AUTHOR:         JOHN R. KIRCHOFF

COPYRIGHT(C) 1977
DIGITAL EQUIPMENT CORPORATION
MARLBORO, MASS. 01752

THIS SOFTWARE IS FURNISHED UNDER A LICENSE FOR USE ONLY
ON A SINGLE COMPUTER SYSTEM AND MAY BE COPIED ONLY WITH
THE INCLUSION OF THE ABOVE COPYRIGHT NOTICE.  THIS SOFTWARE,
OR ANY OTHER COPIES THEREOF, MAY NOT BE PROVIDED OR OTHERWISE
MADE AVAILABLE TO ANY OTHER PERSON EXECPT FOR USE ON SUCH SYSTEM
AND TO ONE WHO AGREES TO THESE LICENSE TERMS.  TITLE TO AND
OWNERSHIP OF THE SOFTWARE SHALL AT ALL TIMES REMAIN IN DEC.

THE INFORMATION IN THIS DOCUMENT IS SUBJECT TO CHANGE WITHOUT
NOTICE AND SHOULD NOT BE CONSTRUED AS A COMMITMENT BY DIGITAL
EQUIPMENT CORPORATION.

DEC ASSUMES NO RESPONSIBILITY FOR THE USE OR RELIABILITY OF ITS
SOFTWARE ON EQUIPMENT WHICH IS NOT SUPPLIED BY DEC.

							MAINDEC-10-DAKBA.TXT
							PAGE 2

			TABLE OF CONTENTS
			-----------------

1.0	ABSTRACT

2.0	REQUIREMENTS

2.1	EQUIPMENT

2.2	STORAGE

2.3	PRELIMINARY PROGRAMS

3.0	PROGRAM PROCEDURES

3.1	LOADING PROCEDURE

3.2	STARTING PROCEDURE

3.3	OPERATING PROCEDURE

4.0	DATA SWITCH FUNCTIONS

5.0	ERRORS

6.0	ITERATION COUNTER

7.0	CYCLE TIME

8.0	OPERATIONAL VARIATIONS

9.0	MISCELLANEOUS

10.0	LISTING

							MAINDEC-10-DAKBA.TXT
							PAGE 3

1.0	ABSTRACT

	THIS PDP-10 KA10 BASIC INSTRUCTION RELIABILITY TEST
	IS THE FIRST IN A SERIES OF PDP-10 KA10 PROCESSOR
	RANDOM NUMBER DIAGNOSTICS.

	THE DIAGNOSTIC TESTS COMPARES, SKIPS, EXCHANGES, BOOLE, ROTATES, TESTS.
	IN THE MAJORITY OF CASES EACH INSTRUCTION IS TESTED BY
	SIMULATING THE INSTRUCTION, WITH SIMPLER INSTRUCTIONS, AND
	THEN EXECUTING THE INSTRUCTION.  RANDOM NUMBERS ARE USED AS
	THE OPERANDS IN AC AND/OR C(E).  THE RESULTS OF THE
	SIMULATION AND EXECUTION ARE COMPARED AND AN ERROR MESSAGE
	IS PRINTED IF THE RESULTS ARE NOT EQUAL.

2.0	REQUIREMENTS

2.1	EQUIPMENT

	A PDP-10 KA10 EQUIPPED WITH A MINIMUM OF 32K OF MEMORY

	CONSOLE TELETYPE
	DECTAPE
	LINE PRINTER (OPTIONAL)

2.2	STORAGE

	THE PROGRAM RUNS WITHIN 32K OF MEMORY.

2.3	PRELIMINARY PROGRAMS

	PREVIOUS PROCESSOR DIAGNOSTICS
	
							MAINDEC-10-DAKBA.TXT
							PAGE 4

3.0	PROGRAM PROCEDURES

3.1	LOADING PROCEDURE

	THIS DIAGNOSTIC REQUIRES THAT THE DECSYSTEM10 SUBROUTINE
	PROGRAM BE RESIDENT IN THE PDP-10.

	DECTAPE - LOAD WITH DIAMON (DECTAPE DEVICE CODE 320)
	TIME SHARING - RUN UNDER DIAMON.

3.2	STARTING PROCEDURE

	A.  SELECT OPERATIONAL CONSOLE DATA SWITCH SETTINGS (REFER TO
	    4.0 DATA SWITCH FUNCTIONS).

	B.  EXEC MODE

	    STAND-ALONE STARTING ADDRESS IS 30000.

	C.  USER MODE

	    RUN UNDER "DIAMON".
	    IN USER MODE THE FOLLOWING QUESTIONS WILL BE ASKED TO 
	    SELECT THE OPERATIONAL SWITCHES:

		    TELETYPE SWITCH CONTROL ? 0,S,Y OR N (CR) -

		    IF THE OPERATOR TYPES "N", THE ACTUAL CONSOLE
		    SWITCHES ARE USED.

		    IF THE OPERATOR TYPES "Y", THE FOLLOWING QUESTIONS
		    ARE ASKED AND THE OPERATOR RESPONDS BY TYPING
		    THE ANSWER AS SIX OCTAL DIGITS REPRESENTING
		    THE DESIRED SWITCH SETTINGS.

		    SPECIFY LH SWITCHES IN OCTAL-

		    SPECIFY RH SWITCHES IN OCTAL-

		    IF THE OPERATOR TYPES "0", ZERO'S ARE USED FOR
		    THE SWITCH SETTINGS.

		    IF THE OPERATOR TYPES "S", PREVIOUSLY SET SWITCHES
		    ARE USED.  THIS IS ONLY VALID UPON RESTARTING
		    OF AN INTERRUPTED PROGRAM.
		    
							MAINDEC-10-DAKBA.TXT
							PAGE 5

3.3	OPERATING PROCEDURE

	NORMAL OPERATION WITH ALL SWITCHES SET TO ZERO IS QUICK
	VERIFY MODE.  TO RELIABILITY TEST SET THE "RELIAB" SWITCH.

	A.  TO THROUGHLY TEST ALL HARDWARE, ALL TEST CONTROL DATA 
	    SWITCHES SHOULD BE SET TO 0.

	B.  WHEN DEBUGGING HARDWARE, SET SWITCHES TO 0.  ALLOW THE 
	    TELETYPE TO PRINT THE ERROR MESSAGES.  THIS ALLOWS THE 
	    PROGRAM TO RUN A COMPLETE PASS AND THEN THE ERROR MESSAGES
	    MAY BE CORRELATED TO QUICKLY DIAGNOSE THE FAILURE.  IF A
	    HARDWARE PROBLEM IS SUCH THAT THE ERROR MESSAGES, AFTER THE
	    FIRST ONE, HAVE NO MEANING (FIRST ERROR CAUSES ALL FOLLOWING
	    TESTS TO FAIL) SET THE LOOP ON ERROR SWITCH AND RESTART THE
	    TEST FROM THE BEGINNING.  THE FIRST FAILURE WILL THEN CAUSE
	    THE PROGRAM TO ENTER A LOOP SUITABLE FOR SCOPING.

	    THE ERROR MESSAGE USED IN CONJUNCTION WITH THE LISTING AND
	    SCOPING IF NECESSARY SHOULD ALLOW THE FAILING CONPONENT 
	    TO BE ISOLATED AND REPLACED AND/OR REPAIRED.

	C.  WHEN TAKING MARGINS, SET DATA SWITCHES 'NOPNT' AND 'DING'.
	    THIS WILL INHIBIT PRINTOUT BUT WILL ALLOW THE TELETYPE
	    BELL TO BE RUNG WHEN A ERROR OCCURS.  IF THE MARGIN OBTAINED
	    IS UNACCEPTABLE, THE OPERATOR MAY REVERT TO STANDARD SWITCH
	    SETTINGS FOR DEBUGGING PURPOSES.

	D.  ERROR INFORMATION MAY BE OBTAINED QUICKLY BY PRINTING 
	    ERRORS ON THE LINE PRINTER.

	E.  IN THE EVENT OF A PRINT ROUTINE FAILURE THE 'NOPNT' SWITCH
	    AND THE 'ERSTOP' SWITCH MAY BE SET TO INHIBIT PRINTOUT 
	    BUT HALT THE PROGRAM POINTING TO THE ERROR.

							MAINDEC-10-DAKBA.TXT
							PAGE 6
4.0	DATA SWITCH FUNCTIONS

	SWITCH		STATE	FUNCTION
	------		-----	--------

	0    ABORT	0	NORMAL OPERATION
			1	ABORT AT END OF PASS

	1    RSTART		NOT USED

	2    TOTALS		NOT USED

	3    NOPNT	0	NORMAL TYPEOUT
			1	INHIBIT ALL PRINT/TYPEOUT (EXCEPT FORCED)

	4    PNTLPT	0	NORMAL OUTPUT TO TTY
			1	PRINT ALL DATA ON LPT

	5    DING	0	NO FUNCTION
			1	RING TTY BELL ON ERROR

	6    LOOPER	0	PROCEED TO NEXT TEST
			1	ENTER SCOPE LOOP ON TEST ERROR

	7    ERSTOP	0	NO FUNCTION
			1	HALT ON TEST ERROR

	8    PALERS	0	PRINT ONLY FIRST ERROR WHEN LOOPING
			1	PRINT ALL ERRORS, EVEN IF SAME ERROR

	9    RELIAB	0	FAST CYCLE OPERATION
			1	RELIABILITY MODE

	10   TXTINH	0	PRINT FULL ERROR MESSAGES.
			1	INHIBIT COMMENT PORTION OF ERROR MESSAGES.

	11   INHPAG		NOT USED

	12   MODDVC		NOT USED

	13   INHCSH		NOT USED
	
							MAINDEC-10-DAKBA.TXT
							PAGE 7

5.0	ERRORS

	ERRORS ARE PRINTED ON THE TTY OR LINE PRINTER.  THE ERROR 
	PRINTOUT CONTAINS THE TEST TITLE, THE PC OF THE FAILURE, AC
	NUMBER, ERROR WORD AND CORRECT WORD.

	THE PC VALUE IS USEFUL IN RELATING THE FAILURE TO THE LISTING.

	WHEN THE SCOPE LOOP MODE IS USED THE MI REGISTER WILL COUNT 
	FOR EACH OCCURANCE OF AN ERROR.  IF AN AUDIO INDICATION OF
	A CONTINUING ERROR IS DESIRED THE 'DING' SWITCH MAY BE SET.

	THE FOLLOWING IS THE DIFFERENT ERROR FORMATS WITH THEIR
	RESPECTIVE UUO'S AND ERROR MESSAGES.

	A.	ERROR #1  -  ERR   AC,E
	-------------------------------

	EXAMPLE:			AC		E
	2053 / CAME   AC1,AC2		;RESULT		CORRECT
	2054 / ERR    AC,RAN1		;ORIG  C(AC)	ORIG C(E)

	AC1=5				;TEST DATA
	C(AC1) = 201532107642
	C(AC2) = 201432107642
	C(RAN1)= 777777777777
	C(AC)  = 576345670135

	ERROR MESSAGE:

				   	(SOURCE OF NUMBERS PRINTED)
	PC =   002054			;PC OF ERROR UUO
	AC =   05			;AC FIELD OF UUO-1
	C(AC)= 201532107642		;C(C(AC)) OF UUO-1
	COR =  201432107642		;C(C(ADDRESS FIELD)) OF UUO-1
	    ORIGINAL
	C(AC)= 777777777777		;C(C(ADDRESS FIELD)) OF UUO
	C(E) = 576345670135		;C(C(AC)) OF UUO
	
							MAINDEC-10-DAKBA.TXT
							PAGE 8

5.0	ERRORS (CON'T)

	B.	ERROR #2  -  ERRM   AC,E
	--------------------------------

	EXAMPLE:			AC		E
	2053 / CAME   AC2,MUD		;CORRECT	RESULT
	2054 / ERRM   AC,RAN1		;ORIG  C(AC)	ORIG C(E)

	MUD=5033			;TEST DATA
	C(MUD) = 201532107642
	C(AC2) = 201432107642
	C(RAN1)= 777777777777
	C(AC)  = 576345670135

	ERROR MESSAGE:

				   	(SOURCE OF NUMBERS PRINTED)
	PC =   002054			;PC OF ERROR UUO
	E  =   5033			;BITS 18-35 (E) OF UUO-1
	C(E) = 201532107642		;C(C(E)) OF UUO-1
	COR =  201432107642		;C(C(AC)) OF UUO-1
	    ORIGINAL
	C(AC)= 777777777777		;C(C(E)) OF UUO
	C(E) = 576345670135		;C(C(AC)) OF UUO
	
							MAINDEC-10-DAKBA.TXT
							PAGE 9

5.0	ERRORS (CON'T)

	C.	ERROR #3  -  ERRI   AC,E
	--------------------------------

	EXAMPLE:			AC		E
	2053 / CAME   AC1,AC2		;RESULT		CORRECT
	2054 / ERRI   RAN1,(AC)		;ORIG C(AC)	ORIG E

	AC1=5				;TEST DATA
	C(AC1) = 107742670135
	C(AC2) = 107642670135
	C(RAN1)= 777777777777
	C(AC)  = 576345670135

	ERROR MESSAGE:

				   	(SOURCE OF NUMBERS PRINTED)
	PC =   002054			;PC OF ERROR UUO
	AC =   5			;AC FIELD OF UUO-1
	C(AC)= 107742670135		;C(C(AC)) OF UUO-1
	COR =  107642670135		;C(C(E)) OF UUO-1
	    ORIGINAL
	C(AC)= 777777777777		;C(C(AC)) OF UUO
	E    = 670135			;C(ADDRESS FIELD) OF UUO

	D.	ERROR #4  -  ERROR   AC,E
	---------------------------------

	EXAMPLE:			AC		E
	2053 / CAME   AC,RAN	
	2054 / ERROR  AC,RAN		;RESULT		CORRECT

	AC=5				;TEST DATA
	C(AC)  = 201532107642
	C(RAN) = 201432107642

	ERROR MESSAGE:

				   	(SOURCE OF NUMBERS PRINTED)
	PC =   002054			;PC OF ERROR UUO
	AC =   5			;AC FIELD OF UUO
	C(AC)= 201532107642		;C(C(AC)) OF UUO
	COR =  201432107642		;C(C(E)) OF UUO
	
							MAINDEC-10-DAKBA.TXT
							PAGE 10

5.0	ERRORS (CON'T)

	E.	ERROR #5  -  ER   AC,[ASCII/MESSAGE/]
	---------------------------------------------

	EXAMPLE:			AC		E
	2053 / JFCL   10,.+2	
	2054 / ER     AC,[ASCII/OV/]	;RESULT		MESSAGE

	AC=5				;TEST DATA
	C(AC)  = 201432107642

	ERROR MESSAGE:

				   	(SOURCE OF NUMBERS PRINTED)
	PC =   002054			;PC OF ERROR UUO
	AC =   5			;AC FIELD OF UUO
	C(AC)= 201432107642 OV		;C(C(AC)) OF UUO
					;ADDRESS FIELD OF UUO POINTS TO AN
					;ASCII MESSAGE

	F.	ERROR #6  -  ERM   AC,E
	-------------------------------

	EXAMPLE:			AC		E
	2053 / SOJ   AC2,	
	2054 / ERM    AC1,(AC2)		;C(AC)		RESULT

	C(AC2)=5033			;TEST DATA
	C(AC)  = 740000005756
	C(C(AC2)=254000004041

	ERROR MESSAGE:

				   	(SOURCE OF NUMBERS PRINTED)
	PC =   002054			;PC OF ERROR UUO
	E  =   5033			;BITS 18-35 (E) OF UUO
	C(AC)= 740000005756		;C(AC) OF UUO
	C(E) = 254000004041		;C(C(E)) OF UUO
	
							MAINDEC-10-DAKBA.TXT
							PAGE 11

5.0	ERRORS (CON'T)

	G.	ERROR #7  -  ERMM   AC,E
	--------------------------------

	EXAMPLE:			AC		E
	2053 / SOJ   AC2,	
	2054 / ERMM   AC1,(AC2)		;C(AC)		RESULT

	C(AC2)=5033			;TEST DATA
	C(AC1)  = 740000005756

	ERROR MESSAGE:

				   	(SOURCE OF NUMBERS PRINTED)
	PC =   002054			;PC OF ERROR UUO
	E  =   5033			;BITS 18-35 (E) OF UUO
	C(AC)= 740000005756		;C(AC) OF UUO


	H.	ERROR #11  -  EERR    ,E
	--------------------------------

	I.	ERROR #12  -  EERRM   ,E
	--------------------------------

	J.	ERROR #13  -  EERRI   ,E
	--------------------------------

	ERRORS 11,12 AND 13 ARE THE SAME AS ERRORS 1,2 AND 3 EXCEPT
	THAT THE AC OF THE UUO IS REPLACED BY C(RAN).  IN
	OTHER WORDS C(RAN) WILL BE PRINTED FOR THE ORIGINAL
	C(E).
							MAINDEC-10-DAKBA.TXT
							PAGE 12

6.0	ITERATION COUNTER

	THE ITERATION COUNT OF THE PROGRAM IS DISPLAYED IN THE MEMORY
	INDICATORS (MI).  THIS COUNT IS A DECREMENTING COUNT AND 
	INITIALLY STARTS AT -1 IN STAND-ALONE OPERATION.

7.0	CYCLE TIME

	A.  NORMAL OPERATION - APPROXIMATELY FIVE SECONDS.

	B.  RELIABILITY MODE - APPROXIMATELY 1.5 TO 3 MINUTES.

8.0	OPERATIONAL VARIATIONS

	A.  DIAGNOSTIC MONITOR

	    THE PROGRAM IS USABLE WITH THE DIAGNOSTIC MONITOR TO PROVIDE
	    RELIABILITY TESTS, ACCEPTANCE TESTS, AND/OR TO PROVIDE A
	    QUICK METHOD OF ISOLATION OF A FAULT TO A PARTICULAR AREA
	    OF THE PROCESSOR.  CERTAIN PROCEDURES ARE USED WHEN THE
	    PROGRAM IS USED IN THIS MANNER.  THEY ARE:

	    1.	THE DIAGNOSTIC MONITOR TRANSFERS CONTROL TO THE PROGRAM
		AND STARTS IT AT LOCATION 30002.

	    2.	MONCTL - LOCATION 30043 IS USED AS THE DIAGNOSTIC MONITOR
		CONTROL WORD.
			LH = 0, STAND-ALONE OPERATION
			    -1, RUNNING UNDER DIAGNOSTIC MONITOR

			RH = RIGHT HALF OF CONSOLE SWITCHES IF UNDER
			     DIAGNOSTIC MONITOR CONTROL.
			     
							MAINDEC-10-DAKBA.TXT
							PAGE 13

8.0	OPERATIONAL VARIATIONS (CON'T)

	B.  USER MODE

	    TO OUTPUT THE PRINTED ERROR MESSAGES TO A USER SPECIFIED
	    DEVICE IN USER MODE, ASSIGN THE DESIRED OUTPUT DEVICE TO
	    DEVICE NAME 'DEV' AND SET SWITCH 'PNTLPT'.  THE PHYSICAL
	    DEVICE USED CAN BE ANY DEVICE THAT CAN ACCEPT ASCII OUTPUT
	    FORMAT SUCH AS LPT, DSK, DTA, ETC.  THE CORRESPONDING 
	    OUTPUT FILE IS 'DAKBA.TMP'

	    EXAMPLE DEVICE ASSIGNMENT:

	    .ASSIGN DSK DEV

	    IN USER MODE THE PROGRAM WILL MAKE 1000(8) PASSES AND THEN
	    RETURN TO DIAMON COMMAND MODE.

	THE OUTPUT FILE (IF USED) MAY THEN BE LISTED BY USING THE
	NORMAL MONITOR COMMANDS (PRINT, LIST, TYPE, PIP, ETC.).

	IF THE PROGRAM IS ABORTED BEFORE COMPLETION (BY ^C, ETC.) THE
	OUTPUT FILE MAY BE CLOSED BY USING THE MONITOR 'REENTER' 
	COMMAND.

	C.  SYSTEM EXERCISER

	    START ADDRESS IS 30003.  DATA SWITCHES ARE PRESTORED IN
	    'SWTEXR' LOC 30023.

9.0	MISCELLANEOUS

	THE NON-EX-MEMORY AND PARITY STOP SWITCHES SHOULD BE RESET 
	(0).  THESE ERRORS, ILLEGAL UUO'S AND OTHER ERRORS OF THIS
	TYPE ARE HANDLED BY PRINTOUT ON THE TELETYPE.

10.0	LISTING
```

DAKBA.HST
---------

	    THIS IS A HISTORY OF THE DEVELOPMENT OF MAINDEC-10-DAKBA
	
	************************************************************************
	
	PRODUCT CODE:       MAINDEC-10-DAKBA
	
	PRODUCT NAME:       KA10 BASIC INSTRUCTION RELIABILITY # 1
	
	DATE RELEASED:      JANUARY 1977
	
	VERSION:            0.2
	
	UPDATE AUTHOR:      JOHN R. KIRCHOFF
	
	CHANGES MADE:
	
	    1. UPGRADE TO ALLOW COMPATABILITY WITH THE SUBROUTINE PACKAGE.
	    2. PROGRAM REPLACES OLD D0XX KA10 SERIES DIAGNOSTIC
	
	************************************************************************

DAKBA.MAC
---------

[[Download](DAKBA.MAC.txt)]
 
{% highlight text %}
{% include_relative DAKBA.MAC.txt %}
{% endhighlight %}
