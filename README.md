# Documentation-ActiveDirectoryDomainController-DnsServer
Hub &amp; Spoke AD DC &amp; DNS Server

![Schema](./asset/Hub2.drawio.png)

1. Prérequis :

* __Réseau__  
 `Cocher Allow pour l'option Traffic Forwaded From Remote Virtual Network afin de connecter et autoriser des applications et services à s'authentifier à travers le domain controler.`  
 `L'adresse Ip de la NIC du Domain Controler doit être en Static.`  
 `Dans Chaque Spoke il faut définir le DNS sur Custom et ajouter Ll'adresse Ip de la NIC du Domain Controler.`

* __Dans le Domain Controler__  
 ` S'assurer de choisir une extension de domaine peu utilisée, par exemple: exemple.lan, exemple.lab` 

* __les Rules__  
 __https://learn.microsoft.com/en-US/troubleshoot/windows-server/identity/config-firewall-for-ad-domains-and-trusts__  
`S'inspirer des Rules de la doc officiel afin de faciler la connexion de la VM (Client) à la VM (DomainControler).`

2. Manipulations sur les VMs et le Firewall.  

* __Créer les VMs__   
`On Bloque tous les inbounds ports (3389, 80, 443, 22) afin de gérer les options de connexions à travers le firewall.`  
`Pas d'adresse Ip public ni NSG.`
`on passe l'adresse ip NIC de la VM Domain Controler de Dynamic à Static.`

* __DNS dans les Vnets__  
`Dans les deux différents Spokes on définit le DNS sur custom dans DNS Servers et on y ajoute l'adresse ip NIC de la VM Domain Controler.`

* __Redémarrer les VMs__  

* __Firewall__  
 __https://learn.microsoft.com/en-US/troubleshoot/windows-server/identity/config-firewall-for-ad-domains-and-trusts__  
`Dans le Firewall créer une collection de network rules et ouvrir tous les ports dans la doc de l'adresse IP de la VM client à l'adresse IP de la VM domain controller`  
`Rajouter les rules DNAT pour la connexion aux VMs en RDP`
`Rajouter les APPLICATIONS RULES pour donner accès à internet aux deux VMs`

3. Manipulations dans la VM Domain Controler
