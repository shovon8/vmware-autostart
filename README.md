## Introduction

This program is used to start VMware Workstation 16 Virtual Machines at boot time and suspend them automatically before system shutdown or restart.

## How to Install

Navigate to the `/opt` directory and clone this GitHub repository as follows:

```
$ cd /opt
$ git clone https://github.com/shovon8/vmware-autostart.git
$ cd /opt/vmware-autostart
```

Make sure that the `/opt/vmware-autostart/bin/autostart` shell script is executable.

```
$ sudo chmod +x bin/autostart
```

Change the login `User` and `Group` to your own login `User` and `Group` name in the `vmware-autostart.service` file.

```
[Service]
...
User=<Your Login User name>
Group=<Your Primary Group name>
```

Install the `vmware-autostart.service` systemd service.

```
$ sudo ln -s /opt/vmware-autostart/vmware-autostart.service /etc/systemd/system/vmware-autostart.service
```

For the systemd changes to take effect, reload systemd daemons.

```
$ sudo systemctl daemon-reload
```

Add the `vmware-autostart.service` to the system startup.

```
$ sudo systemctl enable vmware-autostart.service
```

## Configuring Virtual Machines

To automatically start VMware Workstation Pro 16 virtual machines on boot with this program, add the absolute path of the `.vmx` file of your desired virtual machines in the `config.json` file. The configuration file is self-explanatory.

```
{
  "vms": [
    {
      "name": "vm-1",
      "vmxpath": "/vmware/vm-1/vm-1.vmx",
      "autostart": true
    },
    {
      "name": "vm 2",
      "vmxpath": "/vmware/vm 2/vm 2.vmx",
      "autostart": true
    }
  ]
}
```

## Known Issues

If you keep a virtual machine opened in the VMware Workstation Pro 16 app, the VMware Autostart program won’t be able to suspend the virtual machine when you shutdown or reboot your computer while keeping the VMware Workstation Pro 16 app opened. It might be rare for people to shutdown or reboot their computer while keeping programs open. But the program could be improved to make sure that the VMware Workstation Pro 16 app is closed before suspending virtual machines.
