# RAM-analysis-using-Volatile-Framework

Introducing Volatility-

Volatility is a free memory forensic tool; it is mainly used by malware and SOC analysts within a blue team (people who are on the defensive side in cyber security field). Volatility and its plugins are written in Python. Volatility framework extracts digital artifacts from volatile memory (RAM) samples. We use FTK imager tool for dumping the ram and investigate the dumped (.mem) file, we will be investigating in Windows operating system hence the extension is mem. It is freely available in Git (https://github.com/volatilityfoundation/volatility).

##How to Install Volatility

We need to install python, volatility3 framework and FTK imager. After installing all of them open FTK Imager and go to files and select capture memory.
Download links
Python: https://www.python.org/downloads/
Volatility framework: https://www.volatilityfoundation.org/
FTK Imager: https://www.exterro.com/ftk-imager

#Identifying Malicious Processes
When I receive a RAM dump from a device that may have been compromised, I prefer to check what programmes were active at the time the RAM dump was taken.

One adage that has always resonated with me is "malware can hide but it must run". A fantastic technique to try to find any malware that may be running on a device is to look at the running processes of the device.

#info
  The first plugin I will be using in Volatility is 'info,' which may be used to analyse currently running processes.
  python3 vol.py -f <filename> windows.info
  
#pslist
  The second plugin I will be using in Volatility is 'pslist,' which may be used to analyse currently running processes.

  python3 vol.py -f <filename> windows.pslist
  
#pstree
  The 'pstree' plugin is useful for determining the parent process of a running process, which can help identify suspicious activity. Attackers often name their     malware after legitimate Windows processes, but using 'pstree' can reveal if a process is running from an unexpected location or with an unusual parent process. For instance, 'taskhostw' should always run from '%systemroot%\system32\taskhostw.exe' with 'svchost.exe' as its parent process. Running 'pstree' with the Volatility framework in Python 3 on a memory image file can help identify any processes that may be malicious.
  
  python3 vol.py -f <filename> windows.pstree
  
#psscan
  The 'psscan' plugin is useful To enumerate processes using pool tag scanning (_POOL_HEADER), use the psscan command. This can find processes that previously terminated (inactive) and processes that have been hidden or unlinked by a rootkit. The downside is that rootkits can still hide by overwriting the pool tag values (though not commonly seen in the wild).
  
  python3 vol.py -f <filename> windows.psscan
  
#Identifying Malicious Network Connections
  
  When a RAM dump is taken, any network connections that were active at the time are also captured in the memory. This can be very helpful for incident responders because it allows them to identify any potentially malicious network activity, including the source port, destination IP address, destination port, and the related process.
  
#netscan
  The final plugin we will be using is netscan, which will help us identify network connections. When we captured the RAM dump at the same moment the network connections will also get stored in it, this will be helpful in identifying malicious destination IP, source port, destination port, and network activities related to the processes.

  python3 vol.py -f <filename> windows.netscan
  
  


