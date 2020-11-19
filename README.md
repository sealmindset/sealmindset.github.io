# Windows - Passwordless SSH
#
# Preq - 
#  Git Bash for Windows
#  An account on GitHub
#
# Ref: https://docs.github.com/en/free-pro-team@latest/github/authenticating-to-github/connecting-to-github-with-ssh

# Checking for existing SSH keys
# Before you generate an SSH key, you can check to see if you have any existing SSH keys.
# In Git Bash execute the following
$ ls -al ~/.ssh
total 25
drwxr-xr-x 1 <name> 197121    0 Nov 18 18:22 ./
drwxr-xr-x 1 <name> 197121    0 Nov 18 18:28 ../
-rw-r--r-- 1 <name> 197121  799 Nov 18 18:21 known_hosts

# If the private and public keys is missing, generate a pair
# In Git Bash execute the following
$ ssh-keygen -t rsa -b 4096 -C "<your registered email account on github"

# In Git Bash execute the following
# Ensure the ssh-agent is running.
$ eval $(ssh-agent -s)
> Agent pid 59566

# Modify your ~/.ssh/config file
# In Git Bash execute the following
$ vi ~/.ssh/config

# Enter the following lines in the VI editor
# In Git Bash execute the following
Host *
  AddKeysToAgent yes
  IdentityFile ~/.ssh/id_rsa
  
Host github.com
  HostName github.com
  User git

## To save
## Press the following keys Shift + :
## and type
: wq

# Add your SSH private key to the ssh-agent
# In Git Bash execute the following
$ ssh-add ~/.ssh/id_rsa

# In Git Bash execute the following
# Copy pub key into the clipboard
$ clip < ~/.ssh/id_rsa.pub

# Follow the instructions at https://docs.github.com/en/free-pro-team@latest/github/authenticating-to-github/adding-a-new-ssh-key-to-your-github-account

# Test if everything is setup correctly
# In Git Bash execute the following
$ ssh -T git@github.com
> Hi username! You've successfully authenticated, but GitHub does not
> provide shell access.
  
# Setup Git with your identity
# In Git Bash execute the following
$ git config --global user.email "you@example.com"
$ git config --global user.name "Your Name"
$ git remote set-url origin git@github.com:<name of github>/<name of github>.github.io.git

# Git Clone
# In Git Bash execute the following
$ cd Downloads
$ git clone https://github.com/<name of github>/<name of github>.github.io.git
$ cd <name of github>.github.io

# Update or add a file
# For example, create a file called index.html

# Now push the file into your GitHub repository with entering a password
# In Git Bash execute the following
$ git add index.html
$ git commit -m "Testing"
$ git push
