# 📱 Android App Development Setup for Open edX

This guide walks you through setting up Android Studio and configuring a local development environment for running the Open edX Android app.

---

## 🧰 Install Android Studio

### Step 1: Download and Install

1. Visit the [official Android Studio website](https://developer.android.com/studio).

2. Download the appropriate installer for your OS:

   * **Windows**: `.exe` installer
   * **macOS**: `.dmg` package
   * **Linux**: `.tar.gz` archive

3. Install Android Studio:

   * On **Windows/macOS**: run the installer.
   * On **Linux**:

     ```bash
     tar -xzf android-studio-*.tar.gz
     sudo mv android-studio /opt/
     cd /opt/android-studio/bin
     ./studio.sh
     ```

4. Follow the **Setup Wizard** to install required SDK components.

---

### ✅ Optional (Linux-only): Install Required Libraries

If you're on **Linux (64-bit)**, install the following libraries:

```bash
sudo apt-get install libc6:i386 libncurses5:i386 libstdc++6:i386 lib32z1 libbz2-1.0:i386
```

---

## ⚙️ Enable Emulator Acceleration (All Platforms)

To improve Android emulator performance, enable hardware virtualization using **Intel HAXM** (macOS/Windows) or **KVM** (Linux).

### Step 1: Check Virtualization Support

1. Reboot and enter BIOS/UEFI (press `DEL`, `F2`, or `Esc` during boot).
2. Enable the virtualization setting:

   * **Intel CPUs**: `Intel VT-x`
   * **AMD CPUs**: `AMD-V` or `SVM`

> 💡 Save changes (usually `F10`) and reboot.

### Step 2: OS-Specific Acceleration Setup

#### 🔵 Windows/macOS

* Use the Android Studio SDK Manager to install:

  * **Intel HAXM** (for Intel CPUs)
  * Or enable **hardware acceleration for ARM images**

> Android Studio will prompt you if HAXM isn't available during setup.

#### 🟢 Linux

1. Check if KVM is supported:

   ```bash
   sudo apt-get install cpu-checker
   sudo kvm-ok
   ```

   Expected output:

   ```
   INFO: /dev/kvm exists
   KVM acceleration can be used
   ```

2. Install KVM dependencies:

   ```bash
   sudo apt-get install qemu-kvm libvirt-daemon-system libvirt-clients bridge-utils
   ```

---

# 🧪 Local Development Setup for Open edX Android App

> **⚠️ Important Note:**
> The following configurations are intended _only_ for local development. Some of these are **temporary workarounds** to get the app running on an Android emulator and are **not suitable for production use**.
> Feel free to explore and implement more robust or cleaner solutions as needed.


---

## Step 1: Configure Development Settings

Open the project in **Android Studio** and update the development configuration file:

`default_config/dev/config.yaml`

Update the following keys with the appropriate values:

`API_HOST_URL:  'http://10.0.2.2:8000' `

` OAUTH_CLIENT_ID:  '<your-oauth-client-id>'`


### Why use `10.0.2.2`?

When running the app in an Android emulator, it cannot resolve `local.openedx.io` because that domain points to your local machine, which is _outside_ the emulator's network.

As a workaround, `10.0.2.2` acts as a special alias that allows the emulator to access the host machine’s localhost (`127.0.0.1`).

---

## Step 2: Allow Cleartext Traffic

### 1. Modify `AndroidManifest.xml`

Add the following line inside the `<application>` tag in:

`app/src/main/AndroidManifest.xml`

`android:networkSecurityConfig="@xml/network_security_config"`

### 2. Create Network Security Config File

Create the following XML file at:

`app/src/main/res/xml/network_security_config.xml`

    <?xml version="1.0" encoding="utf-8"?>
    <network-security-config>
       <domain-config cleartextTrafficPermitted="true">
           <domain includeSubdomains="true">10.0.2.2</domain>
           <domain includeSubdomains="true">192.168.1.6</domain>
       </domain-config>
    </network-security-config>


> This configuration allows HTTP (cleartext) traffic to `10.0.2.2`, which is necessary for local development if your server does not support HTTPS.

---

## ✅ You’re All Set!

You should now be able to build and run the Open edX Android app locally using your development server.

---

## Reminder

> ⚠️ **These changes are strictly for local development purposes only.**
> Do **not** commit or push these configurations to version control.
> They include development-only settings such as insecure network access
> (`cleartextTrafficPermitted`) and hardcoded localhost URLs
> (`10.0.2.2`) which are **not safe** or suitable for production
> environments.   Always use secure, environment-specific configurations
> for production builds.


