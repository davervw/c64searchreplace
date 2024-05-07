# Search & Replace in binary file for Commodore #

Streams a file (seq or prg) from disk 8 replacing all occurances of *old* text with *new* text

* new text can be larger than old, or vice versa, or same length
* does work with BASIC files, as Commodore 64 will relink on load
* won't work with machine code or fixed data if change length as addresses/offsets will be off
* limited error checking
* should work with most 8-bit Commodores, written in generic BASIC

(c) 2024 Dave Van Wagner davevw.com
Open Source MIT License

![screenshot](screenshot.png)

````
10 print"searchreplace"
12 print"for commodore"
14 print"(c) 2024 davevw.com"
16 print"mit license"
18 print
20 print "search/replace binary"
22 print "file";
24 input fi$
26 print"[s]eq or [p]rg? ";
28 input ft$
30 print "old string:";
32 input ol$
34 print "new string:";
36 input nw$
38 open 1,8,0,fi$+","+ft$+",r"
40 if st<>0 then print "fail":clr:end
42 s1=st
44 nf$="results"
46 open 2,8,1,nf$+","+ft$+",w"
48 if st<>0 then print "fail":clr:end
50 iflen(sr$)>0thenc$=left$(sr$,1):sr$=mid$(sr$,2):goto 56
52 if s1<>0 then 74
54 get #1,c$:s1=st:if c$="" then c$=chr$(0)
56 if c$<>left$(ol$,1) then print#2,c$;:goto 50
58 sr$=c$+sr$
60 if sr$=ol$ then 72
62 if s1<>0 then 74
64 get#1,c$:s1=st:if c$="" then c$=chr$(0)
66 sr$=sr$+c$
68 ifsr$<>left$(ol$,len(sr$))thenprint#2,left$(sr$,1);:sr$=mid$(sr$,2):goto50
70 goto 60
72 print#2,nw$;:sr$="":goto52
74 print#2,sr$;
76 close 2
78 close 1
80 print "saved to ";nf$
82 end
````
