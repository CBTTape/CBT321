# CBT321
Converted to GitHub via [cbt2git](https://github.com/wizardofzos/cbt2git)

This is still a work in progress. 
Due to amazing work by Alison Zhang and Jake Choi repos are no longer deleted.

```
//***FILE 321 is from Roland Schiradin of Eltville, Germany.        *   FILE 321
//*           This file contains several programs:  One is a        *   FILE 321
//*           COBOL load module analyzer, which will tell you       *   FILE 321
//*           what options a COBOL CSECT was compiled with.         *   FILE 321
//*           Another is a started task tester, to check if a       *   FILE 321
//*           certain started task is running, and to set a         *   FILE 321
//*           condition code in a batch job as a result.            *   FILE 321
//*                                                                 *   FILE 321
//*           Addition of a CICS CEMT interface for batch.          *   FILE 321
//*           Addition of a CICS CEDA INSTALL interface for batch   *   FILE 321
//*                                                                 *   FILE 321
//*       ADDRESS:   ROLAND SCHIRADIN                               *   FILE 321
//*                  TAUSUSSTR 52                                   *   FILE 321
//*                  65343 ELTVILLE, GERMANY                        *   FILE 321
//*                                                                 *   FILE 321
//*       PHONE:     49-172-1435398                                 *   FILE 321
//*                                                                 *   FILE 321
//*       EMAIL:     ROLAND@SCHIRADIN.DE (fix)                      *   FILE 321
//*                                                                 *   FILE 321
//*     Roland Schiradin (August 2024)                              *   FILE 321
//*                                                                 *   FILE 321
//* --------------------------------------------------------------  *   FILE 321
//*                                                                 *   FILE 321
//*     These programs are distributed on an as is, where is        *   FILE 321
//*     basis, without expressed or implied warranty of any         *   FILE 321
//*     kind. It is distributed in hope that it may save other      *   FILE 321
//*     people some wheel re-inventing.                             *   FILE 321
//*                                                                 *   FILE 321
//* --------------------------------------------------------------  *   FILE 321
//*                                                                 *   FILE 321
//*       -------------------  Index  ---------------------         *   FILE 321
//*                                                                 *   FILE 321
//*                                                                 *   FILE 321
//*  COBANAL   Frozen version, only bug-fixes                       *   FILE 321
//*            This version support pre OS/390 R10                  *   FILE 321
//*                                                                 *   FILE 321
//*            Last Change: April 2002                              *   FILE 321
//*                                                                 *   FILE 321
//*  COBANALJ  A sample JCL to assemble CobAnal or CobAnalZ         *   FILE 321
//*                                                                 *   FILE 321
//*            Last Change: November 2002                           *   FILE 321
//*                                                                 *   FILE 321
//*  COBANALZ  This Program analyze your Cobol-Load-Modules.        *   FILE 321
//*            There is no need for the source. Support             *   FILE 321
//*            for single programs also for a complete load-lib.    *   FILE 321
//*            This program require the STRING macro from FILE183.  *   FILE 321
//*            I have include the current versions of STRING        *   FILE 321
//*            Thanks to Gilbert Saint-Flour                        *   FILE 321
//*                                                                 *   FILE 321
//*            Full support for Enterprise Cobol V3                 *   FILE 321
//*            Full support for COBOL for OS/390 & VM V2            *   FILE 321
//*            Full support for COBOL for OS/390 & VM V1            *   FILE 321
//*            Full support for COBOL for MVS and VM formally called*   FILE 321
//*            COBOL/370 or ADCYLE COBOl/370.                       *   FILE 321
//*            Full support for COBOL-II every version.             *   FILE 321
//*            Few support for COBOL-I.                             *   FILE 321
//*                                                                 *   FILE 321
//*            If you have old or newer Cobol-Programs please       *   FILE 321
//*            send me the Load to Roland(at)Schiradin.de. I'll     *   FILE 321
//*            add some code to support those Cobol-Versions.       *   FILE 321
//*                                                                 *   FILE 321
//*            If you like to get the newest Version please contact *   FILE 321
//*            Roland(at)Schiradin.de                               *   FILE 321
//*                                                                 *   FILE 321
//*            Last Change: November 2007                           *   FILE 321
//*                                                                 *   FILE 321
//*  COBJCL    A sample JCL for COBANAL                             *   FILE 321
//*                                                                 *   FILE 321
//*            Last Change: November 2006                           *   FILE 321
//*                                                                 *   FILE 321
//*  EXCIJCL   Sample JCL to invoke the CICS-Batch-Interface        *   FILE 321
//*                                                                 *   FILE 321
//*            Last Change: March 1999                              *   FILE 321
//*                                                                 *   FILE 321
//*  EXCIRDO   CSD for CICS 4.1 and higher                          *   FILE 321
//*                                                                 *   FILE 321
//*            Last Change: March 1999                              *   FILE 321
//*                                                                 *   FILE 321
//*  EXCI      The CEMT-Batch-Interface written in Cobol            *   FILE 321
//*            Note: You need the EXCI-Stub (DFHEXLI) in your       *   FILE 321
//*            BIND-Job !!!! Please specify EXCI and COBOL3 as      *   FILE 321
//*            the precompiler option.                              *   FILE 321
//*                                                                 *   FILE 321
//*            Last Change: March 1999                              *   FILE 321
//*                                                                 *   FILE 321
//*  EXCISE    The CICS-Server-Program written in Assembler.        *   FILE 321
//*            Please expand the program to your needs.             *   FILE 321
//*                                                                 *   FILE 321
//*            Last Change: March 1999                              *   FILE 321
//*  STCCHECK  This program check if a started Task is allready     *   FILE 321
//*            active. This avoid abend U1800 if a operator         *   FILE 321
//*            start the same CICS again. Please note this works    *   FILE 321
//*            only on the same MVS-image, I'll add somtimes        *   FILE 321
//*            code to check the SYSPLEX.                           *   FILE 321
//*                                                                 *   FILE 321
//*            //*******************  EXECUTE CICS                  *   FILE 321
//*            //*****************************************          *   FILE 321
//*            //STCCHECK EXEC PGM=STCCHECK,PARM='DCCA201'          *   FILE 321
//*            //SYSPRINT  DD SYSOUT=*                              *   FILE 321
//*            //SYSUDUMP  DD SYSOUT=D                              *   FILE 321
//*            //*****************************************          *   FILE 321
//*            //DCCSTRT IF (STCCHECK.RC = 0) THEN                  *   FILE 321
//*            //DCCA201 EXEC PROC=DCICSA                           *   FILE 321
//*            //EDCCSTRT ENDIF                                     *   FILE 321
//*                                                                 *   FILE 321
//*            rc = 0   DCCA201 is not active                       *   FILE 321
//*            rc not 0 DCCA201 is active                           *   FILE 321
//*                                                                 *   FILE 321
//*            Last Change: March 1998                              *   FILE 321
//*                                                                 *   FILE 321
//*  STRING    Provides functions similar to PL/I's                 *   FILE 321
//*            PUT EDIT or COBOL's STRING.                          *   FILE 321
//*                                                                 *   FILE 321
//*            Taken from FILE183.                                  *   FILE 321
//*                                                                 *   FILE 321
//*  STRING64  Provides functions similar to PL/I's                 *   FILE 321
//*            PUT EDIT or COBOL's STRING.                          *   FILE 321
//*            Partial 64bit support.                               *   FILE 321
//*                                                                 *   FILE 321
//*  SYEXCIC   Cobol-Source to invoke the CEDA INSTALL from Batch   *   FILE 321
//*                                                                 *   FILE 321
//*            Last Change: March 1996                              *   FILE 321
//*                                                                 *   FILE 321
//*  SYEXCIS   Assembler-Source to invoke the CEDA INSTALL          *   FILE 321
//*                                                                 *   FILE 321
//*            Last Change: March 1996                              *   FILE 321
//*  --------------------------------------------------------       *   FILE 321
//*                                                                 *   FILE 321
```
