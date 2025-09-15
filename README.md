# KKTRAP

## Instalação do kktrap
```
git clone https://github.com/oaugustopro/kktrap.git
sudo cp kktrap/sh.shrc /etc/sh.shrc
```

## Adicione em /etc/profile, acima do primeiro condicional:
```
export ENV=/etc/sh.shrc
readonly ENV
```

## Adicione em /etc/bash.bashrc:
```
source /etc/sh.shrc
```

## Edite o sshd_config:
 Comente a linha "AcceptEnv"
 Reinicie o ssh:
```
 systemctl restart sshd
```
