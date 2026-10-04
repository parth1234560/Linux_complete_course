# 1. Before Virtual Machines: What Is a Server?

Before we understand virtual machines, let's understand **servers**.

A server is a computer whose job is to provide a service, resource, or
data to other computers over a network.

The computer requesting something is generally called a **client**, and
the computer providing the service is the **server**.

### Simple Example

Suppose you open YouTube on your laptop.

``` text
Your Laptop
    |
    |  Request: "Give me this video"
    v
YouTube Server
    |
    |  Response: Video data
    v
Your Laptop
```

Your laptop is acting as the **client**.

The server receives the request, processes it, and sends the required
response back.

------------------------------------------------------------------------

# 2. Is a Server a Special Kind of Computer?

Not necessarily.

A server can be a powerful physical computer, but technically the word
**server** describes a role.

For example:

-   Your laptop can act as a server.
-   A physical machine in a data center can act as a server.
-   A virtual machine can act as a server.
-   A cloud instance such as an AWS EC2 instance can act as a server.

The important thing is **what the computer is doing**, not simply what
hardware it has.

### Example

If I run a web application on my laptop and another computer connects to
it, my laptop is acting as a **server** for that application.

------------------------------------------------------------------------

# 3. What Does a Real Server Look Like?

In companies and data centers, you will often find many physical
servers.

A simplified view looks like this:

``` text
                Data Center
                     |
       +-------------+-------------+
       |             |             |
    Server 1      Server 2      Server 3
       |             |             |
    Website       Database        API
```

Each physical server has resources such as:

-   CPU
-   RAM
-   Storage
-   Network interface

But there is a problem.

## What if we have a very powerful physical server?

Suppose we have one machine with:

``` text
CPU  → 32 cores
RAM  → 128 GB
Storage → 2 TB
```

And our application only needs:

``` text
CPU  → 4 cores
RAM  → 8 GB
```

A lot of the physical machine's resources may remain unused.

This leads us to an important concept:

# Virtualization

------------------------------------------------------------------------

# 4. What Is Virtualization?

**Virtualization is the process of creating virtual versions of
computing resources instead of using only physical resources directly.**

For our discussion, the most important example is creating **virtual
computers**, called Virtual Machines.

Instead of using one physical server for only one application, we can
divide its resources and run multiple virtual machines.

``` text
                Physical Server
             CPU + RAM + Storage
                     |
               Virtualization
          ___________|____________
         |            |            |
        VM 1         VM 2         VM 3
       Linux        Linux        Windows
```

Each VM behaves like an independent computer.

------------------------------------------------------------------------

# 5. What Is a Virtual Machine?

A **Virtual Machine (VM)** is a software-defined computer running inside
another physical computer.

A VM can have its own:

-   CPU allocation
-   RAM allocation
-   Virtual disk
-   Network interface
-   Operating system
-   Applications

For example:

``` text
Physical Laptop
       |
       +----------------------+
       |      VirtualBox      |
       |----------------------|
       |                      |
       |     Ubuntu VM        |
       |                      |
       |  2 CPU + 4 GB RAM    |
       |  25 GB Virtual Disk  |
       |                      |
       +----------------------+
```

Your actual laptop is called the **host**.

The operating system running inside the VM is called the **guest OS**.

------------------------------------------------------------------------

# 6. A Simple Real-Life Example

Let's make the VM concept even more concrete.

Imagine you have one physical apartment building.


Instead of giving the entire building to one person, you divide it into
multiple apartments.

``` text
Physical Server
┌──────────────────────────────┐
│                              │
│  Apartment 1 → VM 1          │
│  Apartment 2 → VM 2          │
│  Apartment 3 → VM 3          │
│                              │
└──────────────────────────────┘
```

The building is the **physical server**.

The apartments are the **virtual machines**.

The resources of the building are shared between the apartments.

This is not a perfect technical analogy, but it is a useful way to
understand the basic idea.

------------------------------------------------------------------------

# 7. Why Do We Need Virtualization?

Let's first look at a simple real-life situation.

Suppose a company has three applications:

```text
Application A → Needs 4 GB RAM
Application B → Needs 4 GB RAM
Application C → Needs 4 GB RAM
```

One option is to buy three separate physical servers.

But if the hardware is powerful enough, the company could instead use virtualization and run three VMs on fewer physical machines.

```text
             Physical Server
                    |
          +---------+---------+
          |         |         |
         VM A      VM B      VM C
          |         |         |
        App A     App B     App C
```

This can improve resource utilization and make infrastructure easier to manage.

Virtualization provides several important benefits.

## Better Resource Utilization

Instead of running one workload on an entire physical server, we can run
multiple VMs.

``` text
Without Virtualization:

Server 1 → Application 1
Server 2 → Application 2
Server 3 → Application 3


With Virtualization:

          Physical Server
                |
       +--------+--------+
       |        |        |
      VM 1     VM 2     VM 3
       |        |        |
     App 1    App 2    App 3
```

This can help organizations use their hardware more efficiently.

------------------------------------------------------------------------

## Isolation

Each VM is separated from other VMs.

For example:

``` text
VM 1 → Ubuntu → Application A

VM 2 → Ubuntu → Application B

VM 3 → Windows → Application C
```

Problems inside one VM generally do not directly mean that the other VMs
become the same environment.

This isolation is one of the major reasons virtualization is useful.

------------------------------------------------------------------------

## Run Different Operating Systems

A single physical computer can run different guest operating systems
through virtualization.

For example:

``` text
Host OS
   |
Virtualization
   |
   +--- Ubuntu VM
   |
   +--- Debian VM
   |
   +--- Windows VM
```

------------------------------------------------------------------------

## Easy Testing

Suppose you want to test something on Linux.

You don't necessarily have to replace your main operating system.

You can create a Linux VM, experiment inside it, and remove the VM
later.

This makes VMs very useful for:

-   Learning
-   Development
-   Testing
-   Labs
-   DevOps practice

------------------------------------------------------------------------

# 8. What Makes a VM Possible?

Now we have another important question:

> If a VM is a virtual computer, who creates and manages it?

The answer is a **Hypervisor**.

------------------------------------------------------------------------

# 9. What Is a Hypervisor?

A **hypervisor** is software or a virtualization layer that creates and
manages Virtual Machines.

It sits between the physical hardware and the virtual machines, directly
or indirectly depending on the type.

``` text
Physical Hardware
       |
   Hypervisor
       |
  +----+----+----+
  |    |    |    |
 VM1  VM2  VM3  VM4
```

The hypervisor manages resources such as:

-   CPU
-   Memory
-   Storage
-   Networking

and assigns them to virtual machines.

------------------------------------------------------------------------

# 10. Two Types of Hypervisors

There are two commonly discussed types of hypervisors:

1.  **Type 1 --- Bare Metal**
2.  **Type 2 --- Hosted**

The major difference is **where the hypervisor runs**.

------------------------------------------------------------------------

# 11. Type 1 Hypervisor --- Bare Metal

A Type 1 hypervisor runs directly on the physical hardware.

``` text
Physical Hardware
       |
 Type 1 Hypervisor
       |
  +----+----+----+
  |    |    |    |
 VM1  VM2  VM3  VM4
```

There is no normal desktop operating system sitting underneath the
hypervisor.

### Examples

-   VMware ESXi
-   Microsoft Hyper-V
-   Xen

### Where is Type 1 Used?

Type 1 hypervisors are commonly associated with:

-   Data centers
-   Enterprise infrastructure
-   Server virtualization
-   Large-scale environments

The main idea is that the hypervisor directly manages the underlying
hardware resources.

------------------------------------------------------------------------

# 12. Type 2 Hypervisor --- Hosted

A Type 2 hypervisor runs on top of an existing operating system.

``` text
Physical Hardware
       |
     Host OS
       |
 Type 2 Hypervisor
       |
  +----+----+
  |         |
 VM1       VM2
```

For example, your laptop may already be running Windows.

You install VirtualBox on Windows.

Then VirtualBox creates and runs an Ubuntu VM.

``` text
Laptop Hardware
       |
    Windows
       |
   VirtualBox
       |
  Ubuntu VM
```

### Examples

-   Oracle VirtualBox
-   VMware Workstation
-   VMware Fusion

### Where is Type 2 Useful?

Type 2 hypervisors are very convenient for:

-   Learning
-   Local development
-   Testing
-   Running Linux on a Windows/macOS machine
-   DevOps labs

------------------------------------------------------------------------

# 13. Why Are There Two Types?

The basic difference is the layer where the hypervisor sits.

### Type 1

``` text
Hardware
   ↓
Hypervisor
   ↓
VMs
```

### Type 2

``` text
Hardware
   ↓
Host OS
   ↓
Hypervisor
   ↓
VMs
```

Type 1 is commonly used for server/data-center virtualization.

Type 2 is convenient for desktop users because you can install it like a
normal application on your existing operating system.

------------------------------------------------------------------------

# 14. Type 1 vs Type 2

  Feature                     Type 1                 Type 2
  --------------------------- ---------------------- -----------------
  Also called                 Bare Metal             Hosted
  Runs on                     Hardware               Host OS
  Common use                  Servers/Data Centers   Desktop/Lab
  Example                     VMware ESXi            VirtualBox
  Existing host OS required   No                     Yes
  Desktop learning            Less convenient        Very convenient

------------------------------------------------------------------------

# 15. Our Practical Example

For this course, we will use:

**Oracle VirtualBox**

VirtualBox is a **Type 2 hypervisor**.

Our setup will look like this:

``` text
Your Physical Laptop
        |
     Windows
        |
    VirtualBox
        |
    Ubuntu VM
        |
   Linux Commands
```

Your Windows system will continue running normally.

Inside Windows, VirtualBox will create a virtual computer.

Inside that virtual computer, we will install Ubuntu.

------------------------------------------------------------------------

# 16. Host vs Guest

These two terms are extremely important.

### Host

The physical computer and its main operating system.

Example:

``` text
My Laptop
Windows
```

### Guest

The operating system running inside the VM.

Example:

``` text
Ubuntu
```

So:

``` text
HOST
Windows Laptop
     |
     ↓
VirtualBox
     |
     ↓
GUEST
Ubuntu VM
```

------------------------------------------------------------------------

# 17. Allocating Resources to a VM

When creating a VM, we decide how many resources the VM can use.

For example:

``` text
Physical Laptop
8 GB RAM
4 CPU cores
```

We could allocate:

``` text
Ubuntu VM
4 GB RAM
2 CPU cores
25 GB virtual disk
```

The VM can use those allocated resources while it is running.

This does **not** mean the VM physically contains a separate CPU and RAM
stick.

These are virtualized resources provided by the host system.

------------------------------------------------------------------------

# 18. Important Point About RAM

Suppose your laptop has:

``` text
8 GB RAM
```

and you give:

``` text
4 GB RAM
```

to your VM.

While the VM is running, approximately that amount of memory is
available to the VM.

That means your host operating system still needs enough RAM to
function.

So don't allocate all of your RAM to the VM.

For example:

``` text
8 GB Laptop
     |
     +--- Windows → remaining RAM
     |
     +--- Ubuntu VM → 4 GB
```

------------------------------------------------------------------------

# 19. Virtual Disk

The VM also needs storage.

We can create something like:

``` text
Ubuntu VM
    |
    +--- Virtual Disk → 25 GB
```

This is a file or virtual disk representation stored on the host's
physical storage.

From inside Ubuntu, it behaves like a normal disk.

------------------------------------------------------------------------

# 20. What Happens When We Start the VM?

When you click **Start** in VirtualBox:

``` text
Windows
   |
VirtualBox starts
   |
Ubuntu VM boots
   |
Ubuntu kernel starts
   |
Ubuntu operating system loads
```

It feels like you have another computer running inside your computer.

------------------------------------------------------------------------

# 21. Simple Example to Remember Everything

Think about your laptop as a large building.

``` text
             PHYSICAL LAPTOP
          ┌───────────────────┐
          │                   │
          │   Windows Host    │
          │                   │
          │    VirtualBox     │
          │                   │
          │ ┌───────────────┐ │
          │ │ Ubuntu VM     │ │
          │ │               │ │
          │ │ Linux         │ │
          │ │ Applications  │ │
          │ └───────────────┘ │
          │                   │
          └───────────────────┘
```

The physical laptop provides the hardware.

Windows is the host OS.

VirtualBox is the Type 2 hypervisor.

Ubuntu is the guest OS.

And Ubuntu can now be used as our Linux learning environment.

------------------------------------------------------------------------

# 22. What We Will Do in the Next Part

In the next part, we will practically create our Ubuntu VM.

We will:

1.  Download Oracle VirtualBox.
2.  Download the Ubuntu ISO.
3.  Create a new VM.
4.  Configure CPU and RAM.
5.  Create a virtual disk.
6.  Start the VM.
7.  Install Ubuntu.
8.  Open the Linux terminal.
9.  Run our first Linux commands.

By the end, we will have a Linux machine running on our own laptop
without replacing Windows.

------------------------------------------------------------------------

# 23. Key Takeaways

Remember these concepts:

### Server

A computer providing a service or resource to clients.

### Virtualization

Creating virtual versions of computing resources.

### Virtual Machine

A virtual computer running on a physical computer.

### Hypervisor

The layer that creates and manages virtual machines.

### Type 1

``` text
Hardware
   ↓
Hypervisor
   ↓
VMs
```

### Type 2

``` text
Hardware
   ↓
Host OS
   ↓
Hypervisor
   ↓
VMs
```

### Our Setup

``` text
Physical Laptop
      ↓
   Windows
      ↓
  VirtualBox
      ↓
   Ubuntu VM
      ↓
 Linux Practice
```

------------------------------------------------------------------------

# Video Flow / What to Say

Start the video with:

> "Before we create a Virtual Machine, I want you to understand why
> Virtual Machines exist in the first place."

Then:

> "Let's start with something you already use every day --- servers."

Explain the client-server example first.

Then transition:

> "Now imagine we have a very powerful physical server, but one
> application is using only a small portion of its resources. What if we
> could divide those resources and run multiple isolated environments on
> the same physical machine?"

> "That's where virtualization comes in."

Then introduce VMs.

After explaining the VM:

> "But now you might be wondering --- who actually creates these virtual
> computers and manages their CPU, memory and storage?"

> "That's the job of a hypervisor."

Then explain Type 1 and Type 2.

Finally:

> "For our practical setup, we're going to use Oracle VirtualBox, which
> is a Type 2 hypervisor. We'll install Ubuntu inside it and use that
> Ubuntu environment to learn Linux."

------------------------------------------------------------------------

# One-Line Definitions for the Video

**Server:** A computer that provides a service or resource to other
computers.

**Virtualization:** A technology that allows physical computing
resources to be represented and used as virtual resources.

**Virtual Machine:** A software-defined computer that runs an operating
system inside another physical computer.

**Hypervisor:** A virtualization layer that creates and manages virtual
machines.

**Type 1 Hypervisor:** Runs directly on physical hardware.

**Type 2 Hypervisor:** Runs on top of a host operating system.
