+++
title = "Remote Recovery mode"
date = 2022-02-09T17:56:26+01:00
weight = 4
chapter = false
pre = "<b>- </b>"
+++

The kairos recovery mode can be used to recover a damaged system, or to regain access remotely (with assistance) to a machine which has been lost access to. The recovery mode is accessible only from the GRUB menu, from both the LiveCD and an installed system.

{{% notice note %}}
On installed system there are two recovery modes available during boot. Below it is described only how the kairos remote recovery works. The manual recovery entry has nothing special from the standard Elemental-toolkit recovery mode. It can be used to reset the A/B partitions (with the user/pass used during setup) and perform any other operation without remote access.
{{% /notice %}}

## Boot into recovery mode

kairos recovery mode can be accessed either via ISO or from an installed system.

A GRUB menu will be displayed:
![Screenshot from 2022-04-28 17-48-06](https://user-images.githubusercontent.com/2420543/165800177-3e4cccd8-f67c-43a2-bd88-329478539400.png)

Select the last entry `kairos (remote recovery mode)` and press enter.

At this point the boot process starts and you should be welcomed by the `kairos` screen: 

![Screenshot from 2022-04-28 17-48-32](https://user-images.githubusercontent.com/2420543/165800182-9aa29c90-09e9-4c53-b3c7-c8ced262e3ac.png)

After few second the recovery process starts, and right after a QR code will be printed out of the screen along with a password which can be used later on to SSH into the machine:

![Screenshot from 2022-04-28 17-48-43](https://user-images.githubusercontent.com/2420543/165800187-4d2fe04e-c501-4ad8-a29f-32a0110eaa72.png)

At this stage, take a screenshot or a photo, just save the image with the QR code.

## Connect to the machine

In another machine you are using to connect to your server (your workstation, a jumpbox, or ..) use the `kairos` CLI to connect over the remote machine:

```
$ ./kairos bridge --qr-code-image /path/to/image.png
 INFO   Connecting to service kAIsuqiwKR
 INFO   SSH access password is yTXlkak
 INFO   SSH server reachable at 127.0.0.1:2200
 INFO   To connect, keep this terminal open and run in another terminal 'ssh 127.0.0.1 -p 2200' the password is  yTXlkak
 INFO   Note: the connection might not be available instantly and first attempts will likely fail.
 INFO         Few attempts might be required before establishing a tunnel to the host.
 INFO   Starting EdgeVPN network
 INFO   Node ID: 12D3KooWSTRBCTNGZ61wzK5tgYvFi8rQVxkXJCDUYngBWGDSyoBK
 INFO   Node Addresses: [/ip4/192.168.1.233/tcp/36071 /ip4/127.0.0.1/tcp/36071 /ip6/::1/tcp/37661]
 INFO   Bootstrapping DHT
```

At this point the bridge should start, and you should be able to see connection messages in the terminal. You can connect to the remote machine by using `ssh` and pointing it locally at `127.0.0.1:2200`. The username is not relevant, the password is print from the CLI.

The bridge operates in the foreground, so you have to kill by hitting CTRL-C.
