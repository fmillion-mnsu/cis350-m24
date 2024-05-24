# Group Assignment 1

This assignment will give you some practice with executing a **port scan**, a simple type of reconaissance. Port scans allow you to probe a computer system to determine which of its IP ports are *listening* for incoming connections. While it is a relatively simple form of reconnaissance, many attackers use port scans across larger networks to test which systems might be running services of interest.

> **WARNING**
>
> Even something as simple as a port scan can be considered unauthorized access to a computer system, and if the owner of the system you scan detects the scan, you could face many consequences, including legal liability. 
>
> In this exercise you will be scanning a virtual machine image that I provide to you. As part of this assignment, you have permission to scan this image. You can also, of course, scan any equipment owned by you. However, **you MUST NOT run port scans on ANY computer system that you do not own or for which you have not received explicit permission!** The consequences depend on the target, but could result in sanctions including being denied access to computing resources up through legal prosecution. **It's not worth it - DO NOT port scan anything you don't own or have permission to scan!**
>
> You are completely 100% responsible for your behavior when you practice cybersecurity skills. "I was learning how to port scan" is **absolutely not** a valid excuse or reason for port scanning, attacking, attempting to gain access to, or otherwise disrupting or probing a computer system you do not own or have permission to attack. 
>
> If you are found to be executing port scans against systems you do not have permission to scan, you will immediately receive a grade of F for this course, as well as facing any consequences that result from such behavior. 
>
> **Don't risk it!!**

For this exercise, you need to download two virtual machine images. The images can be downloaded from D2L in the Content section under "Assignment VM Images/Assignment 1".

There are two sets of images - one for VirtualBox users who are using Windows or Intel Macs, and one for UTM users on Apple Silicon Macs.

## Steps

1. Download the two virtual machine images for your particular virtualization system.

1. Start by adding the "Target" virtual machine to your VM environment. See the [Importing VMs for VirtualBox](IMPORT_VBOX.md) or the [Importing VMs for UTM](IMPORT_UTM.md) documents for details on exactly how to add the VM to your environment.

1. Also add the "PenTest" VM to your environment.

1. **VERY IMPORTANT**: You MUST connect your virtual machines to a **Host-Only** network. (Failing to do this will result in significant point loss!) The method for assigning your VMs to a Host-Only network depends on your virtualization platform:

    # VirtualBox

    stuff

    # UTM

    stuff

1. Start up the Target VM.

    If the VM starts successfully, you should see a screen similar to this:

    **Take a screenshot of this screen**. The four code words on screen are required as part of your submission - not including these code words will result in significant loss of points.

1. Now, start up the PenTest VM.

    The VM should prompt you to login as `root` with a specific password. Log in by typing the username, pressing Enter, then typing the password given and pressing Enter.

    If you are successful, you should now see a screen similar to this:

    You are now ready to perform your port scan.

    (You do not need to screenshot the PenTest boot screen.)

1. On the PenTest VM, verify your IP address by typing the command:

        ip addr show dev eth0

    The `ip` command is a Linux command that lets you view and manipulate settings and information for network interfaces. This command is pretty straightforward: it asks to `show` the `addr`ess of `dev eth0`. Linux network devices have interface names and there are a few different schemes for assigning those addresses; a typical straightforward method is to simply name Ethernet interfaces `eth` followed by a number, in this case `0` for the first interface.

    Compare the IP address you see against the one displayed on the screen of the target VM. **Make sure the two IP addresses are on the same `/24` subnet**. In other words, make sure that the first three numbers of the IP address are the same.

1. Try to **ping** the target VM:

        ping <IP_of_target>

    If the ping works, you should see replies coming from the target VM at the IP address it indicates it has. If you see timeouts or errors, you need to check the configuration of both of your VMs to ensure they are both on the same Host-Only network.

1. Now it's time to actually execute the portscan.

        nmap <IP_of_target>

    The `nmap` command will default to performing a simple port scan of 1,000 common service ports. All of the ports that the target VM might open are within these 1,000 ports.

    If you are successful, you should see a list of open ports, similar to this:

    **Take a screenshot** showing the list of open ports.

1. Power off the target VM by closing its window and choosing to shut down the system. (Do not "save state" or "send shutdown signal" as neither of these will actually effect a full shutdown.)

1. **Repeat the port scan process two more times** for a total of three port scans. (Power on the Target VM and wait for it to display its code words and IP address, then run `nmap` again to do another scan. Once again, screenshot or note both the code words and the list of open ports.) Power off the target VM each time and then turn it back on.

1. Once you're done, you can power off the target VM again, and finally you can type

        poweroff

    at the command prompt of the PenTest VM to power it off.

> **Important:** Each time you boot or reboot the Target VM, **it will select a new random code phrase** and thus, a new random set of open ports. Therefore, **please be careful to keep track of your various port scan runs.** If you are unsure, it is better to simply start the target VM again and run a new scan, making sure you note the code words *and* the open ports at the same time.

## Deliverable

Your deliverable consists of *three* port scan trials. Each trial must include the four-word code phrase as well as the list of ports that were found to be open on the target VM with that code phrase.

You may submit screenshots or a simple document listing the code words and associated open ports. Either is acceptable.

**This is a group project - only ONE submission per group is required!** If more than one group member submits to D2L, I will grade the **most recent** submission that was submitted prior to the due date/time, so I recommend you choose one group member to upload your final results and ensure that only one submission is done per group.

## Scoring Rubric

This group project is worth 100 points:

| Item | Points | Penalties |
|-|-|-|
| Successfully executed three port-scans of the target VM with different code words per scan | 80 | 20 points lost for any scan without code words. 20 points lost for scan with incorrect open ports. |
| Proper procedures and practices followed | 20 | Point loss depends on specific infraction and severity. |

All group members will receive the same score.
