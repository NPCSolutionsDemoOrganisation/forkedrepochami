---
title: Getting set up for the ISC course
original author: Matt Pritchard
Adapted for ISC from JASMIN workshop materials: Alison Pamment
---

> **_NOTE:_** For the purpose of this course you will be accessing resources on the [JASMIN](https://jasmin.ac.uk/about/) computing platform.

> **_NOTE:_**  For the purpose of this course, training accounts are **temporarily** assigned to course participants. In this way we can make sure that all participants have access to all the necessary resources and can minimise logistical issues during the events.
For continued use of JASMIN beyound the duration of the course, or for use of the training materials outside of one of the organised events, users are asked to apply for their own, regular JASMIN account via the normal process if they don't already have one, using an email address associated with their host institution.

> **_NOTE:_**  If the email address you've given us for your **JASMIN training account** is provided by an online service like Gmail, Hotmail or Outlook.com, we recommend that you make that account as secure as possible using 2-factor authentication: please check how to enable this with your own service provider.

> **_NOTE:_**  This takes you up to (but not including) the step of actually connecting to JASMIN: That is the subject of the pre-course session that was advertised in the course joining instructions. This exercise is just about getting everything set up so that it should work when you do connect.

# Exercise 0: Getting set up for the ISC course

### Scenario

I want to get my environment set up on my local machine so that I am ready to work through the practical exercises of the Introduction to Scientific Computing course.

### Objectives

After completing this exercise I will be able to:

 * Get hold of the resources I need for setting up my environment.
 * Set them up ready for working through the bash shell exercises.

### JASMIN resources

 * Training account
    * You will be provided with access to an account which is already set up with all the privileges you need to complete the workshop exercises.

### Local resources

 * **Email address**
    * You will have been contacted in advance of the course to provide an email address.
    * The JASMIN team will have linked your email address to one specific training account: you will be sent the details and credentials for this account.
 * **Training account credentials**. You will be sent the items in the list below, and the instructions in this exercise will cover how to set up your local machine to use them:
    * SSH Key pair
    * Passphrase for SSH Key
    * username for the training account
    * password for the training account


### Introduction

This initial exercise is about setting up what you will need in order to take part in the Introduction to Scientific Computing course, rather than learning in detail about JASMIN platform.

### Which tool should I use to connect to JASMIN?

Here are our recommendations:

| Local machine | Text only | Graphical output |
| - | - | - |
| Windows | `MobaXterm`* | NoMachine Enterprise Client* |
| MacOS | `Terminal` | NoMachine Enterprise Client* |
| Linux | `Terminal` or `xterm`| NoMachine Enterprise Client* |

<br>

> **_NOTE:_**  We recommend using NoMachine Enterprise Client, in combination with specific servers on JASMIN, instead of [X11 graphics](https://en.wikipedia.org/wiki/X_Window_System) because performance is much better over the network to your local machine. This is particularly recommended if you need to use a graphical user interface to control an application, for example manipulating a large satellite image.

> **_NOTE:_**  We recognise that other applications are available for each of these choices, but in order to keep the instructions as similar as possible between different platforms, we would ask that you stick to these recommendations at least for use during the workshop. If you choose another option and it doesn't work as you hope, we may not be able to help.

For the options marked `*` above, **you'll need to download and install software to run on your own/local machine before taking part in the course**. You should check that you have sufficient privileges (permissions) on your local machine to do this. If in doubt, ask the IT support team responsible for your **local** machine.

We'll cover all of these combinations, so please follow the instructions relevant to your local machine to ensure you have everything you need for the course.

The overall concept is as follows. All the applications we'll cover follow the same overall process:

* You have an SSH key consisting of 2 parts: public and private.
   * The *private* key (`id_rsa_jasmin`) stays with you on your local machine.
   * For your training account, the *public* key `id_rsa_jasmin.pub` is already put into the right place at the JASMIN end for you.
* The software which you use to connect to JASMIN needs to "present" your private key, but to do that, first you have to load it, which involves "unlocking" it with its passphrase. 
> **_NOTE:_**  Private keys for accessing JASMIN must always be protected with a strong passphrase. **DO NOT** use an unprotected private key, and **DO NOT** share your key with anyone else. JASMIN has a strict **1 key, 1 user** policy.

You will also need to enable "agent forwarding", meaning that the same key can be used for onward connections to other machines as well as the first one. Different applications have different ways of applying this setting.
* When you use your application to connect to a JASMIN server, under the hood there's a check that the 2 halves of your key match. If they don't, you'll be denied access.
* Once you're connected, you can make onward connections to other machines inside JASMIN using the same key. But importantly, the private key does not need to be copied to JASMIN: it should stay **only** on your local machine. This helps to keep it secure.

The details of how each software tool does this may look different, but they're all essentially doing the same thing. Setting up each application will involve (not necessarily in the same order):
1. Installing the software, unless it's something built-in to your operating system
2. Telling it where your private key is, on your local machine
3. Loading that private key, using the passphrase, and enabling agent forwarding
4. (in some cases) Setting up "connection profiles" to connect to particular remote machines of your choice

In most cases, you are able to load your key into an "agent" or key manager, which means that your key remains loaded across any individual terminal sessions you open using that software. The alternative is that you need to load your key each time you open a new terminal session. Either should work, but the former can be more convenient as you only need to enter your passphrase when you first open the software, rather than for each connection.

Once all that is done, you're (almost) ready to make a connection to a remote machine.

For all the methods below, you will need to provide the location of the private key which the JASMIN team will have sent you prior to the workshop event. You should save this somewhere safe as follows: (create the directory indicated if it doesn't exist already)

|System|Location|
|-|-|
|Windows|`Desktop\ssh` (a folder called `ssh` on your Desktop)|
|MacOS|`~/.ssh` (a directory called `.ssh` in your `$HOME` directory)|
|Linux|`~/.ssh` (a directory called `.ssh` in your `$HOME` directory)|

> **_NOTE:_**  On MacOS, you may not see "hidden" directories in `Finder` unless you have enabled this in your Preferences, but you can temporarily enable this with `cmd + L-Shift + .` 

<br>

### Windows

Our recommended choice for a terminal application on Windows is **MobaXterm**.

#### Software installation
* Download from [MobaXterm](https://mobaxterm.mobatek.net/).
* Choose the "Home Edition" (free), then either the "Installer edition" or "Portable Edition" and follow the instructions.

[![MobaXterm v20.6 setup on Windows, loading private key](https://img.youtube.com/vi/yG8yyTt2R-0/0.jpg)](https://www.youtube.com/watch?v=yG8yyTt2R-0)

In the above video, you can see the steps needed to load the key, i.e:

* Tick "Use internal SSH agent "MobAgent"
* UN-tick "Use external Pageant"
* Tick "Forward SSH agents" **important**
* Click the "+" symbol to locate your private key file (i.e. wherever you put `id_rsa_jasmin`, above)
* Click OK to save the settings. MobaXterm will now need to restart.
* When you restart MobaXterm you will be prompted for the passphrase associated with your private key.

> **_NOTE:_** It is best to copy and paste the passphrase from the credentials you were sent, or from a password manager if you are using your own account. To paste, first left click in the correct place (in the terminal window somewhere) then right-click to paste what's on the Windows clipboard. Note that the characters of your password will NOT be displayed as you type/paste them (this is normal!)

Click "Start local terminal".

You can then check that your key is correctly loaded with this command in the terminal window: 

> **_NOTE:_**  In this exercise, all the workshop exercises and in JASMIN documentation, when we're showing commands and their output, the `$` at the start of a line simply represents the command prompt: **it is not a character which you need to type**. Lines without the `$` at the start represent output from a command.


```
$ ssh-add -l
```
If you see a message similar to the following, your key is correctly loaded:
```
2048 SHA256:0y7Oh7J+kN6hPotWCerXsZBlRBL205UMGlJVZ1I0A8c you@somewhere.ac.uk (RSA)

```
If not, you will need to try again before you will be able to log in to a remote host using the key.

### MacOS

Our recommended choice for a terminal application on MacOS is the `Terminal` app. Find this by searching in the "spotlight search" (magnifying glass, usually top-right in the Apple menu bar). If you're using it regularly, it may help to right-click its Dock icon and select "Options > Keep in Dock".

In a new terminal window:
```
$ ssh-add ~/.ssh/id_rsa_jasmin
```
You can add the `-K` option here: this stores the passphrase in your KeyChain, so that it's available whenever you're logged in to your Mac. Obviously, **only** do this on a machine where your initial login after rebooting is protected by a strong password and/or fingerprint ID.

You'll be prompted for your passphrase at this point.

> **_NOTE:_** It is best to copy and paste the passphrase from the credentials you were sent, or from a password manager if you are using your own account. Note that the characters of your password will not be displayed as you type/paste them (this is normal!)

> **_NOTE:_**  [Advanced users] You can also add that same line to your `~/.bashrc` so that this is automatically done for you in each new terminal window you open. Only when you reboot your machine will you be prompted for your passphrase.
For full details see the `man` page for `ssh-add`.

In the same terminal window, check that your key is now loaded:

```
$ ssh-add -l
```
You should see output like this:
```
2048 SHA256:0y7Oh7J+kN6hPotWCerXsZBlRBL205UMGlJVZ1I0A8c you@somewhere.ac.uk (RSA)

```
If not, you will need to try again before you will be able to log in to a remote host using the key.

### Linux

The Linux platform has various terminal applications available depending on which flavour of Linux and which desktop manager you use: there are too many to cover them all, but the command-line instructions should be the same.

Start your terminal application (`Terminal` or `xterm`). If you're in a desktop environment, you may find this in a menu or by using the search.

Then, initiate an agent to store your key:
```
$ eval $(ssh-agent -s)
Agend pid XXX       (where XXX is some process ID)
```

Now, load your key, having stored it in your `~/.ssh` directory:
```
$ ssh-add ~/.ssh/id_rsa_jasmin
```

You'll be prompted for the passphrase at this point.

> **_NOTE:_** It is best to copy and paste the passphrase from the credentials you were sent, or from a password manager if you are using your own account. Note that the characters of your password will not be displayed as you type/paste them (this is normal!)

Check it's loaded
```
$ ssh-add -l
```
You should see output like this:
```
2048 SHA256:0y7Oh7J+kN6hPotWCerXsZBlRBL205UMGlJVZ1I0A8c you@somewhere.ac.uk (RSA)

```
If not, you will need to try again before you will be able to log in to a remote host using the key.

### Troubleshooting loading your key

1. Unprotected key

   If you see a message like the following, this means that you need to restrict the permissions on your key file so that only you (and no other users on your system) can read your key.
   ```
   @@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@
   @         WARNING: UNPROTECTED PRIVATE KEY FILE!          @
   @@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@
   Permissions 0644 for 'id_rsa_jasmin' are too open.
   It is required that your private key files are NOT accessible by others.
   This private key will be ignored.
   ```
   You can do this with a command like this (you'll need to do this in a terminal window):
   ```
   chmod 600 <path>/id_rsa_jasmin  
   ```
   where `<path>` is wherever you saved your key (see above: this can vary by platform).

2. Agent refused connection

   Sometimes this message is displayed, but as long as your key is listed when you do `ssh-add -l` then the command has worked.

3. Could not open a connection to your authentication agent

   This means that the agent is not running, for some reason. If you can't find out why, having checked the instructions above for your platform, you can start it manually with
   ```
   $ eval (ssh-agent -s)
   agent pid 1234    # or some similar output
   ```
   You can then load your key as described above with the `ssh-add` command. Loaded this way, the key may or may not persist between sessions.
   
4. Not prompted for your passphrase when MobaXterm restarts (having specified the location of your key)
   * In MobaXterm settings / SSH
      * Check that you have ticked "Use internal SSH Agent 'MobAgent'"
      * Check that you have UN-ticked "Use external pageant"
      * (you should also have ticked "Forward SSH agents", but that's not relevant to this problem)
   * Restart MobaXterm, retry
   * Uninstall MobaXterm, download the latest version & re-install. Reboot your machine. Cross your fingers ;-)
   * If it still doesn't work then start a session window and refer to item 3 above and load your key manually.


This video covers some issues you might encounter when logging in, including network considerations mentioned below. **Please watch this before attempting to connect in [ex01](../ex01)**. 

[![Ex00 Getting set up for the JASMIN Workshop - login issues](https://img.youtube.com/vi/3_teCxssQAU/mqdefault.jpg)](https://www.youtube.com/watch?v=3_teCxssQAU)

### Network Considerations

JASMIN is an academic research infrastructure primarily designed to be accessible from other acadmic research networks. As such, and as part of a layered approach to security, it is preferred that you access JASMIN from your institutional network. This means that if you are connecting from home via your home broadband internet service provider, it is preferred that you first access your insitutional network and then connect from a host there, or that you use your instutional Virtual Private Network (VPN) to obtain an IP address which belongs to your institutional network before making your connection.

Please consult the [documentation here](https://help.jasmin.ac.uk/article/190-check-network-details) about how to check whether your connection meets the criteria.

If it does, then you can use the "standard" login servers, `login[1,3,4].jasmin.ac.uk` and `nx-login[1,3].jasmin.ac.uk` (see below for what the `nx-` login servers are for).

If it does not, then you can use the "contingency" login servers, currently `login2.jasmin.ac.uk` and `nx-login2.jasmin.ac.uk`. You may not be able to use the standard transfer servers, however, so in this case you should use the contingency transfer server `xfer3.jasmin.ac.uk` (but if you are using your own account, rather than a training account you will need to apply for this additional role if you don't have it already.).
If you plan to become a JASMIN user for longer-term use, it's something you should sort out with your local IT support if you plan to use JASMIN longer-term after the workshop: ask them to "ensure that the IP address your machine is assigned (including when connected via VPN) has forward and reverse DNS lookup enabled."

We'll cover how to actually connect to the login servers in [exercise 1](../ex01), but please bear this in mind for your choice of which server to connect to. 

One final note: 

> **_NOTE:_**  Any account credentials but also scripts, configuration, code or data belonging to or created by your training account will be wiped after some short period (normally 48hrs) following the end of the workshop event. This is to preserve resources and clean up, but also to maintain security and to prepare the accounts for the next set of training users.
You will be reminded of this during the course and should make sure you retrieve or copy away any items that you want to keep either before the end of the course, or within the 48hrs following the end of the course.

<br>

Remember, actually connecting to JASMIN is the subject of [ex01](../ex01), so you don't necessarily need to try that step here.
<br>
Hopefully, if you've got this far, you should be good to go for the JASMIN Workshop. We look forward to seeing you there!

