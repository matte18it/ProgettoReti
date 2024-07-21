# 🌐 Sviluppo di una rete usando GNS3 🌐
Il progetto consiste nello sviluppo e simulazione di una rete locale (Firewalling+routing+configurazione) utilizzando GNS3. 
La traccia del mio progetto è la seguente:<br>
<div align="center">
  <img src="https://github.com/matte18it/ProgettoReti/blob/main/Traccia.png" alt="Traccia Progetto">
</div>
Le specifiche del progetto sono disponibili al seguente link: [Specifiche Progetto GNS3](https://github.com/matte18it/ProgettoReti/blob/main/SpecificheProgettoGNS3.pdf)

# 🛜 Configurazione TAP 🛜
Il Tap è stato configurato attraverso il seguente script (da eseguire sulla macchina locale non su GNS3):
```shell
# Installazione pacchetti utili
sudo apt install uml-utilities
sudo su

# Crea interfaccia di rete tap0
tunctl -g netdev -t tap0

# Configura l'interfaccia di rete tap0
ifconfig tap0 xxx.xxx.xxx.xxx
ifconfig tap0 netmask xxx.xxx.xxx.xxx
ifconfig tap0 broadcast xxx.xxx.xxx.xxx
ifconfig tap0 up

# Crea le regole di firewalling
iptables -t nat -F
iptables -t nat -X
iptables -F
iptables -X
iptables -t nat -A POSTROUTING -o NOME_PROPRIA_SCHEDA_RETE_CONNESSA_INTERNET -j MASQUERADE
iptables -A FORWARD -i tap0 -j ACCEPT

sysctl -w net.ipv4.ip_forward=1

route add -net xxx.xxx.xxx.xxx/x gw xxx.xxx.xxx.xxx dev tap0
```

# ❗️ Disclaimer ❗️
Questo progetto è stato sviluppato come parte del corso "Fondamenti di Reti e Sicurezza Informatica" presso il Dipartimento di Matematica e Informatica (DeMaCS) dell'Università della Calabria. Essendo un lavoro universitario, potrebbe contenere qualche errore o imprecisione. Accolgo con piacere qualsiasi feedback e suggerimento per migliorare! Grazie per la comprensione e il supporto.
