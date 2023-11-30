# Linux Boot Process

## Step 1: Power On, BIOS/UEFI Initialization, and POST

### 1.1. Power On:
   - When you turn on the computer, the power supply sends electricity to the components.
   - This initiates the boot process.

### 1.2. BIOS/UEFI Initialization:
   - The Basic Input/Output System (BIOS) or Unified Extensible Firmware Interface (UEFI) is a firmware stored in non-volatile memory (e.g., ROM or flash memory).
   - BIOS/UEFI initializes critical hardware components to ensure they are in a usable state.

### 1.3. Power On Self Test (POST):
   - POST is a diagnostic process conducted by the BIOS/UEFI during the initial startup.
   - It checks the functionality of various hardware components to ensure they are working correctly.

> Example Scenarios During POST:
   - **Memory Check:** The BIOS/UEFI verifies the integrity of the system's RAM by writing and reading test patterns.
   - **CPU Check:** The processor registers, arithmetic logic unit (ALU), and control unit are tested.
   - **Peripheral Check:** Connected peripherals such as keyboard, mouse, and storage devices are checked.
   - **BIOS/UEFI Firmware Check:** The BIOS/UEFI itself is verified for integrity.
   - **Graphics Card Check:** If a separate graphics card is present, it undergoes a self-check.
   - **Initialization of System Timer:** The system timer, crucial for various time-related functions, is initialized.

### Example Error Indications During POST:
   - **Beep Codes:** Some motherboards emit a series of beeps during POST to indicate errors. For example, a single beep may indicate a successful POST, while a series of beeps may indicate a hardware issue.
   - **LED Indicators:** Some systems have LEDs that indicate the status of various components. For instance, a red LED might indicate a failed POST.

### Outcome of POST:
   - If POST completes without critical errors, the BIOS/UEFI proceeds to the next step in the boot process.
   - If there are errors, the BIOS/UEFI may halt the boot process, display an error message, or use other means to communicate the issue.

---

## Step 2: Hardware Detection Process during BIOS/UEFI Initialization:

### 2.1. **Power-On and Initialization:**
   - When the computer is powered on, the BIOS/UEFI firmware is executed.
   - BIOS/UEFI initializes key components to prepare the system for booting.

### 2.2. **CPU Detection and Initialization:**
   - The BIOS/UEFI identifies the CPU (Central Processing Unit).
   - It initializes the CPU, including setting the instruction pointer and configuring registers.

### 2.3. **Memory Detection and Initialization:**
   - The BIOS/UEFI detects and initializes RAM (Random Access Memory).
   - A portion of the system's memory may be reserved for system use.
   - Example: If a system has 8 GB of RAM, the BIOS/UEFI ensures that this memory is functional and available for use.

### 2.4. **Storage Device Detection:**
   - BIOS/UEFI identifies and initializes storage devices such as hard drives and SSDs.
   - It may perform a brief check on connected storage to determine if they are accessible.
   - Example: Detecting a SATA SSD and preparing it for use as a boot device.

### 2.5. **Peripheral Devices Detection:**
   - Connected peripherals like keyboards, mice, and USB devices are detected.
   - BIOS/UEFI ensures these devices are ready for use.
   - Example: Ensuring that a USB keyboard is responsive.

### 2.6. **System Timer Initialization:**
   - The BIOS/UEFI initializes the system timer.
   - The system timer is crucial for various time-related functions.
   - Example: Initializing the timer to maintain accurate timekeeping.

### 2.7. **Interrupt Controllers Setup:**
   - The BIOS/UEFI sets up interrupt controllers to handle hardware interrupts.
   - Interrupt controllers are essential for managing hardware events.
   - Example: Configuring the interrupt controllers to handle keyboard input.

### 2.8. **System Memory Map Creation:**
   - BIOS/UEFI creates a memory map, detailing how memory is allocated and used.
   - It establishes regions for the operating system, reserved areas, and peripherals.
   - Example: Allocating specific memory ranges for system processes and device access.

### 2.9. **Display Initialization:**
   - Graphics adapters are initialized to provide basic display capabilities.
   - Example: Preparing the graphics card to display system information during the boot process.

---

## Step 3: Choosing Boot Device

### 3.1. **BIOS/UEFI Settings:**
   - Users can configure the boot order in the BIOS/UEFI settings.
   - The boot order defines the sequence in which devices are checked for a bootable operating system.
   - Example: In the BIOS settings, a user sets the primary boot device as the hard drive and the secondary boot device as a USB flash drive.

### 3.2. **Power-On Self-Test (POST):**
   - After initializing hardware, the system performs a Power-On Self-Test.
   - The BIOS/UEFI checks devices in the configured boot order for bootable information.
   - Example: The POST process detects a USB flash drive and a hard drive during the boot order check.

### 3.3. **Device Detection:**
   - The BIOS/UEFI identifies and detects connected devices based on the boot order.
   - It looks for a Master Boot Record (MBR) or EFI System Partition (ESP) to determine bootability.
   - Example: Detecting a bootable USB drive with an MBR or an ESP.

### 3.4. **Bootable Media Detection:**
   - The BIOS/UEFI checks for bootable media on the identified devices.
   - Bootable media contains the necessary bootloader to initiate the OS.
   - Example: Verifying that the USB drive has a valid bootloader or checking for an OS partition on the hard drive.

### 3.5. **User Intervention:**
   - If multiple bootable devices are found, or the user wishes to override the default boot order, they may intervene.
   - Users can access the boot menu during the initial startup phase.
   - Example: Pressing a designated key (e.g., F12) to open the boot menu and manually selecting the desired boot device.

### 3.6. **Boot Loader Execution:**
   - The selected boot device's bootloader is executed.
   - The bootloader loads the initial part of the operating system into memory.
   - Example: GRUB (Grand Unified Bootloader) is a common bootloader for systems using BIOS. It loads the Linux kernel.

### 3.7. **Handoff to Operating System:**
   - The bootloader hands control over to the operating system.
   - The OS kernel takes charge and continues the boot process.
   - Example: The Linux kernel initializes the system, mounts filesystems, and starts user-space processes.

**Note:**
> The Choosing Boot Device process enables users to define the priority of bootable devices, allowing flexibility in the system's startup behavior. Examples highlight scenarios such as USB drives, hard drives, and user interventions in selecting the boot device.


---

## Step 4: Boot Loader Execution (GRUB)

### 4.1. **GRUB Installation:**
   - GRUB is installed in the Master Boot Record (MBR) or the EFI System Partition (ESP) of the storage device.
   - Example: After installing a Linux distribution, GRUB is commonly placed in the MBR or the ESP.

### 4.2. **Menu Presentation:**
   - Upon system startup, GRUB presents a menu to the user.
   - The menu lists available operating systems and kernels.
   - Example: A typical GRUB menu might display options like "Ubuntu," "Advanced options for Ubuntu," and "Memory test."

### 4.3. **User Selection:**
   - The user selects an entry from the GRUB menu.
   - Selection can include different OS versions or recovery modes.
   - Example: The user chooses "Ubuntu" from the menu.

### 4.4. **Loading Configuration:**
   - GRUB reads its configuration file (usually located in /boot/grub/grub.cfg) to determine how to boot the selected entry.
   - The configuration file includes kernel paths, initial RAM disk (initrd) information, and boot parameters.
   - Example: The GRUB configuration file specifies the path to the Linux kernel and its associated initrd.

### 4.5. **Kernel Loading:**
   - GRUB loads the selected Linux kernel into memory.
   - The kernel is the core of the operating system responsible for managing hardware and launching user processes.
   - Example: Loading the Linux kernel, such as vmlinuz-5.4.0-1042-azure.

### 4.6. **Initrd Initialization:**
   - If specified in the configuration, GRUB loads the initial RAM disk (initrd).
   - The initrd contains essential drivers and modules needed to mount the root filesystem.
   - Example: Loading an initrd file like initrd.img-5.4.0-1042-azure.

### 4.7. **Control Handover to Kernel:**
   - GRUB hands control over to the loaded kernel with specified boot parameters.
   - The kernel continues the boot process, initializing devices, mounting filesystems, and launching user-space processes.
   - Example: The Linux kernel receives control and begins executing the kernel code.

**Note:**
> GRUB serves as a flexible and user-friendly bootloader, allowing users to choose the OS or kernel to boot. It reads its configuration, loads the selected kernel and initrd, and facilitates the transition to the operating system. Examples illustrate the GRUB menu, user selection, and key steps in the loading process.

---

## Step 5: Kernel Initialization

### 5.1. **Kernel Loading:**
   - Once the bootloader (e.g., GRUB) hands over control, the kernel is loaded into memory.
   - The kernel is often stored in the /boot directory and is specified in the bootloader's configuration.
   - Example: Loading the Linux kernel, vmlinuz-5.4.0-1042-azure.

### 5.2. **Initrd Initialization (if used):**
   - If an initial RAM disk (initrd) is specified in the bootloader configuration, the kernel loads it into memory.
   - The initrd is a temporary root filesystem that contains essential modules and drivers needed to mount the actual root filesystem.
   - Example: Loading an initrd file like initrd.img-5.4.0-1042-azure.

### 5.3. **Kernel Initialization:**
   - The kernel initializes itself, setting up the essential data structures and configuring various parameters.
   - It identifies and initializes hardware components, such as the CPU, memory, and peripherals.
   - Example: The kernel initializes CPU registers, sets up interrupt handling, and initializes memory management.

### 5.4. **Root Filesystem Mounting:**
   - The kernel mounts the root filesystem, which contains the core operating system files.
   - The root filesystem is specified as a kernel parameter or is determined by the initrd.
   - Example: Mounting the root filesystem located on a partition like /dev/sda1.

### 5.5. **Init Process Launch:**
   - The kernel launches the init process as the first user-space process.
   - The init process is responsible for initializing the user space, starting system services, and transitioning to the default runlevel or target.
   - Example: Executing /sbin/init.

### 5.6. **Switch to User Space:**
   - The kernel switches control to user space, allowing user-level processes to start.
   - Initiated by executing the /sbin/init process.
   - Example: The system transitions to user space, and the init process becomes the first user space process.

**Note:**
> Kernel initialization involves loading the kernel into memory, initializing hardware, mounting the root filesystem, and launching the init process.Examples illustrate key steps such as loading the Linux kernel and initializing the initrd if used. The process sets the stage for the operating system to become fully operational.
   
---

## Step 6: User Space Initiation

### 6.1. **Systemd Activation:**
   - After launching the init process, the kernel activates systemd as the first user-space process.
   - Systemd is a system and service manager that plays a crucial role in managing processes, services, and other aspects of the system.
   - Example: Activating systemd as the primary init system.

### 6.2. **Hardware Probing:**
   - Systemd probes the remaining hardware components that may not have been initialized during the kernel phase.
   - It identifies and configures devices, ensuring the system has access to all necessary hardware resources.
   - Example: Detecting and configuring hardware devices like USB controllers or additional storage devices.

### 6.3. **Filesystem Mounting:**
   - Systemd mounts additional filesystems beyond the root filesystem, such as /proc, /sys, and others required for proper system operation.
   - These filesystems provide interfaces to kernel and system information.
   - Example: Mounting /proc and /sys virtual filesystems.

### 6.4. **Target Activation:**
   - Systemd activates the default target unit, defining the system state. Targets are similar to runlevels in traditional init systems.
   - The default target specifies which services and processes should run at startup.
   - Example: Activating the graphical.target, which is often the default target for systems with a graphical user interface.

### 6.5. **Startup Scripts and Configuration:**
   - Systemd executes startup scripts, also known as units, to configure the environment.
   - These units define services, sockets, devices, and other system components.
   - Example: Running service units like network.service to start networking services.

### 6.6. **Login Window Presentation:**
   - As part of the user space initiation, a login window or display manager may be presented to users.
   - This allows users to log in and start graphical sessions if applicable.
   - Example: Presenting a login screen for user authentication.

**Note:**
> User space initiation involves the activation of systemd, probing hardware, mounting additional filesystems, activating target units, and executing startup scripts. Examples illustrate key steps such as mounting virtual filesystems and activating the default target. This phase prepares the system for user interaction and the execution of user applications and services.


---

## Step 7: Activation of Default Target Unit

### 7.1. **Definition of Target Units:**
   - In systemd, a target unit is a representation of a specific system state or a set of tasks.
   - Targets group services and other units, defining the system's behavior in a given state.
   - Example: The graphical.target unit, which signifies a state with a graphical user interface.

### 7.2. **Default Target:**
   - The default target unit is the one activated during the startup process by systemd.
   - It defines the initial state of the system, including essential services and processes.
   - Example: The default target might be multi-user.target for a server or graphical.target for a desktop environment.

### 7.3. **Activation Process:**
   - During the startup, systemd activates the default target unit based on the configuration.
   - The default target guides which services and processes are started at boot.
   - Example: Activating multi-user.target to initialize a system without a graphical interface.

### 7.4. **Dependencies and Ordering:**
   - Target units can have dependencies on each other, and systemd ensures that units are started in the correct order.
   - Dependencies define the sequence in which units are activated.
   - Example: If graphical.target depends on networking.service, the network service starts before the graphical environment.

### 7.5. **Service Activation:**
   - The default target typically includes services relevant to the chosen system state.
   - Services are individual units responsible for specific tasks or processes.
   - Example: Activating services like networking.service or display-manager.service as part of the default target.

### 7.6. **Outcome:**
   - Activation of the default target unit sets the stage for the system's primary mode of operation.
   - The default target defines the system's behavior and initializes essential services.
   - Example: If the default target is graphical.target, the system launches into a state where graphical user interface services are active.

**Example:**
Suppose the default target is set to graphical.target:

```bash
# Set the default target to graphical.target
sudo systemctl set-default graphical.target
```

**Note**
> During startup, systemd activates the graphical.target, initializing services necessary for a graphical user interface. This might include services for display management, windowing system, and other graphical components.

---

## Step 8: Startup Scripts and Login

### 8.1. **Startup Scripts Execution:**
   - After the default target unit is activated, startup scripts and configuration files are executed.
   - Startup scripts set up the environment, configure system settings, and launch essential services.
   - Example: Running shell scripts in `/etc/init.d` or executing systemd service units.

### 8.2. **Environment Setup:**
   - System-wide and user-specific environment configurations are applied.
   - Settings related to paths, variables, and system parameters are initialized.
   - Example: Loading global environment variables from `/etc/environment`.

### 8.3. **Networking Initialization:**
   - Networking services are initialized to establish network connectivity.
   - Configuration files and scripts related to networking are processed.
   - Example: Executing scripts in `/etc/network/if-up.d` to configure network interfaces.

### 8.4. **Service Launch:**
   - Essential services and daemons required for system operation are started.
   - This includes background services, system monitors, and other critical processes.
   - Example: Starting the systemd-logind service for user session management.

### 8.5. **User Login Prompt:**
   - Once the system is configured and essential services are running, the system presents a login window.
   - Users can log in, initiating their individual sessions.
   - Example: Displaying a graphical login screen or a text-based login prompt.

### 8.6. **Login Process:**
   - After entering valid credentials, the user's shell is launched, and the user gains access to the system.
   - User-specific startup scripts, such as `.bashrc` or `.profile`, are executed.
   - Example: Running a user's specified login commands and initializing their environment.

### 8.7. **User Session Initialization:**
   - User-specific settings and services are initialized based on the user's profile.
   - Desktop environments, session managers, and user-specific daemons are started.
   - Example: Launching the user's chosen desktop environment, such as GNOME or KDE.

### 8.8. **System Ready for Interaction:**
   - Once the user login process is complete, the system is fully operational and ready for user interaction.
   - Users can interact with the desktop environment or command-line interface.
   - Example: The user sees a graphical desktop or a command prompt, depending on the system setup.

**Example:**
```bash
# Execute startup script
/etc/init.d/my_startup_script.sh

# Launch a systemd service unit
sudo systemctl start my_service.service

# Display login prompt
login:
```

**Note:**
> During this process, system-wide and user-specific configurations are applied, essential services are started, and the system becomes accessible for user interaction.

---

> #### This entire process ensures that the system transitions from a powered-off state to a fully initialized and user-ready state. Each step is crucial for the proper functioning of the operating system.
