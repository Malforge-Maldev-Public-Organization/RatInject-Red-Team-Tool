# RatInject - Red Team Tool

## Introduction

Welcome to this article! Today, I’m introducing my new C++ tool — RatInject.

Repository Link:

> GitHub - S12cybersecurity/RatInject: Rat Inject is C++ Executable to gain Undetectable Persistence\
Rat Inject is C++ Executable to gain Undetectable Persistence in Windows via 4 Registry Keys This tool gains. [github.com](https://github.com/S12cybersecurity/RatInject)

---

**What is RatInject?**

RatInject is a modular C++ tool designed to achieve persistence on Windows systems while remaining invisible to the average user.
To achieve persistence, it offers four different methods — you can use any one individually or combine them as needed.

The four persistence methods used by RatInject are :
- Runkeys
- WinLogon
- Image File Execution Options (Open)
- Image File Execution Options (Close)

We’ll dive deeper into how each method works shortly, but for now, let’s keep things general and focus on the overall approach.\
These four methods work by modifying or adding specific keys and values in the Windows registry to achieve persistence.

**What is Windows Register?**

the Windows Registry is a hierarchical database essential for the operating system and applications. It organizes configuration data in a tree structure, **where each node is called a 'key'** that can contain subkeys and associated data entries known as **'values'**.

**How it Works?**

By modifying specific Windows registry keys, we can configure an executable to run automatically at various stages of system activity.

- **Runkey:**

  The Run registry key is one of the most important on a Windows system. It is executed multiple times during system operation, particularly at startup.

- **WinLong:**

  Winlogon is a critical Windows component responsible for handling user authentication events such as logon, logoff, profile loading, shutdown, and the lock screen. By modifying its registry keys, an executable    can be triggered during these events.

- **Image File Execution Options (Open):**

  This method allows you to execute your binary whenever a specific process or application is launched. For example, you can configure it to run your executable when the user opens the `calc.exe` process.
  
- **Image File Execution Options (Close):**
  
  This method enables you to execute your binary when a specific process is closed. For example, you can set it to run your executable when the user ends the `explorer.exe` process.

**Compile**

To compile this on a Linux machine, execute the following command:

```bash
x86_64-w64-mingw32-g++ persistence.cpp -o ratinject.exe -static-libstdc++ -static-libgcc -fpermissive
```

![image](https://github.com/user-attachments/assets/c7ef5a05-c01b-4b6a-bbca-ce15250ad87e)

## Proof of Concept (PoC)

In this section, we’ll cover the most important part: how to use this tool.

## All:

To enable all four persistence options, run the following command: 

```cmd
ratinject.exe evil.exe All
```

![image](https://github.com/user-attachments/assets/d31dcfc8-274e-45cd-b69f-3e290495aed2)

Now, your malicious executable is set to run at four critical moments: when the user logs in, logs out, switches users, and more — all through Winlogon.

Additionally, your executable will run when the user opens the `calc.exe` process (the Calculator) using the Image Options Executor.

Your executable will also run when the user closes the `explorer.exe` process (File Explorer) using the Image Options Executor.

Additionally, your executable will run when the machine starts, using the RunKey method.

### Mix :

You don’t need to execute all options at once — you have the flexibility to choose. For more details, you can refer to the help menu, which provides more information:

![image](https://github.com/user-attachments/assets/657d5faa-57e8-4259-ae48-34bb5f113be1)

Recommended execution:

```cmd
ratinject.exe evil.exe Open Run Close
```

Using Winlogon for persistence may cause instability or bugs in the operating system.

### Individual:

Logically, you should execute only one persistence method at a time to avoid conflicts or instability :

![image](https://github.com/user-attachments/assets/61a95027-519f-4317-bf5d-beda50a910ed)

## Conclusions

That’s all for today’s article! I hope you found it useful and enjoyed learning how to use the tool effectively.

Thanks for reading! :B

**- Malforge Group**
