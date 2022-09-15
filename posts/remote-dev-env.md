---
title: "Setup VS Code remote dev environment using DigitalOcean"
date: "2022-09-15"
---

We'll start by setting up a DigitalOcean droplet (virtual machine in the cloud), creating a non-root user and setting up VS Code remote environment

### Create a DigitalOcean account first

Well in order to setup a remote environment, you need a DigitalOcean account, you can use my referral code below to get $100 for 60 days just to try these things out 👇
[![DigitalOcean Referral Badge](https://web-platforms.sfo2.digitaloceanspaces.com/WWW/Badge%203.svg)](https://www.digitalocean.com/?refcode=34d6c62184bd&utm_campaign=Referral_Invite&utm_medium=Referral_Program&utm_source=badge)

After you're done creating an account, let's move to the next step

### Creating a Droplet

- On the left menu, click on the Droplet button
![Droplet button in the left menu](../images/remote_dev_env/droplet.png)

- Create a new droplet by clicking on the `"Create Droplet"` buton
![Create a new Droplet](../images/remote_dev_env/create_droplet.png)

- Choose a distro of your flavour (I choose Ubuntu for ease of use) and select your desired specs
![Droplet details](../images/remote_dev_env/droplet_details_1.png)

- Select the datacenter region closest to you for better latency
![Droplet region](../images/remote_dev_env/droplet_details_2.png)

- For Authentication, choose SSH keys and click on the `"New SSH Key"` button below
![Droplet region](../images/remote_dev_env/droplet_details_3.png)
Use the command `ssh-keygen` to generate an SSH key, and the file would be stored under `~/.ssh/id_rsa.pub` (for Mac and Linux) and `C:\<user_name>\.ssh\id_rsa.pub` (for Windows)

*NOTE: The command `ssh-keygen` might not work on Windows CMD, so either use Powershell or [Git Bash](https://git-scm.com/download/win)*

- Finally, click on `"Create Droplet"` at the bottom and wait for a few minutes for it to spin up
![Droplet starting](../images/remote_dev_env/droplet_starting.png)

### Connecting to droplet via SSH

- Copy the IP address
- Go to your terminal, and type 👉 `ssh root@<IP_ADDRESS>`
  - Example 👉 `ssh root@127.0.0.1`
- Once inside the Droplet, create a new `sudo` user
  - Create a new user 👉 `adduser vscode`
  - Add it to `sudo` group 👉 `usermod -aG sudo vscode`
    ![New User](../images/remote_dev_env/new_user.png)
  - Login as the user 👉 `su - vscode`
    ![New User](../images/remote_dev_env/user_vscode.png)
  - Create a new `ssh` directory 👉 `mkdir ~/.ssh`
  - Create a new file inside it 👉 `touch ~/.ssh/authorized_keys`
  - Copy the contents of `id_rsa.pub` file, present on your local PC and paste it inside the `authorized_keys` file you created on your Droplet
    - To paste the contents into `authorized_keys` file, you can use any cli based text editor, `nano` example below 👇
      ![SSH keys](../images/remote_dev_env/authorized_keys.png)
    - Press **Ctrl-X**, then **Y** and then **Enter** to save the file
  - [OPTIONAL] Type `chmod 600 ~/.ssh/authorized_keys` to make sure other users don't access this file
- Press **Ctrl-D** twice to logout from the Droplet and test ssh connection of this new user `vscode`
- Type `ssh vscode@<IP_ADDRESS>` to connect to your Droplet, but now as the user `vscode` instead of `root`

### VS Code Remote development

- Add the [**Remote - SSH** extension](https://marketplace.visualstudio.com/items?itemName=ms-vscode-remote.remote-ssh) to VS Code
![Remote SSH extension - VS Code](https://code.visualstudio.com/assets/docs/remote/ssh-tutorial/remote-ssh-extension.png)

- Go to VS Code, click on the bottom left button
![Remote - SSH button](https://code.visualstudio.com/assets/docs/remote/ssh-tutorial/remote-status-bar.png)

- Choose **Connect to host**
![Connection to host](../images/remote_dev_env/connect_host.png)

- Type in `ssh vscode@<IP_ADDRESS>`

- Choose your `ssh` folder

- Then you can connect to your Droplet for remote development
![SSH connect](../images/remote_dev_env/connect.png)

- A new window will open, with remote connection to your Drop
![New window](../images/remote_dev_env/window.png)


Now, you can make use of the VMs resources to build (and possible deploy) applications

\- KH