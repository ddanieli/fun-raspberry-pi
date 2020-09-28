# fun-raspberry-pi
Repository for my Raspberry Pi projects [Public]

# Setup

Starting with:

* [Cana Kit Raspberry Pi 4](https://www.canakit.com/raspberry-pi-4-starter-kit.html)
* HDMI Monitor and USB Mouse/Keyboard

## Assemble hardware and run default setup

Go through the instructions that came with the device to make sure everything is working.  The instructions were pretty straight forward and I had no problems getting it to work.

*Note:* After instructions, I tried to update the operating system and my system froze: the screen went black but my keyboard and mouse still had power.  I had the system update, terminal, and Chromium running at that time.  I manually unplugged and replugged in power and the system started again without problem but the system settings I set were not saved.  I went through the setup again but skipped the update.  I only had a terminal and Chromium running and the system froze again some time later.  I hard reset it and started again.  This time, the settings were saved.

I didn't start Chromium but opened a terminal and let it sit overnight (without problems).

At this point, I figured that I'll make this headless and use my Mac for all development.

To shutdown the device, they recommend (at a terminal):

`sudo shutdown -h now`

I pulled out the MicroSD card and put it in my Mac for this next part. 

Note: I have an SMK Link port extender for my MacBook Pro which, surprisingly, had a MicroSD slot that I had never noticed/used before now.

## Setting up a Raspberry Pi to Run Headless

Running headless means that it doesn't need to have a monitor, mouse, or keyboard.  You will connect to your Raspberry Pi remotely through your development environment (i.e., a Mac for me) via SSH.  I like this headless option more because I can use the tools like PyCharm with my settings and personalizations.

To do this, follow the instructions [here](https://desertbot.io/blog/headless-raspberry-pi-4-ssh-wifi-setup).

After you have touched the `/ssh` file and added the `/wpa_supplicant.conf` file with your configuration, plug the MicroSD card back into the device, pull out the power plug and plug it back in, the device will restarted and you will see it booting.

## Setting up SSH securely from a Mac/Linux development machine

On a Mac/Linux...

Create a keypair called `id_raspberrypi` (or whatever you want):

```
cd ~/.ssh
ssh-keygen
```

Then copy the public key to your device:

```
ssh-copy-id -i id_raspberrypi.pub pi@your_raspberry_pi_name.local:
```

While I was at it, I updated my local `~/.ssh/config` file to shorten the hostname I need to use and make ssh use this private key when connecting:

```
Host pi
  User pi
  Port 22
  Hostname your_raspberry_pi_name.local
  IdentityFile ~/.ssh/id_raspberrypi
  TCPKeepAlive yes
  IdentitiesOnly yes
```

Now, I can access the device from my Mac like this:

```
$ ssh pi
```

And I get this:

```
Linux your_raspberry_pi_name 5.4.51-v7l+ #1333 SMP Mon Aug 10 16:51:40 BST 2020 armv7l

The programs included with the Debian GNU/Linux system are free software;
the exact distribution terms for each program are described in the
individual files in /usr/share/doc/*/copyright.

Debian GNU/Linux comes with ABSOLUTELY NO WARRANTY, to the extent
permitted by applicable law.
Last login: ...
pi@your_raspberry_pi_name:~ $
```

I am now connected to the device via SSH.  I can write all software with my nice development setup on my mac, but still run any command, copy files over, sync projects with github, etc.






