# What is SSH?
SSH stands for "Secure SHell". *Secure* means your trafic is encrypted so that nobody on the internet can see the information that you're sending to the server or the server is sending back. *Shell* just means you're administrating over the Command Line Interface. If you were to login to a text interface at a physical or virtual console, that would also be a Command Line Interface, where you can type out commands you want to execute.

In order to connect via SSH, you need:
- the IP address where you can connect to the server, or a domain name that points to that IP
- the name of the user you're logging in as, 
- some way to prove that you have access to that user
    - a password, 
    - an SSH private key file that corresponds to one of the public keys installed for that user on the server

# Use cases
### VirtualBox
If you just came here from the article about creating a new machine in Virtual Box, you'll probably notice a frustrating limitation quite quickly.  You cannot copy text from your host computer and paste it into the virtual console of the guest machine. So, if you have a guide open in a browser or a text document where you've taken notes about useful commands, you'll have to type out each command for as long as you work through the virtual console.

However, if you establish an SSH connection to the guest machine, then you will be able to paste lines of text into the "remote" connection to the guest machine.

### Remote Linux over a Network
Suppose your server is physically located in a place that's really inconvenient to reach, like the downstairs closet, or a datacenter in New York.  You'd want to be able to access it remotely and make changes, right?


# Configuring SSH access
If you're setting up this server for the first time, you'll need to make sure the program that listens for incoming SSH connections is installed and listening for incoming connections.

If you have already done this before and you just need to configure SSH access for an additional user, you can skip to the next section.

### Ensure that the SSH service is installed and listening
- Run one of these commands to see which ports the server is listening on for incoming connections:
    - `sudo lsof -i -P -n | grep LISTEN`
    - `netstat -plnt`
- Using either command above, you're looking for something that says it's listening on port 22.
- You may have to use your package manager to install the tools you need in order to see if the SSH listener is running.
- If you do not see anything listening on port 22, you need to install the SSH server using the package manager:
    - `sudo apt install openssh-server`
    - `sudo yum install openssh-server`
- If you had to install openssh-server above, run these commands to ensure that it is started and enabled.
    - `sudo systemctl start sshd`
    - `sudo systemctl enable sshd`

The last thing you'll need to do is obtain the IP address of the server. You can use this to see a list of all IPs on the server:
```
ip addr show | awk '/inet /{print $2}' | cut -d/ -f 1
```

### Connecting using a password
At this point, if a user exists on the server and has a password and SSH is running on the server, you should be able to login using the password.

If you're using PuTTY, you would put `username@IP.AD.DR.ESS` in the "Host" field and click "Open" and enter the password when prompted.  Be aware that Linux often listens for passwords silently; it does not display a `*` for every character you type.  So you'll have to type in your password and hit enter with no confirmation that the server has accepted keyboard input.

If you're using the command line on Mac or a linux work station, you'll need to connect via terminal using something similar to this command:
```
ssh username@IP.AD.DR.ESS
```

Some servers, such as AWS EC2 instances will ask you to create or input an SSH key while you are setting them up because they are deployed with password authentication disabled.  For instructions about connecting via SSH using an SSH key, please visit that section later in this document.

### Creating an SSH key
On linux, you can create an ssh key using the command `ssh-keygen`. The command will prompt you for input a few times:
- what file name would you like to create the private key
- what passphrase would you like to use to encrypt the key
- repeat passphrase
To suppress these propmts you can use:
```
ssh-keygen -t rsa -b 4096 -f path/to/file -P 'Optional_Passphrase'
```
In the above command: 
- `-t rsa` specifies to use the RSA encoding when generating the key pair
- `-b 4096` specifies the key should be 4096 bytes long; more secure than the default 2048
- `-P 'Optional_Passphrase'` specifies the passprhase. You can use `-P ''` to specify an empty passphrase and still suppress the prompt.

On Windows, you'll need to generate a key using PuTTYgen.
- Open the PuTTYgen program.
- Click the button that says "Generate" on the right hand side, midway down.
- Move your mouse over the grey area to help the program come up with a very truly random number to generate this key.
- When it's finished, the grey area will be replaced with a block of seemingly random letters. That is your public key.
- You should save the private key in a place where you will remember it.
- For convenience, if you would like to save the public key, you can do that as well.
- If you choose not to save the public key, you'll need to click the "Load" button (above "Generate") each time you want to install the public key on a new server.







