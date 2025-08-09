# How to Add a Custom Resolution for NVIDIA GPUs (Registry Method)

This guide explains how to manually add a custom screen resolution for your NVIDIA graphics card by editing the Windows Registry.

**⚠️ Warning:** Editing the registry can be risky. Always be careful and follow the steps exactly. It's a good idea to back up your registry before you begin. (In the Registry Editor, go to `File` > `Export` to save a backup).

---

### Step 1: Find Your NVIDIA Folder in the Registry

1.  Open the Start Menu, type **`regedit`**, and press Enter to open the Registry Editor.
2.  In the address bar at the top of the Registry Editor, copy and paste the following path and press Enter:
    `HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\Video\`
3.  You will see several folders with long names like `{A1547018...}`. You need to find the one for your NVIDIA card.
4.  Click on the first folder, then click on the `0000` subfolder. Look at the list of items on the right for one named **`DriverDesc`**.
5.  Check the "Data" column. If it doesn't say "NVIDIA...", move to the next folder with a long name and check its `0000` subfolder.
6.  Repeat this until you find the folder where `DriverDesc` shows your **"NVIDIA GeForce..."** graphics card. This is the correct folder.


---

### Step 2: Edit or Create the Resolution Value

1.  Stay inside that correct `0000` folder.
2.  Look for an existing value named **`NV_Modes`**.
    * **If it already exists**, double-click it to edit.
    * **If it does NOT exist**, right-click in the empty white space on the right panel, go to **`New` -> `Multi-String Value`**, and name it exactly **`NV_Modes`**.
<img width="333" height="205" alt="image" src="https://github.com/user-attachments/assets/003e713c-aac8-4b8f-a9e9-616f7892c283" />
<img width="540" height="191" alt="image" src="https://github.com/user-attachments/assets/de23f4e9-5374-4ece-863c-e7fe59953999" />

---

### Step 3: Add Your Custom Resolution

Double-click your `NV_Modes` value to open the editor box. **Delete any text already inside** and replace it with the resolution(s) you want.

<img width="341" height="310" alt="image" src="https://github.com/user-attachments/assets/e8ff68ce-dec9-4315-983e-e6d47b160f81" />

**Format A: For adding a single resolution from scratch.**

* **Template:**
    `{*}S [Width] [Height] [Width] [Height] 32 [RefreshRate]`

* **Example (for 3840x1440 @ 240Hz):**
    `{*}S 3840 1440 3840 1440 32 240`
<img width="347" height="311" alt="image" src="https://github.com/user-attachments/assets/36bac91b-605b-47ca-b758-4ccda73b5ea6" />

**Format B: For creating a list of resolutions.**

* **Template:**
    `[Width]x[Height]x32,[RefreshRate]`

* **Example (for 3840x1440 @ 240Hz):**
    `{*}S 640x480x32,64 720x480x32,64 800x600x32,64 1024x768x32,64 1152x864x32,64 1280x720x32,64 1280x768x32,64 1280x800x32,64 1280x960x32,64 1280x1024x32,64 1360x768x32,64 1366x768x32,64 1440x1080x32,64 1600x900x32,64 1600x1024x32,64 1600x1200x32,64 1680x1050x32,64 1920x1080x32,64 1920x1200x32,64 1920x1440x32,64 2048x1536x32,64 2560x1440x32,64 2560x1600x32,64 3840x1440x32,240=1; 720x576x32,64=8032;
`
<img width="345" height="313" alt="image" src="https://github.com/user-attachments/assets/e5bef724-13fb-4f75-a39c-d2381ee1c72c" />

---

### Step 4: Restart Your Computer

This is the final and most important step. Close the Registry Editor and **restart your PC**. The new resolution will not appear until you have rebooted.

---

### Troubleshooting

* **Problem:** I get a warning that says "Data of type REG_MULTI_SZ cannot contain empty strings."
    * **Solution:** This just means you accidentally pasted a blank line. Click **OK** on the warning. Then, double-check the text box and delete any empty lines, especially at the very end of the text.

* **Problem:** The `NV_Modes` key already existed. What about the `0001`, `0002` folders?
    * **Solution:** That's perfectly normal. If `NV_Modes` already exists, your action was correct: you should edit it and replace its contents. The other folders (`0001`, `0002`, etc.) represent different connection states or profiles. While changing the `0000` folder is usually enough, changing it in the other folders as well is a good "just in case" step and does no harm.
