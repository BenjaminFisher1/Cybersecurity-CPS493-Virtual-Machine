Assignment 2 for Cybersecurity CPS493 
Professor Hoffman

This assignment is a very basic introduction to accessing and using a virtual machine running Ubuntu Server set up earlier in class, as well as a few simple user, group, and permissions commands.
I named this virtual machine "pal", as a sort of homage to HAL 9000. 

![[Pasted image 20250928150631.png]]

Once I've SSH'd in, I run the command "sudo apt update" to fetch info on any upgradable packages.

![[Pasted image 20250928151453.png]]

Here, I can see 15 packages can be upgraded. 

![[Pasted image 20250928152011.png]]

Let's upgrade those packages. 

![[Pasted image 20250928152053.png]]

Packages upgrade, and then we are greeted by a lovely purple screen and this message:

![[Pasted image 20250928152327.png]]

The next step on the assignment is to reboot, so I hit enter.

![[Pasted image 20250928152418.png]]

I hit enter on Ok to restart any services whose Daemons are using the old versions of the packages I just upgraded.

![[Pasted image 20250928152605.png]]

Some restarts have been deferred. That isn't really anything to be concerned about, as I am about to reboot the system.

![[Pasted image 20250928152718.png]]

Here, I run the straightforward command to reboot the VM.

![[Pasted image 20250928152828.png]]

After rebooting, I SSH back in. 

![[Pasted image 20250928153036.png]]

The next step is to change my user to root and show the prompt. 

![[Pasted image 20250928153303.png]]
I've successfully changed my user to root, and I back out of my previous directory.

![[Pasted image 20250928153426.png]]

This step doesn't mention anything about specific flags for the useradd command, so I'm assuming there will be no flags set.

![[Pasted image 20250928153725.png]]
Looks like the command ran successfully.

![[Pasted image 20250928153817.png]]
Because I didn't specify a home directory, useradd didn't create one for bobby.

Next, I will use the adduser command to create a user for sally.

![[Pasted image 20250928154458.png]]
It's clear that using adduser automates some steps of user creation that useradd would not. 

![[Pasted image 20250928154632.png]]
I enter a password for sally, and I am prompted to enter some basic information about the new user. I enter some made up values, then just hit enter until the prompt ends.


![[Pasted image 20250928154826.png]]
Pretty simple, I use the su command to switch users to sally.

![[Pasted image 20250928154911.png]]
Now, the prompt shows I am sally, and the hashtag from root has changed back to the dollar sign, also indicating I am no longer root.

![[Pasted image 20250928155014.png]]
Sally does not belong to sudo, so this action should be blocked.

![[Pasted image 20250928155116.png]]
As expected, sally is blocked from creating a user. 

![[Pasted image 20250928155936.png]]
I'm assuming this step has a typo. Because sally couldn't create the user earl, I believe this is meant to say "Delete the user bobby". So, I will delete bobby. 

The command to delete a user is "deluser". I exit back to the original user, named "fisherb" in my case. 
![[Pasted image 20250928162542.png]]
Goodbye bobby!

![[Pasted image 20250928162610.png]]


![[Pasted image 20250928162801.png]]
This is a pretty simply command, just entering a new password for sally. 

![[Pasted image 20250928162848.png]]
Oops! I didn't realize I was still supposed to be signed in as root. It's bad practice to stay logged in as root for a number of reasons. If I type a command that would break something within my machine, root might not give me any warning or sign that said command is bad. Additionally, staying logged in as root creates a chance for somebody else to come up to my keyboard and do whatever they please on my machine. 

![[Pasted image 20250928163151.png]]
I'm a big fan of how intuitive simple linux commands are.

![[Pasted image 20250928163251.png]]
My user id is 1000.

![[Pasted image 20250928163318.png]]

Looks like fisherb belongs to a few groups: 
- fisherb, a group just for my user
- adm, the system monitoring group
- cdrom, the group to allow other users to access CD/DVD drives
- sudo, the group to use sudo to temporarily elevate privileges
- dip, the group able to use dial-up tools
- plugdev, the group able to use and mount external drives
- lxd, the group of users who can manage the LXD container hypervisor

![[Pasted image 20250928163842.png]]

Here, I am running usermod with the flag -aG, which stands for "append group", which will add sally to the end of the group file being edited (sudo in this case). Next, I search the group file for the word "sudo" using grep, which outputs the line of the file showing sudo users. 

![[Pasted image 20250928164114.png]]

My command succeeded, and sally has been added to the sudo group. I use su to switch to sally. Now, I'll verify that she can create a new user.

![[Pasted image 20250928164616.png]]

Looks good! Sally successfully created a new user "mikey" (after being yelled at for a weak password).

![[Pasted image 20250928164839.png]]

Since I just gave sally sudo access, I can create this group while logged in as her. 

![[Pasted image 20250928165007.png]]

The group was successfully created! However, there are no members of the group currently. Let's fix that.

![[Pasted image 20250928165049.png]]

Using the same command we used to add sally to sudo, just changing the group to cybersec:
![[Pasted image 20250928165324.png]]
Checking that sally was added properly:
![[Pasted image 20250928165409.png]]

Looks good! Now sally is a member of cybersec.

![[Pasted image 20250928165457.png]]
I'm going to use the "groups" command to see which groups sally belongs to.

![[Pasted image 20250928165714.png]]

Initially, the command didn't display the updated result, so I quickly switched to my user, then back to sally. After that, the "groups" command displayed the correct result.

![[Pasted image 20250928165906.png]]

I'm going to switch back to fisherb to do this step. Then, I use "mkdir" to create the lab1 directory, and check that it executed properly using "dir".

![[Pasted image 20250928170101.png]]

Next, I check the permissions of the directory using ls -ld. This will list directories in a long format, as well as just the directories and not any files. I provide the location "./lab1/", which navigates from the working directory straight into the lab1 directory, rather than providing the entire path to lab1.

![[Pasted image 20250928170445.png]]

Looks like fisherb is both the owner and group owner here. The permissions are as follows:
- Owner: Read, Write, Execute
- Group: Read, Write, Execute
- Other: Read, Execute

![[Pasted image 20250928170742.png]]

First, I'll navigate into lab1 using cd.

![[Pasted image 20250928170821.png]]

Now I am in lab1.

Now for the bash file. I open a new instance of nano on a file called "hello". 
![[Pasted image 20250928171025.png]]

First, I add the shebang to indicate that this is a script, and specify that it should be run using a bash shell.
![[Pasted image 20250928171231.png]]

Next, I'll use a simple echo command to print "Hello World!".
![[Pasted image 20250928171338.png]]

All set! Now I save and exit nano. Next, I use cat to verify the contents of the file.
![[Pasted image 20250928171427.png]]

Looks good! Time to make it executable. I'll use chmod to make the file executable using the flag +x (add executable). Then, I'll run it using ./hello

![[Pasted image 20250928171548.png]]

It worked!

![[Pasted image 20250929122624.png]]

![[Pasted image 20250929122759.png]]

Again, running ls with the -l flag shows a long listing (including permissions), and the -a flag shows all files. Specifying "hello" will show files/directories whose name contains "hello".

The permissions are:
- Owner: Read, Write, Execute
- Group: Read, Write, Execute
- Other: Read, Execute

Now, to change the permissions so the group has write and execute permissions:

This handy cheat sheet from [GeeksForGeeks](https://www.geeksforgeeks.org/linux-unix/set-file-permissions-linux/) shows octal values of permissions for files.
![[Pasted image 20250929125331.png]]

Currently, the permissions for group are set to rwx, or 7 in octal. So, the file already has the permissions asked for in the assignment.

![[Pasted image 20250929125718.png]]

![[Pasted image 20250929125812.png]]

Running getfacl shows the access control list for the file, similar to the output of "ls -la ", just a little more detailed and organized. 

![[Pasted image 20250929130015.png]]

Here, I'm running setfacl with the -m flag (Modify) for the user sally, giving her read write permissions on the file hello.

![[Pasted image 20250929131702.png]]

After running setfacl, I fetch the ACL for hello using getfacl, showing that sally was successfully given read write permissions!


That's the end of this assignment. Overall, it was a good review of basic commands for switching between users, manipulating groups, and editing file permissions!

