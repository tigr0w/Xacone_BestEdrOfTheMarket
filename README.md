
# <a href="https://xacone.github.io/BestEdrOfTheMarket.html"> Best EDR Of The Market (BEOTM) 🐲 </a>
<i>Little AV/EDR Evasion Lab for training & learning purposes.</i> (🏗️ under construction..)​


<img src="Assets/beotm_banner.png">

<br>BestEDROfTheMarket is a naive user-mode EDR (Endpoint Detection and Response) project, designed to serve as a testing ground for understanding and bypassing EDR's user-mode detection methods that are frequently used by these security solutions.
<br>These techniques are mainly based on a dynamic analysis of the target process state (memory, API calls, etc.), 

<a href="https://xacone.github.io/BestEdrOfTheMarket.html"><b>- Introducing the Best EDR Of The Market Project</b></a><br>
<a href="https://xacone.github.io/BestEdrOfTheMarketV2.html"><b>- Best EDR Of The Market v1.1.0</b></a>

## Defensive Techniques ⚔️​
- [x] <a href="#"> NT-Level API Hooking </a> <br>
- [x] <a href="#"> Kernel32/Base API Hooking </a> <br>
- [x] <a href="#"> Active Response w/ YARA rules or simple patterns </a> <br>
- [x] <a href="#"> SSN Hooking/Crushing </a> <br>
- [x] <a href="#"> IAT Hooking </a> <br>
- [x] <a href="#"> Threads Call Stack Monitoring (Stacked parameters + Unbacked addresses) </a> <br>
- [x] <a href="#"> Heap Regions Analysis </a> <br>
- [x] <a href="#"> Direct Syscalls Detection </a> <br>
- [x] <a href="#"> Indirect Syscalls Detection </a> <br>
- [ ] <a href="#"> AMSI/ETW Patching Mitigation </a> <br>



<i>In progress</i>:
- [ ] <a href="#"> Call Stack Spoofing Mitigation </a> <br>
- [ ] <a href="#"> Proper Threads Creation Monitoring </a> <br>
- [ ] <a href="#"> AMSI Scanning </a> <br>

## Examples⚡

<details>
  <summary><b>Shellcode injectors detection (Unbacked functions regions analysis + YARA)</b></summary>
  
  <code>BestEdrOfTheMarket.exe /v </code>
 
  
</details>

<details>
  <summary><b>APC Queue Early Bird Injector detection (Kernel32 hooking + YARA)</b></summary>


</details>

<details>
  <summary><b>Early Bird  APC Queue Injector detection (IAT hooking + YARA)</b></summary>

</details>

<details>
  <summary><b>Low level Early Bird APC Queue Injector detection (Stacked functions parameters + YARA / Custom patterns)</b></summary>
    
   <pre><code>BestEdrOfTheMarket.exe /v /stack /yara /p C:\Malwares\early_bird_apc.exe</code></pre>


   <pre><code>BestEdrOfTheMarket.exe /v /stack /p C:\Malwares\early_bird_apc.exe</code></pre>



</details>

<details>
  <summary><b>Indirect Syscalls Detection (Stack pointer sanity check)</b></summary>

  BEOTM vs Hell's Hall (by @Maldev-Academy)



</details>

<details>
  <summary><b>Direct Syscalls Detection (Instruction pointer sanity check)</b></summary>



</details>

<details>
  <summary><b>Reflective DLL Injector (Heap analysis 9 YARA)</b></summary>

</details>

<details>
  <summary><b>AMSI Patcher detection</b></summary>

</details>


<br>
<!--<a href="#"> Performance brief </a> <br>-->

<img src="Assets/beotmgif1.gif">

## Usage 📜
```
Usage: BestEdrOfTheMarket.exe [args]

      /help : Shows this help message and quit
      /v : Verbosity  
      /yara : Enabling YARA rules
      /iat : IAT hooking
      /stack : Threads call stack monitoring
      /nt : Inline Nt-level hooking
      /k32 : Inline Kernel32/Kernelbase hooking
      /ssn : SSN crushing
      /direct : Direct syscalls detection
      /indirect : Indirect syscalls detection
      /heap : Heap regions analysis (to use with /k32 or /nt)

```
```
BestEdrOfTheMarket.exe /stack /v /k32
BestEdrOfTheMarket.exe /stack /nt
BestEdrOfTheMarket.exe /iat
```

## Structure & Config files ⚙️
```
📁 BestEdrOfTheMarket/
    📄 BestEdrOfTheMarket.exe
    📁 DLLs/
        📄 Kernel32.dll
        📄 ntdll.dll
        📄 iat.dll
        📄 callbacks.dll
        📄 magicbp.dll
    📁 YARA/
        📄 Metasploit_Artefacts_Rule.yara
        📄 ...
    📝 YaroRules.json
    📄 jsoncpp.dll
```

<b>YaroRules.json: </b>Contains a json array filled with the patterns you would like to be identified while monitoring threads call stacks.
```json
{
	"Patterns": [
		"d2 65 48 8b 52 60 48 8b 52 18 48 8b 52 20 48 8b 72 50 48",
		"49 be 77 73 32 5f 33 32 00 00",
                "..."
    ]
}
```

If you don't compile your own DLLs, take a look at the functions already hooked into the DLLs provided <a href="DLLs/">in sources</a>.

## <a href="https://github.com/Xacone/BestEdrOfTheMarket/releases/tag/Beta">Releases</a> 📦

## <a href="Docs/Setup.md"> Project Setup & Crafting your own hooks 🛠</a> 

## Disclaimer ⚠️​
- There's no interest in mixing the defensive methods or in putting them all (/nt + /stack + /k32 + /blahblah) as you may encounter crashes due to conflicts beetwen them, especially for low level hooks. Activate the one you want depending on your needs. 
- Don't link the EDR to programs that are too CPU-intensive/thread-creating, as some detection techniques such as call stack analysis constantly monitor the stack state of each thread and this can quickly increase the load on the EDR, it's more relevant (that's also the point) that you link the tool to your own artifacts and keep in mind that a good evasive artifact tries to be as discrete as possible.