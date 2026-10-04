# Setting Up Linux on Windows and macOS

Now that we understand the basics of Linux, the next question is:

**How can we actually set up Linux on our computer?**

There are multiple ways to do this.

### Different Ways to Set Up Linux

1. **Dual Boot**
2. **Virtual Machines**
3. **WSL2**
4. **Docker Containers**
5. **Cloud Virtual Machines — AWS EC2**

In this video, we'll focus on the first two:

* **Dual Boot**
* **Virtual Machines**

And then we'll actually create an **Ubuntu Virtual Machine using Oracle VirtualBox**.

---

# 1. Dual Boot

The first approach is **Dual Booting**.

In a dual-boot setup, we install two operating systems on the same physical computer.

For example:

```plaintext
Physical Computer
       │
       ├── Windows
       │
       └── Linux / Ubuntu
```

Both operating systems are installed directly on the computer's storage.

When we turn on the computer, we can choose which operating system we want to boot.

For example:

```plaintext
Boot Menu

→ Ubuntu
  Windows Boot Manager
```

If we select Ubuntu, the computer boots directly into Linux.

If we select Windows, it boots directly into Windows.

### Advantages of Dual Boot

* Linux gets direct access to the physical hardware.
* Performance is close to running Linux natively.
* You can use the full CPU, RAM, GPU, and storage resources when booted into Linux.
* Useful when you need Linux as a primary operating system.

### Disadvantages of Dual Boot

* You need to partition your storage.
* Setting it up is more complicated than a VM.
* Switching between Windows and Linux usually requires restarting the computer.
* Incorrect partition or bootloader configuration can cause problems.

### When Should You Use Dual Boot?

Dual boot makes sense when you:

* Want to use Linux regularly as a full operating system.
* Need near-native Linux performance.
* Need direct access to hardware.
* Don't mind restarting the computer to switch operating systems.

But if you're just learning Linux and want to experiment without changing your existing system, there is another much easier approach:

**Virtual Machines.**

---

# 2. Virtual Machines

A **Virtual Machine**, or VM, is a software-based computer running inside your physical computer.

Instead of installing Linux directly on your hardware, we create a virtual computer and install Linux inside it.

For example:

```plaintext
Physical Computer
       ↓
Windows
       ↓
Virtualization Software
       ↓
Virtual Machine
       ↓
Ubuntu Linux
```

The VM gets virtualized resources such as:

* CPU
* RAM
* Storage
* Network interface

And inside that VM, we can install a complete Linux operating system.

---

# What Makes a VM Possible?

This is where the concept of a **Hypervisor** comes in.

## What Is a Hypervisor?

A **hypervisor** is software that creates and manages virtual machines.

It takes the physical resources of a computer and provides virtual resources to the VMs.

For example:

```plaintext
Physical Hardware
       ↓
    Hypervisor
       ↓
 ┌──────────────┐
 │ Linux VM     │
 └──────────────┘
```

The hypervisor manages things such as:

* CPU allocation
* Memory allocation
* Virtual disks
* Networking
* VM lifecycle

There are two major types of hypervisors.

---

# Type 1 Hypervisor — Bare Metal

A **Type 1 hypervisor** runs directly on the physical hardware.

There is no traditional host operating system sitting underneath it.

```plaintext
Hardware
    ↓
Type 1 Hypervisor
    ↓
 ┌────────┐  ┌────────┐
 │ VM 1   │  │ VM 2   │
 │ Linux  │  │Windows │
 └────────┘  └────────┘
```

### Examples

* VMware ESXi
* Microsoft Hyper-V
* Xen

### Why Use Type 1?

Type 1 hypervisors are commonly used where virtualization is the primary purpose of the machine.

For example:

* Data centers
* Enterprise servers
* Cloud infrastructure

They generally provide strong performance and efficient resource management.

---

# Type 2 Hypervisor — Hosted

A **Type 2 hypervisor** runs on top of an existing operating system.

For example:

```plaintext
Hardware
    ↓
Windows / macOS
    ↓
Type 2 Hypervisor
    ↓
Linux VM
```

Here, your normal operating system remains in control of the physical machine.

The hypervisor runs as software inside that operating system and creates VMs.

### Examples

* Oracle VirtualBox
* VMware Workstation
* VMware Fusion

---

# Why Are There Two Types?

The fundamental difference is **where the hypervisor sits in the stack**.

### Type 1

```plaintext
Hardware
   ↓
Hypervisor
   ↓
VMs
```

### Type 2

```plaintext
Hardware
   ↓
Host OS
   ↓
Hypervisor
   ↓
VMs
```

So the main trade-off is:

**Type 1 → better suited for dedicated virtualization and production infrastructure.**

**Type 2 → easier and more convenient for desktop users and developers.**

For example, if a company is running a virtualization server in a data center, using a Type 1 hypervisor makes sense.

But if you're sitting at home with Windows and want to learn Linux without replacing Windows, a Type 2 hypervisor is much more convenient.

---

# Type 1 vs Type 2

| Feature     | Type 1                       | Type 2                 |
| ----------- | ---------------------------- | ---------------------- |
| Also called | Bare Metal                   | Hosted                 |
| Runs on     | Hardware                     | Existing OS            |
| Performance | Generally higher             | Generally lower        |
| Common use  | Servers / Data Centers       | Desktops / Development |
| Example     | VMware ESXi                  | VirtualBox             |
| Setup       | More infrastructure-oriented | Easier for beginners   |

---

# What Are We Going to Use?

For this demonstration, we'll use:

**Oracle VirtualBox**

VirtualBox is a **Type 2 hypervisor**.

Why?

Because we're running it on our existing operating system.

For example:

```plaintext
My Physical Laptop
        ↓
      Windows
        ↓
   VirtualBox
        ↓
   Ubuntu VM
```

We don't need to replace Windows.

We don't need another physical computer.

We simply allocate a portion of our laptop's resources to the VM.

---

# Ubuntu VM Demo

Now let's actually create our Linux environment.

## Step 1 — Download VirtualBox

First, install Oracle VirtualBox on the host operating system.

Once it is installed, open VirtualBox.

### What to say while showing it:

> "So guys, instead of just understanding this theoretically, let's actually create our Linux machine. I'm going to use Oracle VirtualBox here. Remember, VirtualBox is a Type 2 hypervisor because it runs on top of my existing operating system."

---

# Step 2 — Download Ubuntu ISO

Next, download the Ubuntu ISO image.

The ISO is essentially the installation media that we'll use to install Ubuntu inside our VM.

### What to say:

> "Now we need the operating system that we want to install. In this case, I'm using Ubuntu. This ISO file contains the Ubuntu installation environment, similar to how we would use a bootable USB when installing an operating system on a physical computer."

---

# Step 3 — Create a New VM

Open VirtualBox and click **New**.

Give the VM a name such as:

```text
Ubuntu-Dev
```

Select the Ubuntu ISO file.

### What to say:

> "I'm creating a new virtual machine and I'll call it Ubuntu-Dev. I'm also selecting the Ubuntu ISO that I downloaded earlier. VirtualBox will use this ISO to install Ubuntu inside our virtual machine."

---

# Step 4 — Allocate Hardware

Now VirtualBox will ask us to configure resources.

We can allocate:

* RAM
* CPU
* Storage

For example:

```plaintext
RAM  → 4 GB
CPU  → 2 cores
Disk → 25–30 GB
```

The exact values depend on your physical machine.

### What to say:

> "Now we need to decide how much of our physical machine's resources we want to give to this VM. I'm allocating around 4 GB of RAM and 2 CPU cores. These resources aren't magically created — they are being taken from my physical laptop while the VM is running."

---

# Step 5 — Create the Virtual Disk

Create a virtual hard disk for the VM.

You can think of this as the VM's own storage.

```plaintext
Physical SSD
      ↓
Virtual Disk
      ↓
Ubuntu VM
```

### What to say:

> "Next, I'm creating a virtual disk. Think of this as the hard drive of our virtual computer. Ubuntu, applications, packages and our files will be stored inside this virtual disk."

---

# Step 6 — Start the VM

Now start the virtual machine.

VirtualBox will boot from the Ubuntu ISO.

You'll see the Ubuntu installation screen.

### What to say:

> "Now I'm starting the VM. Notice that I haven't rebooted my actual computer. VirtualBox is creating this virtual computer inside my existing operating system."

---

# Step 7 — Install Ubuntu

Follow the Ubuntu installation process.

Choose:

* Language
* Keyboard layout
* Installation options
* Username
* Password
* Disk configuration

Then start the installation.

### What to say:

> "At this point, we're basically installing Ubuntu just like we would install an operating system on a physical computer. The difference is that the computer we're installing it on is virtual."

---

# Step 8 — Ubuntu Is Ready

After installation, Ubuntu will boot inside the VM.

Now we have:

```plaintext
Physical Laptop
       ↓
Windows
       ↓
VirtualBox
       ↓
Ubuntu VM
       ↓
Ubuntu Linux
       ↓
Terminal
```

Open the terminal and run:

```bash
pwd
```

Then:

```bash
ls
```

And:

```bash
cat /etc/os-release
```

### What to say:

> "And that's it. We now have a complete Ubuntu Linux environment running inside our Windows machine. From here, we can open the terminal and start learning Linux commands."

---

# Important Things to Remember

A VM is a **complete virtual computer**.

It has its own:

* Operating system
* Kernel
* File system
* Processes
* Network configuration
* Virtual hardware

But the physical resources ultimately come from the host machine.

So if your laptop has:

```text
16 GB RAM
```

and you allocate:

```text
4 GB → Linux VM
```

that 4 GB is being used by the VM while it is running.

---

# Advantages of a VM

### Safe

You can experiment with Linux without replacing your main operating system.

### Isolated

The VM provides a separate environment for your Linux experiments.

### Easy to Experiment

You can install packages, modify configurations and practice system administration.

### Snapshots

VirtualBox supports snapshots, allowing you to save a VM's state and restore it later.

---

# Disadvantages of a VM

### Resource Consumption

The VM consumes CPU, RAM and storage from your physical machine.

### Performance Overhead

There can be some performance overhead compared with running Linux directly on hardware.

### Storage

The VM requires disk space for the operating system, applications and data.

### Host Dependency

If your host machine is shut down, the VM also stops.

---

# Dual Boot vs Virtual Machine

|                               | Dual Boot            | Virtual Machine           |
| ----------------------------- | -------------------- | ------------------------- |
| Linux installation            | Directly on hardware | Inside virtual machine    |
| Performance                   | Near native          | Some overhead             |
| Restart required to switch OS | Yes                  | No                        |
| Hardware access               | Direct               | Virtualized               |
| Resource sharing              | One OS at a time     | Host + VM share resources |
| Beginner friendly             | Moderate             | Easier                    |
| Experimentation               | Less convenient      | Very convenient           |

### Simple Rule

If you want **maximum native performance and Linux as a primary OS**, consider **Dual Boot**.

If you want to **learn Linux while keeping Windows/macOS and without restarting every time**, a **Virtual Machine** is usually more convenient.

---

# What's Next?

So now we know the different ways we can set up Linux, we've understood **Dual Boot**, we've learned what a **Virtual Machine** is, and we've understood the two types of hypervisors.

We've also created our own **Ubuntu VM using Oracle VirtualBox**.

In the next video, we'll look at the other approaches:

* **WSL2**
* **Docker**
* **AWS EC2**

and understand when each one makes sense for a DevOps engineer.


