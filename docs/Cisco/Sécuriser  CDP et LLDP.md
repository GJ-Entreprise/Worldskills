# Sécuriser - CDP et LLDP :

Ressource :

* [https://cisco.goffinet.org/ccna/gestion-infrastructure/cdp-et-lldp/](https://cisco.goffinet.org/ccna/gestion-infrastructure/cdp-et-lldp/)

Dans ce billet j'utilise uniquement un switch mais la configuration est identique sur un routeur.

---

## 0 Le laboratoire :
Voici le laboratoire que j'utilise pour tester la sécurité des protocoles CDP et LLDP :

![img](../images/Cisco/CDP-LLDP/networkPlan.png)
<div align="center">
	<i><b>Illustration 1 :</b> Plan réseau du laboratoire.</i>
</div>

Adressage MAC :

* KALI, 00:0C:29:05:A1:31
* SW-1, 0C:44:BE:18:8F:00

---

## 1 Le protocole CDP :
### 1.1 Activer CDP :
Par défaut CDP est actif sur tous les ports d'un equipement Cisco, mais il est possible de l'activer (ou ré-activer) comme ceci :
````text
SW-1(config)# cdp run
````

Ou uniquement de l'activer sur une interface :
````text
SW-1(config)# interface GigabitEthernet 0/0
SW-1(config)# cdp enable
````

--- 

### 1.2 Désactiver CDP :
Pour désactiver CDP globalement :
````text
SW-1(config)# no cdp run
````

Ou le désactiver sur un ou des port(s) spécifique(s) :
````text
SW-1(config)# interface GigabitEthernet 0/0
SW-1(config)# no cdp enable
````

---

### 1.3 Voir les voisins CDP depuis Kali :
Depuis la VM KALI, utilisation de  Wireshark avec le filtre **cdp** :

![img](../images/Cisco/CDP-LLDP/cdp.png)
<div align="center">
	<i><b>Illustration 2 :</b> Trame CDP de SW-1.</i>
</div>

Sous Kali-Linux, il est aussi possible d'utiliser ces logiciels pour récupérer les informations CDP :

 * Cdpsnarf,
 * Yersinia,

---

### 1.4 Voir les voisins CDP depuis Cisco :
Sur un switch Cisco pour voir les voisins :
````text
SW-1# show cdp neighbors detail
````

---

## 2 Le protocole LLDP :
### 2.1 Activer LLDP :
Le protocole LLDP n'est pas par défaut actif sur les équipements Cisco, mais il est possible de l'activer comme ceci :
````text
SW-1(config)# lldp run
````

Ou uniquement de l'activer sur une interface :
````text
SW-1(config)# interface GigabitEthernet 0/0
SW-1(config)# lldp transmit
````

---

### 2.2 Désactiver LLDP :
Pour désactiver LLDP globalement :
````text
SW-1(config)# no lldp run
````

Ou le désactiver sur un ou des port(s) spécifique(s) :
````text
SW-1(config)# interface GigabitEthernet 0/0
SW-1(config)# no lldp transmit
````

---

### 2.3 Voir les voisins LLDP depuis Kali :
Depuis la VM KALI, utilisation de  Wireshark avec le filtre **lldp** :

![img](../images/Cisco/CDP-LLDP/lldp.png)
<div align="center">
	<i><b>Illustration 3 :</b> Trame LLDP de SW-1.</i>
</div>

Sous Kali-Linux, il est aussi possible d'utiliser ces logiciels pour récupérer les informations LLDP :

 * Lldpd,
 * Yersinia,

---

### 2.4 Voir les voisins LLDP depuis Cisco :
Sur un switch Cisco pour voir les voisins :
````text
SW-1# show lldp neighbors detail
````

## 3 Conclusion :
Par défaut, sur les switchs et routeurs Cisco :

* CDP est activé,
* LLDP est désactivé

Il peut être possible de désactiver ces deux protocoles :

* Sur l'équipement en entier,
* Sur une interface spécifique,
