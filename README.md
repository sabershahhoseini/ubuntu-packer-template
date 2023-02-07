# Ubuntu Packer Template
If you want to create an Ubuntu image template and other repos are not willing to help you, well, this repo is the one.
I tried every repo out there but all of them were confusing and some of them were out of date and didn't work.
Here, you can create an Ubuntu 22.04 image template, and install necessary stuff on it with the help of Ansible.

## Getting Started

This template is using *Ubuntu 22.04.1*. It's tested with Packer version 1.8.5.
This repo also has an example Ansible playbook that installs *NGINX*. You can change this playbook for your own usage.

First, clone the project:

```
git clone 'https://github.com/sabershahhoseini/ubuntu-packer-template.git'
```

And build the image template:

```
packer build ubuntu-22-04.json
```

Done!

## How It Works

Well, Packer is simple to understand. Inside `ubuntu-22-04.json` file, there are configurations to instruct Packer how to build the image.

### Builder Section

In `"builders"` section, We'll tell Packer how to install OS and we will set the boot command. Then, Packer will literally type this command for us (literal magic). In this boot command, we will use `cloud-init` configs. Things like keyboard layout, running some commands, changing apt mirror, installing some packages and more.

### Provisioners Section

When `cloud-init` finishes its job, Packer reaches the `"provisioners"` section. Here, we can run shell commands, use Ansible playbooks and more.
We are using Ansible playbook for our example to config GRUB to use predictable interface names, and change `fstab` to use device path instead of UUID.
