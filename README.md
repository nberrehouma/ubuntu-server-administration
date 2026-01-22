GIT Repo for linux server adminstration

# when working without GUI (only with shell). many problem appreas.  one of the absence of the copy/paste convevience. in the following i try to resume many tics do deal with this issue: 

 # tmux
    - split screen ctrl-b %
    - ctrl-b ->  <- to navigate between screen panels
    - Closing a pane is as simple as closing a regular terminal session. Either type exit or hit Ctrl-d and it’s gone.
    - ctrl-b c to create new window and ctrl-b p , ctrl-b n to navigate betwwen them 
    - ctrl-b d detach from a session
    -tmux ls to list all session
    -tmux new -s <session-name> to create new session 
    -tmux attach -t < nmuber or name of session > to attach to that session
    -tmux rename-session -t 0 database to rename a session
    -type C-b ? to see a list of all available commands and start experimenting.
    - ctrl-b [ to star copy mode , then deplace with arrws to the begennig of your selection position, ctrl-space to satrt selection, finish with alt-w , and paste with ctrl-b]

  # xclip 
    -copy the content of a file : xclip -selection clipboard < myfile.txt
    - pipe to clipboard  echo "hello world"> xclip -selection clipboard
    - paste to a terminal : xclip -o -selection clipboard
    - paste into file xclip -o -selection clipboard > file.txt
    - to copy a selection to clipboard
  # how to extract a file from virtual machine to the host file system
    - On the Host: Create a folder (e.g., ~/vbox_share).
    - Update package list   sudo apt update
    - Install required packages : sudo apt install -y build-essential dkms linux-headers-$(uname -r)
    -Insert Guest Additions CD image  :In VirtualBox menu  ( of the  guest window) : Devices → Insert Guest Additions CD Image 
    -Mount the CD  : sudo mount /dev/cdrom /mnt
    -Run the installer : cd /mnt && sudo ./VBoxLinuxAdditions.run
    -Reboot   : sudo reboot
    -Check if modules are loaded : lsmod | grep vbox    # Should see: vboxguest, vboxsf, vboxvideo
    - Create Shared Folder in VirtualBox   (in the seeting of the virtual machine dashboard)
    -List shared folders :ls -la /media/ # You should see something like: sf_shared
    - Access the shared folder cd /media/sf_shared   && ls -la
    -sudo usermod -aG vboxsf $USER  && groups 
