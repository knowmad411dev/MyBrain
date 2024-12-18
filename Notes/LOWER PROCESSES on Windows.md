---
tags:
- windows
---
## **LOWER PROCESSES on Windows

## **How to Reduce System Process Count and Boost Performance**

This guide provides several methods to reduce your system's process count, lower resource usage, and potentially improve FPS in games or general system performance.

---

### **1. Understanding Task Manager Processes**

1. Open **Task Manager** (Ctrl + Shift + Esc).
2. Go to the **Performance** tab.
    - At the bottom, you'll see the number of processes running.
    - High process counts can be alarming but often represent grouped processes.

---

### **2. SVC Split Threshold Registry Tweak**

This tweak groups processes together but does not physically reduce them. The benefits are often minimal and can introduce issues.

**Steps:**

1. Press `Win + R` to open the Run box.
2. Type `regedit` and press Enter to open the **Registry Editor**.
3. Navigate to the following path:
    
    ```
    HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control
    ```
    
4. Locate the file **SVCSplitThresholdInKB**.
5. Change the default value to match your installed RAM (in KB).
    - Example: For **64 GB RAM**, set it to `65536` KB.

**Note:**

- Check RAM in Task Manager: **Performance > Memory**.
- Restart your PC to apply the change.
- **Recommendation:** This tweak has little to no real-world benefit. Create a restore point or revert if issues occur.

---

### **3. Reducing System Tray Applications**

Minimizing startup applications reduces processes and boosts system performance.

#### **Method 1: Taskbar System Tray**

1. Click on the **system tray** (bottom-right corner).
2. Close unnecessary applications running in the background.

#### **Method 2: Startup Apps**

1. Open **Settings** > **Apps** > **Startup**.
2. Sort by **Startup Impact**.
3. Disable apps you don’t use daily (e.g., OneDrive, Microsoft Edge).
4. Example:
    - **Disable:** Riot Games, Microsoft Bing, Vanguard.
    - **Keep Enabled:** Applications you use frequently like Epic Games Launcher.

#### **Alternative: Task Manager**

1. Open **Task Manager**.
2. Go to **Startup Apps**.
3. Sort by **Startup Impact** and disable unnecessary apps.

---

### **4. Disabling Background Apps in Windows 11**

Prevent unused apps from running in the background to save resources.

**Steps:**

1. Go to **Settings** > **Apps** > **Installed Apps**.
2. Find an app you don’t want running in the background.
3. Click on the three dots (**...**) > **Advanced Options**.
4. Under **Background Apps Permissions**, select **Never**.
5. Example: Disable apps like **Maps**, **Quana**, or others you rarely use.

**Optional:** Uninstall unwanted apps instead of disabling them.

---

### **5. Disabling Useless Services**

Services can run in the background unnecessarily. Disabling unused ones reduces process count.

**Steps:**

1. Press `Win + R`, type `services.msc`, and press Enter.
2. Review services and disable those you don’t use.
3. Right-click the service > **Properties**.
    - Change **Startup Type** to **Disabled**.

**Examples of Services to Disable:**

- **Connected User Experiences and Telemetry**: Sends diagnostic data to Microsoft.
- **Downloaded Maps Manager**: For offline maps.
- **Print Spooler**: Disable if you don’t use a printer.
- **Windows Biometric Service**: For fingerprint scanners (disable on desktops).
- **Windows Insider Service**: If you’re not part of the Windows Insider program.

**Important:**

- **Research** each service before disabling.
- Example: Disabling Bluetooth services can break Bluetooth devices.

---

### **6. Adjust Windows Visual Effects for Performance**

Reduce Windows animations and effects to lower resource usage.

**Steps:**

1. Open the Run box (`Win + R`).
2. Type:
    
    ```
    systempropertiesperformance.exe
    ```
    
3. In the **Performance Options** window, select **Adjust for best performance**.
4. Re-enable basic functionalities for usability:
    - **Animations in the taskbar**
    - **Save taskbar thumbnail previews**
    - **Show thumbnails instead of icons**
    - **Show window contents while dragging**
    - **Smooth edges of screen fonts**
5. Click **Apply** > **OK**.

---

### **Summary Checklist**

- **Task Manager:** Reduce tray and startup apps.
- **Registry Tweak:** Avoid or test carefully.
- **Background Apps:** Set unwanted apps to “Never”.
- **Services:** Disable unnecessary services (research first).
- **Visual Effects:** Adjust for performance.

---

By following these steps, you can effectively reduce your system’s process count, boost overall performance, and potentially improve FPS in games. Always create restore points before making significant changes.

[[Windows]]