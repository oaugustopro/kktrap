# kktrap
Trap shell to catch naive red team members

## How to
- save the file as /etc/sh.shrc
- add to profile and to bash.bashrc the lines, I dont remember if is needed in .bashrc and .profile of all users
 export ENV=/etc/sh.shrc
 readonly ENV
- copy the bashrc
 cp /etc/bash.bashrc /etc/bash.bashcr
- add to bash.bashrc
  source /etc/sh.shrc
