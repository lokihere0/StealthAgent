# **<i>StealthAgent</i>**:


<i>Self-Extracting EXE & DLL Protector for Covert Payloads</i>

- ![Project](https://img.shields.io/badge/Project-StealthAgent-blue?style=flat-square)
- ![Version](https://img.shields.io/badge/Version-1.0.0-blue?style=flat-square)
- ![Status](https://img.shields.io/badge/Status-Stable-brightgreen?style=flat-square)

---
## Disclaimer

**StealthAgent** is intended for **security professionals** and **ethical hackers**. Unauthorized use is illegal.

- Always comply with the legal framework in your jurisdiction.
- The creators of this project are not responsible for any misuse or illegal actions.

I do not take any responsibility for this tool's usage in for malicious purposes. It is free and provided AS-IS for everyone.


---
## **Glossary**

- **EXE**: Executable file format used on Windows systems.
- **DLL**: Dynamic Link Library, a file containing code and data that can be used by other programs.
- **XOR**: A logical operation that compares bits and returns true when the bits are different.
- **RLE**: Run-Length Encoding, a basic form of data compression.
- **MinGW**: Minimalist GNU for Windows, a development environment for compiling native Windows applications.

---

# **Transform and Protect Your Executables**  
Secure your EXEs, embed them inside stealthy DLLs, and deliver your payloads covertly. From XOR encryption to custom compression, StealthAgent provides the tools you need for enhanced security and stealth.

---

# Table of Contents

1. Credits
2. Overview
3. Key Features
4. System Requirements
5. Installation Instructions
6. Self-Extracting EXE Generator
7. DLL with Embedded EXE
8. In-Depth Technical Walkthrough
9. Advanced Customization
10. Security Considerations
11. Troubleshooting & FAQs

---
## **Credits**

This project incorporates and acknowledges the following important contributions:

- **UACME Project**:  
   The **User Account Control (UAC) bypass** techniques used in StealthAgent are based on the excellent work of [hfiref0x](https://github.com/hfiref0x/) and the **UACME** project.  
- **UACME GitHub Repository**: [Click here](https://github.com/hfiref0x/UACME/) to access the project.

We extend our gratitude to the community for their contributions to this project.

---



<b>This project follows the license specified in the **UACME** repository, as follows: </b>

---

> **UACME Project License**  
> *Copyright (c) 2014 - 2024, UACMe Project*  
> Redistribution and use in source and binary forms, with or without modification, are permitted provided that the following conditions are met:  
> - Redistributions of source code must retain the copyright notice, this list of conditions, and the following disclaimer.  
> - Redistributions in binary form must reproduce the above copyright notice, this list of conditions, and the following disclaimer in the documentation and/or other materials provided with the distribution.  
> 
> **THIS SOFTWARE IS PROVIDED "AS IS", WITHOUT ANY EXPRESS OR IMPLIED WARRANTIES** (INCLUDING, BUT NOT LIMITED TO, THE IMPLIED WARRANTIES OF MERCHANTABILITY OR FITNESS FOR A PARTICULAR PURPOSE), AND IN NO EVENT SHALL THE COPYRIGHT HOLDER OR CONTRIBUTORS BE LIABLE FOR ANY DIRECT, INDIRECT, INCIDENTAL, SPECIAL, EXEMPLARY, OR CONSEQUENTIAL DAMAGES (INCLUDING, BUT NOT LIMITED TO, PROCUREMENT OF SUBSTITUTE GOODS OR SERVICES; LOSS OF USE, DATA, OR PROFITS; OR BUSINESS INTERRUPTION) HOWEVER CAUSED AND ON ANY THEORY OF LIABILITY, WHETHER IN CONTRACT, STRICT LIABILITY, OR TORT (INCLUDING NEGLIGENCE OR OTHERWISE) ARISING IN ANY WAY OUT OF THE USE OF THIS SOFTWARE, EVEN IF ADVISED OF THE POSSIBILITY OF SUCH DAMAGE.

---

## **Overview**

**StealthAgent** is a comprehensive toolkit designed to secure, encrypt, and stealthily deploy executable files (EXEs) by embedding them inside self-extracting EXEs or DLLs. It is intended for developers, penetration testers. 

<b>StealthAgent employs techniques such as:</b>

- **XOR Encryption** for lightweight, fast obfuscation.
- **Run-Length Encoding (RLE)** for compression of payloads without sacrificing stealth.
- **Random Padding** to generate unique file hashes, thwarting signature-based detection.

### **Key Features:**

- **Self-Extracting EXE** creation that unpacks and runs the embedded payload without leaving traces on disk.
- **Encrypted EXE embedding** into stealthy DLLs, ideal for integration with legitimate software.
- **Advanced obfuscation & encryption** techniques, including XOR encryption and custom padding.
- **High versatility**, supporting both EXE and DLL formats for different deployment strategies.

| Feature                 | Description                                                                            |
|-------------------------|----------------------------------------------------------------------------------------|
| **Encryption**          | XOR-based encryption with a unique key for every file.                                |
| **Compression**         | Proprietary compression reduces size without compromising data integrity.             |
| **Execution**           | Seamless in-memory execution via dynamically created DLLs.                            |
| **Compatibility**       | Works flawlessly with Windows systems and GCC.                                        |
| **Stealth**             | Randomized data injection ensures detection evasion.                                  |

---

---

## **Attributes**

### 1. **XOR Encryption**
   - **What is it?** A symmetric encryption technique that obfuscates your EXE files.
   - **Why it matters:** Ensures that even if your EXE is intercepted, its contents remain unreadable unless the key is known.

### 2. **Run-Length Encoding (RLE) Compression**
   - **What is it?** A data compression method that reduces file size by encoding repeating byte sequences.
   - **Why it matters:** Minimizes the payload size, improving efficiency while maintaining stealth.

### 3. **Random Padding for Unique Hashes**
   - **What is it?** Padding added to your encrypted payload to generate a unique file hash every time.
   - **Why it matters:** Prevents signature-based detection and makes reverse engineering more difficult.

### 4. **Self-Extracting EXE Creation**
   - **What is it?** A generated EXE that unpacks and runs the embedded payload in a streamlined process.
   - **Why it matters:** Ensures no remnants are left on disk, reducing detection by antivirus tools.

### 5. **DLL with Embedded EXE**
   - **What is it?** A DLL that holds and executes your EXE as part of the DLL's operations. Useful for embedding payloads into legitimate software or during post-compilation processes.
   - **Why it matters:** Enables stealthy execution within another application or system process.

---
## ️ Usage Instructions

### 1. **Prepare the Environment**
Ensure the following tools are installed on your system:
- GCC (MinGW recommended for Windows systems)
- A compatible EXE file for encryption

### 2. **Encrypt Your EXE File into a SFX File**
```bash
exeagent.exe --exe-path <path_to_your_exe> --output <path_to_output.exe> --gcc-path <path_to_gcc>
```
### 2. **Encrypt Your EXE File into a DLL**
```bash
dllagent.exe --exe-path <path_to_your_exe_or_sfx_file> --output <path_to_output.dll> --gcc-path <path_to_gcc>
```

### 3. **Execute the DLL**
- Place the DLL in a secure directory.
- Use a loader to run the DLL or integrate it into your application.
```bash
regsvr32 output.dll
```


---

## **In-Depth Technical Walkthrough**

### **XOR Encryption and Decryption**  
XOR encryption applies a key to each byte of the EXE file. The same key is used for both encryption and decryption. Though simple, it offers effective obfuscation.

### **Run-Length Encoding (RLE) Compression**  
RLE reduces payload size by converting repeating byte sequences into a more compact format. This helps reduce the EXE size and adds another layer of obfuscation.

### **Random Padding for Unique Hashes**  
Padding ensures that every generated file has a unique fingerprint, preventing detection through static file signature-based methods.

### **C Code Integration & Compilation**  
The encrypted and compressed EXE is embedded into C code. The code is then compiled using GCC to produce either a self-extracting EXE or DLL. This ensures that no remnants of the original EXE remain on disk.

---

## **Features**

### **Custom Compilation Framework**  
The generated DLLs and executables are structured with efficient code and optimized for various architectures. Each build undergoes rigorous testing to ensure compatibility and functionality across diverse runtime environments.

### **High-Performance Compression & Encryption**  
An innovative compression algorithm paired with dynamic encryption mechanisms ensures data integrity and confidentiality. These features work in tandem to reduce payload size while maintaining unparalleled security.

### **Sophisticated Code Obfuscation**  
The core compilation techniques ensure the generated binaries are resistant to reverse engineering and static analysis. This guarantees operational secrecy and secures the integrity of the execution flow.


---

## **Security Considerations**

### **Counteracting Reverse Engineering**  
XOR encryption is basic and not fully secure. The following measures are implemented to improve security:

- **Dynamic Key Generation:** Keys are managed in a way that prevents static analysis.
- **Multi-layer Encryption:** Multiple encryption methods are used to add layers of obfuscation, enhancing security.
- **Code Obfuscation:** Techniques are applied to obscure the code, making reverse engineering more difficult.

### **Advanced Encryption Techniques**  
AES-256 or RSA encryption is used for robust security, providing significantly stronger protection than XOR encryption.

---

## **Troubleshooting & FAQs**

### **Common Errors and Solutions**

- **Error: "GCC not found"**  
  Solution: Ensure that MinGW is installed and that the `bin` folder is included in your system’s PATH.

- **Error: "File not found"**  
  Solution: Double-check the paths to your EXE and output files to ensure they are correct.

- **Error: "Invalid EXE format"**  
  Solution: Verify that the EXE is properly compiled and compatible with the toolset.

---
## © StealthAgent.
 [![Author](https://img.shields.io/badge/Author-LOKI-green?style=flat-square&logo=github&logoColor=white)](https://github.com/lokihere0/)

---
