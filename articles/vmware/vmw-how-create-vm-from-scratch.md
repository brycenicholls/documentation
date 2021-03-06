---
title: How to create a virtual machine from scratch | UKCloud Ltd
description: Shows how to create virtual machines from scratch within vCloud Director
services: vmware
author: Sue Highmoor

toc_rootlink: How To
toc_sub1:
toc_sub2:
toc_sub3:
toc_sub4:
toc_title: Create a virtual machine from scratch
toc_fullpath: How To/vmw-how-create-vm-from-scratch.md
toc_mdlink: vmw-how-create-vm-from-scratch.md
---

# How to create a VM from scratch

## Overview

As well as deploying pre-built VMs from a catalog, you can build your own VMs from scratch, as you would do on a physical machine, using an ISO image in place of a physical CD or DVD.

For information about creating a VM from a template, see [*How to create a VM from a template*](vmw-how-create-vm-from-template.md).

## Creating a VM from scratch

1. In vCloud Director, select the **My Cloud** tab.

    ![My Cloud tab in vCloud Director](images/vmw-vcd-tab-my-cloud.png)

2. Open the vApp in which you want to create the VM.

    > [!TIP]
    > To create a new vApp, see [*How to create a vApp*](vmw-how-create-vapp.md)

3. On the **Virtual Machines** tab, click the **Add VM** icon.

    ![Add VM icon](images/vmw-vcd-ico-add-vm.png)

4. On the *Add Virtual Machines* page of the *New Virtual Machine* wizard, click **New Virtual Machine**.

    ![New Virtual Machine button in New Virtual Machine wizard](images/vmw-vcd-btn-new-virtual-machine.png)

5. In the *New Virtual Machine* dialog box, enter a **Virtual Machine name** and, in the **Computer name** field, enter a name for the server within the operating system (OS) once built.

6. Leave the **Virtual hardware version** at the default value, unless you have a particular reason to change it.

7. Select the **Operating System Family** to use for your VM, then from the **Operating System** list, select the specific OS that you want to use.

8. Select the **Number of virtual CPUs** for your VM

    > [!NOTE]
    > With a Windows OS, select at least two vCPUs if you think you'll need two or more in the future, as the multi-processor HAL will be loaded as part of the OS build.

9. You can additionally select the number of **Cores per socket**. This may be useful if you're deploying software that uses sockets for its licensing model.

10. If you want to run virtualisation servers as a VM, select the **Expose hardware-assisted CPU virtualisation** check box.

    For example, you can run a Windows 2008 or 2012 server with Hyper‑V, or a VMware ESX host.

11. Select the amount of **Memory** (RAM) and the **Hard disk size*.

    > [!NOTE]
    >Although you can build a VM to your own specification in terms of the number of vCPUs, and amount of memory and disk space, you'll be billed based on the closest (next highest) match to a UKCloud pre-defined VM size.
    >
    > Given the flexibility of VMs, and the ability to change the number of vCPUs and amount of memory and disk space on the fly, it's often better to start small as you're not tied by the constraints of a physical server. Remember too that more vCPUs or RAM won't necessarily make a server faster, and could cost a lot more. You need to understand how well your application can make use of multi-threading.

12. Leave **Bus type** as the default.

13. Select the **Number of NICs** (network interface cards) you need in the first instance.

    ![New Virtual Machine dialog box](images/vmw-vcd-new-virtual-machine.png)

14. When you're finished, click **OK** then click **Next**.

15. On the *Configure Resources* page, select the **Storage Policy** for the VM and click **Next**.

    We recommend using the `*-*-*-Any` option as this will assume your VMs are balanced evenly across all storage pools. However, you could use this option to specifically separate VMs on different storage if required for high availability purposes. In this example, two VMs could be specifically placed on `*.*.*-Storage1` as opposed to `*.*.*-Storage2`.

    ![Configure Resources page of New Virtual Machine wizard](images/vmw-vcd-new-virtual-machine-resources.png)

16. On the *Configure Virtual Machines* page, select which **Network** to connect the VM to.

17. Select an *IP Assignment* method:

    - **Static - IP Pool** is the usual method, which injects an IP address into the VM via VMware Tools from a list of available IP addresses. The address may vary with each boot, but there is a checkbox to keep IP address assignments elsewhere within the UI once the VMs are
    created.
    - **Static - Manual** is similar to Static - IP Pool, but you need to type in a valid IP address from the pool, which the VM will then keep.
    - **DHCP** vCloud Director interacts with the OS via VMware Tools to use DHCP rather than static IPs. You'll need to define a DHCP server on your edge gateway. Check with UKCloud or your organisation administrator that this is set up before you use it.

    ![Configure Virtual Machines page of New Virtual Machine wizard](images/vmw-vcd-new-virtual-machine-vms.png)

18. Click **Next**.

19. On the *Configure Networking* page you can change how the vApp and its virtual machines connect to the VDC networks.

    You can find out about network fencing in [*How to create a vApp network*](vmw-how-create-vapp-network.md).

20. Click **Next**.

21. Review the information on the summary page and then click **Finish**.

    The VM will then be deployed as bare metal.

## Installing an operating system into a bare metal VM

1. On the **Home** or **My Cloud** page, right-click the vApp and select **Start**.

    This starts the vApp and all the VMs within it. The vApp shows a status of **Starting**, then **Running**.

2. Click the monitor display, or right-click on the VM within the vApp and select **Popout Console**.

    > [!NOTE]
    > The first time you use vCloud Director, you'll be asked to download a Remote Console client, which is a Windows installable file. You'll only need to do this once. The Remote Console client is available only on Windows, under Internet Explorer (compatibility mode) and Firefox.

3. As with a physical server, no virtual CD or DVD is available at first boot, so the server will attempt to PXE boot.

    ![VM popout console](images/vmw-vcd-vm-console.png)

4. Right-click on the VM within the main vCloud Director interface (not the popout console) and select **Insert CD/DVD from Catalog**.

5. Select the ISO image you want, then click **OK**.

6. In the popout console, click the **Reset** icon then click **OK** to reset the VM so that it picks up the virtual CD/DVD.

    ![Reset VM icon in popout console](images/vmw-vcd-ico-reset-vm.png)

    After a short while the VM will start the boot process and pick up the CD/DVD. Resize the VM window if necessary to see the whole screen.

7. Carry out the operating system install as normal. When you've finished, remember to install VMware Tools (for more information, see [*VMware Tools Installation*](vmw-ref-vmware-tools-installation.md).

## Feedback

If you have any comments on this document or any other aspect of your UKCloud experience, send them to <products@ukcloud.com>.