![Shape Description automatically
generated](vertopal_1ff9736b36fd4fbe9eb809638d3a3928/media/image1.png){width="5.889550524934383in"
height="2.0681813210848645in"}

Submitted by

Name: Ankit Kumar Singh

Roll no: 53.

Reg no: 11910439

Course code: INT301

CA-3

> [INTRODUCTION]{.underline}
>
> [Objective]{.underline}

Investigate the system run time state of a device (RAM), extract the
information present in RAM with the help of volatility Framework.

> [Description]{.underline}

Volatility is a free memory forensic tool; it is mainly used by malware
and SOC analysts within a blue team (people who are on the defensive
side in cyber security field). Volatility and its plugins are written in
Python. Volatility framework extracts digital artifacts from volatile
memory (RAM) samples. We use FTK imager tool for dumping the ram and
investigate the dumped (.mem) file, we will be investigating in Windows
operating system hence the extension is mem.

> [Scope]{.underline}

This project is based on analysing the dumped RAM memory through various
techniques and finding out information regarding the system like
processes, build version, architecture etc, and detecting malwares and
rootkits which may be hidden in processes.

[System Description]{.underline}

OS: Windows 10

Processor: AMD Ryzen 9 5900HX

RAM: 16 GB

System type: 64-bit operating system

> [Analysis report]{.underline}

**[Step 1:]{.underline}**

We need to install python, volatility3 framework and FTK imager. After
installing all of them open FTK Imager and go to files and select
capture memory.

![](vertopal_1ff9736b36fd4fbe9eb809638d3a3928/media/image2.jpeg){width="6.304812992125984in"
height="3.4916666666666667in"}

*Download links*

Python:
[https://www.python.org/downloads/](https://www.youtube.com/redirect?event=video_description&redir_token=QUFFLUhqbFEyLUdTWWRRQkN5SWZjczRRRXJZN3Q2SzRMUXxBQ3Jtc0tsRVZTMElUSWVtOV9OaE5FNm02Y1JyNG1qa2VYTnFLcjVNdTI2S0prZ01CNnBlU3JOYnBvQmIwRXNPeXdhUGRGcGVzV2FzLXRUcXY4YUdDX2VDZ3FMS2lsOEQwSmN6UG9xSjJoV01ubHJVcWk2RWliWQ&q=https%3A%2F%2Fwww.python.org%2Fdownloads%2F&v=-bMde2glwnE)

Volatility framework:
[https://www.volatilityfoundation.org/](https://www.youtube.com/redirect?event=video_description&redir_token=QUFFLUhqbE0wR0VwSFdXSnV2b3ZlQ0hWRDRNelBULUdid3xBQ3Jtc0trT0VkX01LaDBQR1hIUm5odks4NWFYVEtsZV9YaDdSODRtSzFxUXV4X1BHM0VXTHdBU3l1dWhlOFZLVS1xU2pMSTcwZmd5RUViR21GMTQyaXAtWU9sSzNMUmZVLVd6OWxDc0p3TnlzTUtpOHlSdFoxbw&q=https%3A%2F%2Fwww.volatilityfoundation.org%2F&v=-bMde2glwnE)

FTK Imager:
[https://www.exterro.com/ftk-imager](https://www.youtube.com/redirect?event=video_description&redir_token=QUFFLUhqbE9kYzQ5cHVNaWhhVFFJcnBjSEpJUzhQeVhPZ3xBQ3Jtc0trYURLOUhJYnliX3YySldMeWlBWDJYVFdiSUFGQzNNWURlNGRzbXo0ZWhqN096ems1NDg4S041dkRiXzVIVnBUZlQyLXBxSjNJRWRzZnNWWDRMUlRiMWFUNTdsN3l0ZXVaSDlfYnphT0hPYkY5ZHlMdw&q=https%3A%2F%2Fwww.exterro.com%2Fftk-imager&v=-bMde2glwnE)

**[Step 2]{.underline}**

Then we create a memory dump of RAM, by clicking on capture memory and
browsing it to your favourable location. In my case here it was around
16.4 gb.

![Graphical user interface, application Description automatically
generated](vertopal_1ff9736b36fd4fbe9eb809638d3a3928/media/image3.jpeg){width="6.268055555555556in"
height="3.109027777777778in"}

**[Step 3]{.underline}**

Now we need to open our command prompt in the same location where we
stored our captured memory, I have created a folder named
"dump_analysis" where the memdump.mem (memory dump of RAM) is stored.

![Graphical user interface Description automatically generated with
medium
confidence](vertopal_1ff9736b36fd4fbe9eb809638d3a3928/media/image4.jpeg){width="6.268055555555556in"
height="0.9493055555555555in"}

**[Step 4]{.underline}**

Now after opening command prompt, we need to type: "python vol.py" to
check if it's installed or not, for that we need to be in the same
directory where you have installed volatility. We can view help by
typing: "python vol.py -h" command.

**[Step 5]{.underline}**

Since I am using volatility on windows 10, I need to know the
information of the memory dump. So, we will use the "windows.info"
plugin for gaining information like, processor and architecture version
of the memory.

Syntax: python vol.py -f "\<filename with path\>" windows.info

![Text Description automatically
generated](vertopal_1ff9736b36fd4fbe9eb809638d3a3928/media/image5.jpeg){width="6.268055555555556in"
height="3.3048611111111112in"}

**[Step 6]{.underline}**

Now we are going to list processes using the plugin "pslist", this
plugin will get the list of processes from doubly linked list that keeps
track of processes in memory. It's like viewing task manager.

Syntax: python vol.py -f "\<filename with path\>" windows.pslist

![](vertopal_1ff9736b36fd4fbe9eb809638d3a3928/media/image6.jpeg){width="6.268055555555556in"
height="2.9097222222222223in"}

**[Step 7]{.underline}**

What we did above was simply listing processes, but sometimes we need to
find malicious activity to prevent damage that a malware can do, they
hide themselves by unlinking themselves from the list and we won't be
able to see their process. So, to counter this evasion technique use
"psscan" this technique can help locate processes by finding the data
structure that match \_EPROCESS. But this listing technique can also
result in false positives.

Syntax: python vol.py -f "\<filename with path\>" windows.psscan

![](vertopal_1ff9736b36fd4fbe9eb809638d3a3928/media/image7.jpeg){width="6.268055555555556in"
height="2.2125in"}

**[Step 8]{.underline}**

Sometimes it is useful if we know the full story of processes and what
may have occurred during extraction, for this purpose we will be using
"pstree" plugin it will list all processes based on their parent process
ID.

Syntax: python vol.py -f "\<filename with path\>" windows.pstree

![](vertopal_1ff9736b36fd4fbe9eb809638d3a3928/media/image8.jpeg){width="6.268055555555556in"
height="2.8625in"}

**[Step 9]{.underline}**

Now we will be using the plugin "dlllist" it will list all DLLs
associated with processes at the time of extraction. This can be
especially helpful once you have done further analysis and can filter
output to a specific DLL that might be an indicator for a specific type
of malware that might be present in the system.

Syntax: python vol.py -f "\<filename with path\>" windows.dlllist

![](vertopal_1ff9736b36fd4fbe9eb809638d3a3928/media/image9.jpeg){width="6.268055555555556in"
height="2.522222222222222in"}

**[Step 10]{.underline}**

There are many plugins that are used for hunting and detecting malwares
in a system using volatility one of them being "malfind". This is useful
when hunting for code injection, it identifies injected processes and
their PID's along with their offset address and a Hex, ascii and
disassembly view of the infected area.

Syntax: python vol.py -f "\<filename with path\>" windows.malfind

![](vertopal_1ff9736b36fd4fbe9eb809638d3a3928/media/image10.jpeg){width="6.268055555555556in"
height="3.272222222222222in"}

**[Step 11:]{.underline}**

The final plugin we will be using is netscan, which will help us
identify network connections. When we captured the RAM dump at the same
moment the network connections will also get stored in it, this will be
helpful in identifying malicious destination IP, source port,
destination port, and network activities related to the processes.

Syntax: python vol.py -f \<filename\> windows.netscan

![](vertopal_1ff9736b36fd4fbe9eb809638d3a3928/media/image11.png){width="6.268055555555556in"
height="3.3319444444444444in"}

[Reference]{.underline}

1.  <https://www.varonis.com/blog/how-to-use-volatility>

2.  <https://infosecwriteups.com/forensics-memory-analysis-with-volatility-6f2b9e859765>

3.  [https://github.com/volatilityfoundation/volatility]{.underline}

Github link of my project: https://github.com/Barman7085/INT301_CA3
