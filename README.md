# KKTRAP

*kktrap — an adversary-deception shell trap for labs and CTFs*

kktrap is a lightweight Bash “booby-trap” you preload into interactive shells to frustrate intruders, slow down their workflow, and quietly capture TTPs for analysis. Instead of blocking access outright, it degrades the attacker experience with subtle sabotage—turning common commands into dead ends, faking prompts, and bending the terminal just enough to waste time while you observe.

*Why it’s interesting*

- *Deception over denial:*  Rather than a hard lock, kktrap lets you watch behavior in a controlled way. Attackers think they’re progressing; you’re collecting evidence.
  
- *Tool disruption at scale:* Popular utilities (e.g., =apt=, =git=, =nmap=, =sudo=, =ssh=, =docker=, =tmux=, =journalctl= ) are aliased to realistic errors, breaking copy-paste playbooks and automated scripts.
  
- *Credential canaries:* Fake =sudo=, =su=, and =ssh=  prompts lure password reuse and stash inputs to tamper-evident files for later review in a lab setting.
  
- *Keystroke friction:*  Readline and TTY tweaks (e.g., disabling Tab completion, remapping characters, muting Ctrl-C/Ctrl-V) add “sand in the gears” without immediately revealing the trap.
  
- *Environment confusion:* The prompt, =$SHELL=, and =PS1= are pinned; =cd= is neutered; editors open in read-only temp files; =ls= / =pwd=  lie just enough to mislead.
  
- *Quick escape hatch for owners:* A built-in =oaugustopro=  function cleans up aliases, restores bindings, reloads bash-completion, and returns you to a sane shell when you need it.
  

*Typical uses (lab-only)*

- Blue-team training and red-team emulation labs.
  
- CTF environments where you want attackers to work /through/  friction.
  
- Teaching sessions on OPSEC, TTPs, and the value of deception in incident response.
  

*How it plugs in*   
kktrap is “drop-in”: source it via =/etc/sh.shrc= using =ENV=  so every interactive shell inherits the trap. Because it relies on Bash features (aliases, readline bindings, TTY flags), there’s no daemon to manage and very little runtime footprint.

*Important notes*

- Designed for *controlled environments*  (labs, sandboxes, CTFs). Don’t deploy on shared production systems or where it could impede legitimate users.
  
- Captured inputs are for *educational/research*  purposes only. Handle any collected data responsibly and legally.
  
- Always provide yourself an escape path ( =oaugustopro= ) and document it for your team.
  

In short, kktrap is a clever, low-overhead way to turn a shell into a deception layer—perfect for demonstrating how small, well-placed misdirections can derail attacker workflows while giving defenders richer visibility in a safe, educational context.


## Install  kktrap
```
sudo su
git clone https://github.com/oaugustopro/kktrap.git
sudo cp kktrap/sh.shrc /etc/
sudo sed -i '1iexport ENV=/etc/sh.shrc\nreadonly ENV' /etc/profile && echo 'source /etc/sh.shrc' | sudo tee -a /etc/bash.bashrc
sudo sed -i 's/^\s*AcceptEnv/#&/' /etc/ssh/sshd_config && sudo systemctl restart sshd
ln -sf ~/.bash_history /dev/null
rm -rf kktrap
dirs="/etc"
find $dirs -type f -exec touch {} \;
``
