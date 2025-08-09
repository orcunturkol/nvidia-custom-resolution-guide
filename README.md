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

### Step 2: Create the Resolution Value

1.  Stay inside that correct `0000` folder.
2.  In the empty white space on the right panel, right-click and go to **`New` -> `Multi-String Value`**.
3.  Name this new value exactly **`NV_Modes`** and press Enter.

### Step 3: Add Your Custom Resolution

Double-click your new `NV_Modes` value to open the editor box. Here, you will type the resolution you want to add. There are two common formats.

**Format A: For adding a single resolution from scratch.**

* **Template:**
    `{*}S [Width] [Height] [Width] [Height] 32 [RefreshRate]`

* **Example (for 3840x1440 @ 240Hz):**
    `{*}S 3840 1440 3840 1440 32 240`

**Format B: For adding to an existing list of resolutions.**

* **Template:**
    `[Width]x[Height]x32,[RefreshRate]`

* **Example (for 3840x1440 @ 240Hz):**
    `3840x1440x32,240`

Copy the template, replace the `[bracketed]` parts with your desired numbers, and paste it into the text box.

### Step 4: Restart Your Computer

This is the final and most important step. Close the Registry Editor and **restart your PC**. The new resolution will not appear until you have rebooted.

---

### Troubleshooting

* **Problem:** I get a warning that says "Data of type REG_MULTI_SZ cannot contain empty strings."
* **Solution:** This just means you accidentally pasted a blank line. Click **OK** on the warning. Then, double-check the text box and delete any empty lines, especially at the very end of the text.
