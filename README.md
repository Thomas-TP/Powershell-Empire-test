# 🚀 Installation de PowerShell-Empire sur Kali Linux

<div align="center">
  <a href="#">
    <img src="https://capsule-render.vercel.app/api?type=waving&color=gradient&customColorList=27&height=300&section=header&text=Thomas%20P.&fontSize=90&fontAlignY=38&desc=%20%20%7C%20Informaticien%20%7C%20&descAlignY=60&animation=fadeIn" width="100%" alt="Empire Thomas Prud'homme">
  </a>
</div>

<div align="center">
  <div>
    <img src="https://img.shields.io/badge/2024--2028-Geneva%20Institute%20of%20Technology-blue?style=for-the-badge" alt="Geneva Institute of Technology"/>
    <p>🎓 CFC d'informaticien, Informatique</p>
  </div>
</div>

## 💻 Ouvrir un terminal
Ouvrez un terminal sur votre machine Kali Linux 🐧.

## 🔄 Mettre à jour le système
```bash
sudo apt update && sudo apt upgrade -y
```

## 🛠️ Installer PowerShell-Empire
```bash
sudo apt install powershell-empire -y
```

# ⚙️ Configuration et démarrage de PowerShell-Empire

## 🏗️ Configuration initiale (première utilisation)
Lors de la première utilisation, configurez les répertoires de données pour Empire :
```bash
sudo powershell-empire setup
```

## 🚀 Démarrage du serveur PowerShell-Empire
Pour lancer le serveur PowerShell-Empire, utilisez la commande :
```bash
sudo powershell-empire server
```
Cette commande démarre le serveur Empire et l'interface web Starkiller 🌐. Vous verrez un message indiquant que "Starkiller served at http://localhost:1337/" et "Uvicorn running on http://0.0.0.0:1337".  
![image](https://hackmd.io/_Uploads/SkCqFxtZgx.png)

## 🔗 Accès à l'interface web Starkiller
- Laissez le terminal avec le serveur en cours d'exécution (ne le fermez pas 🚫).
- Ouvrez un navigateur web sur votre machine Kali Linux 🌍.
- Accédez à l'URL : [http://localhost:1337/](http://localhost:1337/).
- Connectez-vous avec les identifiants par défaut :
  - Nom d'utilisateur : `empireadmin` 👤
  - Mot de passe : `password123` 🔑  
![image](https://hackmd.io/_Uploads/ryAaceFZgx.png)

*📝 Note : Ces identifiants peuvent varier selon votre installation. Si les identifiants par défaut ne fonctionnent pas, consultez la documentation de votre version spécifique.*

## 🎧 Configuration d'un listener via Starkiller
Un listener est un composant qui attend les connexions entrantes des agents installés sur les machines cibles 🎯.

1. Dans l'interface Starkiller, cliquez sur l'onglet "Listeners" dans le menu de gauche 📡.  
![image](https://hackmd.io/_Uploads/HJVEixtZxe.png)
2. Cliquez sur le bouton "Create" ou "+" pour créer un nouveau listener ➕.
3. Sélectionnez le type de listener "HTTP" dans le menu déroulant 🌐.
4. Configurez les paramètres suivants :
   - Name : Donnez un nom à votre listener (par exemple "HTTP_9080") 📛.
   - Host : Laissez l'adresse IP de votre machine Kali (détectée automatiquement) 🖥️.
   - Port : Entrez un port disponible (par exemple "9080") 🔢.
5. Laissez les autres paramètres par défaut ou ajustez-les selon vos besoins ⚙️.
6. Cliquez sur le bouton "Submit" pour créer le listener ✅.
7. Vérifiez que votre listener apparaît dans la liste des listeners actifs avec le statut "Active" 🟢.  
![image](https://hackmd.io/_Uploads/ryhcieKZee.png)

## 🛠️ Création d'un stager via Starkiller
Un stager est un petit morceau de code qui sera exécuté sur la machine cible pour établir une connexion avec votre listener 🔗.

1. Dans l'interface Starkiller, cliquez sur l'onglet "Stagers" dans le menu de gauche 📜.  
![image](https://hackmd.io/_Uploads/SJJZnlYZle.png)
2. Cliquez sur le bouton "Create" ou "+" pour créer un nouveau stager ➕.
3. Sélectionnez le type de stager "multi/launcher" dans le menu déroulant 🚀.
4. Configurez les paramètres suivants :
   - Listener : Sélectionnez le listener que vous avez créé précédemment (par exemple "HTTP_9080") 🎧.
5. Laissez les autres paramètres par défaut ou ajustez-les selon vos besoins ⚙️.
6. Cliquez sur le bouton "Generate" pour créer le stager 📦.
7. Une fois généré, copiez le code PowerShell affiché (il s'agit d'une commande encodée en base64) 📋.  
![image](https://hackmd.io/_Uploads/rk5V3xKWlx.png)

## 🎯 Exécution du stager sur la machine cible
Dans un environnement réel, vous devriez trouver un moyen d'exécuter ce code sur la machine cible (via une vulnérabilité, un document malveillant, etc.) 🎭. Pour ce guide, nous supposons que vous avez un accès direct à la machine cible.

1. Sur la machine Windows cible, ouvrez PowerShell 🖥️.
2. Collez et exécutez le code du stager que vous avez copié précédemment ▶️.  
![image](https://hackmd.io/_Uploads/HylGq2lKbeg.png)
3. Retournez à l'interface Starkiller et cliquez sur l'onglet "Agents" dans le menu de gauche 🤖.
4. Vous devriez voir un nouvel agent apparaître dans la liste avec un nom généré automatiquement 🟢.  
![image](https://hackmd.io/_Uploads/H1JanxtZlx.png)

## 🤝 Interaction avec l'agent via Starkiller
1. Dans l'onglet "Agents", cliquez sur l'agent avec lequel vous souhaitez interagir 🤖.
2. Vous accéderez à la page de détails de l'agent qui affiche plusieurs onglets :
   - Overview : Informations générales sur l'agent 📊.
   - Interact : Pour exécuter des commandes sur l'agent 🖱️.
   - Files : Pour gérer les fichiers sur la machine cible 📂.
   - Credentials : Pour gérer les identifiants récupérés 🔑.
   - Screenshots : Pour prendre des captures d'écran 📸.
3. Dans l'onglet "Overview", vérifiez la valeur de "High Integrity" - si elle est "false", cela signifie que vous n'avez pas encore les privilèges administrateur 🚫.  
![image](https://hackmd.io/_Uploads/H1HlTxK-eg.png)

## 🔝 Escalade de privilèges via Starkiller
Pour effectuer une escalade de privilèges et obtenir des droits administrateur sur la machine cible 🔐 :

1. Dans l'interface Starkiller, cliquez sur l'onglet "Modules" dans le menu de gauche 🧰.
2. Utilisez la barre de recherche pour trouver "bypassuac" ou naviguez dans la catégorie "powershell/privesc" 🔍.
3. Cliquez sur le module "bypassuac" pour le sélectionner ⚙️.  
![image](https://hackmd.io/_Uploads/HkMIagYWle.png)
4. Configurez les paramètres suivants :
   - Agent : Sélectionnez l'agent sur lequel vous souhaitez effectuer l'escalade de privilèges 🤖.
   - Listener : Sélectionnez le listener que vous avez créé précédemment 🎧.
5. Laissez les autres paramètres par défaut ou ajustez-les selon vos besoins ⚙️.
6. Cliquez sur le bouton "Submit" pour exécuter le module ✅.
7. Si l'opération réussit, un nouvel agent avec des privilèges administrateur sera créé 🟢.
8. Retournez à l'onglet "Agents" et recherchez le nouvel agent (il aura un nom différent) 🔍.
9. Vérifiez que la valeur "High Integrity" est maintenant "true" dans les détails de l'agent ✅.  
![image](https://hackmd.io/_Uploads/ByOdpeY-le.png)

## 🔄 Mise en place de la persistance via Starkiller
Pour que l'agent se reconnecte automatiquement à votre serveur PowerShell-Empire après un redémarrage de la machine cible 🔁 :

1. Dans l'interface Starkiller, cliquez sur l'onglet "Modules" dans le menu de gauche 🧰.
2. Utilisez la barre de recherche pour trouver "schtasks" ou naviguez dans la catégorie "persistence/elevated" 🔍.
3. Cliquez sur le module "schtasks" pour le sélectionner ⚙️.  
![image](https://hackmd.io/_Uploads/HJDhTgFbgg.png)
4. Configurez les paramètres suivants :
   - Agent : Sélectionnez l'agent administrateur (celui avec "High Integrity" à "true") 🤖.
   - Listener : Sélectionnez le listener que vous avez créé précédemment 🎧.
   - OnLogon : Cochez cette option pour activer la connexion automatique à la connexion de l'utilisateur ✅.
5. Laissez les autres paramètres par défaut ou ajustez-les selon vos besoins ⚙️.
6. Cliquez sur le bouton "Submit" pour exécuter le module ✅.
7. Vous devriez voir un message de confirmation indiquant que la tâche planifiée a été créée avec succès 🟢.  
![image](https://hackmd.io/_Uploads/BJxlRxt-ll.png)

## 🛠️ Utilisation de l'agent via Starkiller
Une fois que vous avez un agent avec des privilèges administrateur et un mécanisme de persistance, vous pouvez effectuer diverses actions sur la machine cible 🚀 :

### 🖥️ Exécuter des commandes shell :
1. Dans l'onglet "Interact" de l'agent, sélectionnez "Shell" dans le menu déroulant 🖱️.
2. Entrez votre commande (par exemple "calc.exe" pour lancer la calculatrice) 🧮.
3. Cliquez sur "RUN" pour exécuter la commande ▶️.  
![image](https://hackmd.io/_Uploads/HJ3mAxFbgx.png)

### 📊 Récupérer des informations système :
1. Dans l'onglet "Interact" de l'agent, sélectionnez "Sysinfo" dans le menu déroulant 📈.
2. Cliquez sur "Submit" pour récupérer les informations système ✅.  
![image](https://hackmd.io/_Uploads/Sy-cAeK-gx.png)

### ⌨️ Capturer les frappes clavier :
1. Dans l'onglet "Modules", recherchez "keylogger" 🔍.
2. Sélectionnez le module "collection/keylogger" ⚙️.
3. Configurez l'agent cible 🤖.
4. Cliquez sur "Submit" pour démarrer la capture des frappes clavier ✅.  
![image](https://hackmd.io/_Uploads/Byc20gtZge.png)

### 🔑 Extraire des mots de passe :
1. Dans l'onglet "Modules", recherchez "mimikatz" 🔍.
2. Sélectionnez le module "credentials/mimikatz/command" ⚙️.
3. Configurez l'agent cible 🤖.
4. Cliquez sur "Submit" pour exécuter Mimikatz et extraire les mots de passe ✅.  
![image](https://hackmd.io/_Uploads/HyNlJZt-gl.png)

### 📹 Vidéo de démonstration
https://vimeo.com/1085791100/a588dbfdf3?share=copy  
<div style="position: relative; padding-bottom: 56.25%; height: 0;"><iframe id="js_video_iframe" src="https://jumpshare.com/embed/GPN6ip8bwlDWcJv84HpS" frameborder="0" webkitallowfullscreen mozallowfullscreen allowfullscreen style="position: absolute; top: 0; left: 0; width: 100%; height: 100%;"></iframe></div>

### 📊 PowerPoint de présentation
<iframe src="https://gamma.app/embed/9b4oxogok1i92pq" style="width: 700px; max-width: 100%; height: 450px" allow="fullscreen" title="Installation et utilisation de PowerShell-Empire sur Kali Linux"></iframe>

<div align="center">
  <img src="https://capsule-render.vercel.app/api?type=waving&color=gradient&customColorList=27&height=120&section=footer&animation=fadeIn" width="100%" alt="Pied de page">
</div>

<div align="center">
  <a href="#">
    <img src="https://capsule-render.vercel.app/api?type=waving&color=gradient&customColorList=27&height=300&section=header&text=Solution%20Contre%20cela&fontSize=90&fontAlignY=60&animation=fadeIn" width="100%" alt="Empire Thomas Prud'homme">
  </a>
</div>

# 🛡️ Défense contre les attaques PowerShell-Empire

PowerShell-Empire est un outil puissant pour les tests de pénétration, mais il peut être utilisé de manière malveillante pour compromettre des systèmes 🚨. Voici des stratégies pour prévenir, détecter et répondre aux attaques similaires à celles décrites ci-dessus.

## 1. 🛠️ Prévention des attaques initiales

### 🔐 Restreindre l’exécution de scripts PowerShell
- **Configurer la politique d’exécution PowerShell** : Sur les machines Windows, configurez la politique d’exécution des scripts PowerShell pour limiter l’exécution de scripts non signés. Utilisez la commande suivante dans PowerShell avec des privilèges administrateurs :
  ```powershell
  Set-ExecutionPolicy -ExecutionPolicy RemoteSigned -Scope LocalMachine
  ```
  Cette politique exige que les scripts soient signés par une autorité de confiance, rendant l’exécution de stagers malveillants plus difficile 🔒.
- **Désactiver PowerShell non essentiel** : Sur les postes de travail où PowerShell n’est pas nécessaire, désactivez-le via les stratégies de groupe (GPO) ou supprimez-le des systèmes non critiques 🚫.

### 🔐 Sécuriser les points d’entrée
- **Protéger contre les vulnérabilités** : Les stagers de PowerShell-Empire exploitent souvent des vulnérabilités (par exemple, via des documents malveillants ou des pièces jointes). Assurez-vous que :
  - Les logiciels (systèmes d’exploitation, applications) sont à jour avec les derniers correctifs de sécurité 🛠️.
  - Les pièces jointes et les liens dans les e-mails sont scannés par un antivirus robuste avec détection heuristique 🛡️.
- **Filtrage réseau** : Configurez des pare-feu pour bloquer les connexions sortantes vers des adresses IP ou domaines suspects. Les listeners Empire utilisent des ports spécifiques (par exemple, 9080). Surveillez et limitez les connexions sortantes non autorisées 🌐.

### 📚 Sensibilisation des utilisateurs
- Formez les utilisateurs à reconnaître les tentatives de phishing, qui sont souvent utilisées pour déployer des stagers 🎣. Encouragez la vérification des sources des e-mails et l’évitement des pièces jointes ou liens suspects 🚫.

## 2. 🔍 Détection des activités malveillantes

### 📜 Surveiller l’activité PowerShell
- **Activer la journalisation PowerShell** : Activez la journalisation détaillée des activités PowerShell pour détecter l’exécution de commandes suspectes, comme des stagers encodés en base64 📝. Configurez cela via les stratégies de groupe :
  - Activez l’option « Activer la journalisation des modules » et « Activer la journalisation des scripts » dans `GPO > Configuration ordinateur > Modèles d’administration > Windows PowerShell`.
  - Consultez les journaux dans l’Observateur d’événements Windows (ID 4103, 4104) 📊.
- **Utiliser un EDR (Endpoint Detection and Response)** : Déployez un EDR comme Microsoft Defender for Endpoint ou CrowdStrike pour détecter les comportements anormaux, comme l’exécution de scripts PowerShell non signés ou des connexions réseau inhabituelles 🛡️.

### 🌐 Surveiller le trafic réseau
- **Analyser les connexions sortantes** : Les agents PowerShell-Empire communiquent avec les listeners via HTTP/HTTPS. Utilisez un IDS/IPS (comme Snort ou Suricata) pour détecter des modèles de trafic inhabituels vers des ports non standards (par exemple, 1337 ou 9080) 🔍.
- **Inspecter les payloads** : Les stagers encodés en base64 peuvent être détectés par des outils d’analyse réseau qui inspectent le contenu des paquets 📦.

### 🔄 Détecter la persistance
- **Surveiller les tâches planifiées** : Les attaquants utilisent des modules comme `schtasks` pour établir la persistance. Vérifiez régulièrement les tâches planifiées avec :
  ```powershell
  Get-ScheduledTask | Where-Object {$_.State -eq "Ready"}
  ```
  Recherchez des tâches suspectes, notamment celles déclenchées à la connexion de l’utilisateur (`OnLogon`) 🔍.
- **Audit des processus** : Surveillez les processus PowerShell anormaux avec des outils comme Sysmon. Les événements Sysmon (ID 1) peuvent révéler des instances PowerShell lancées avec des arguments suspects (par exemple, `-Enc` pour les commandes encodées) 📊.

## 3. 🚨 Réponse aux incidents

### 🛑 Isoler et analyser les systèmes compromis
- **Isoler la machine** : Si un agent PowerShell-Empire est détecté (par exemple, via l’onglet « Agents » dans Starkiller), isolez immédiatement la machine compromise du réseau pour limiter la propagation 🚫.
- **Analyser les journaux** : Examinez les journaux PowerShell et réseau pour identifier le stager initial et le listener utilisé. Cherchez des commandes encodées en base64 ou des connexions vers des adresses IP inconnues 🔍.

### 🗑️ Supprimer la persistance
- **Désactiver les tâches malveillantes** : Supprimez les tâches planifiées créées par le module `schtasks` :
  ```powershell
  Unregister-ScheduledTask -TaskName "NomDeLaTacheMalveillante" -Confirm:$false
  ```
- **Nettoyer les agents** : Tuez les processus PowerShell suspects avec :
  ```powershell
  Stop-Process -Name powershell -Force
  ```

### 🔒 Renforcer les privilèges
- **Réinitialiser les comptes compromis** : Si des identifiants ont été exfiltrés (par exemple, via Mimikatz), réinitialisez immédiatement les mots de passe des comptes affectés 🔑.
- **Bloquer l’escalade de privilèges** : Appliquez le principe du moindre privilège pour limiter les comptes avec droits administrateurs. Activez l’UAC (User Account Control) pour empêcher les modules comme `bypassuac` de fonctionner sans interaction utilisateur 🔐.

## 4. 🛠️ Outils et bonnes pratiques recommandés
- **Antivirus et EDR** : Utilisez des solutions comme Microsoft Defender, Kaspersky ou CrowdStrike pour détecter les comportements malveillants de PowerShell-Empire 🛡️.
- **SIEM (Security Information and Event Management)** : Implémentez un SIEM (par exemple, Splunk ou ELK) pour corréler les journaux et détecter les anomalies 📊.
- **Mises à jour régulières** : Gardez tous les systèmes à jour pour réduire les vulnérabilités exploitables par les stagers 🔄.
- **Sauvegardes** : Maintenez des sauvegardes régulières et hors ligne pour récupérer les données en cas d’attaque par ransomware ou autre 💾.

## 5. 📚 Ressources pour approfondir
- Consultez le **Verizon Data Breach Investigations Report** pour des statistiques sur les types d’attaques similaires 📊.
- Explorez **Cybermalveillance.gouv.fr** pour des guides sur la protection contre les cyberattaques en France 🌐.
- Utilisez des outils comme **Sysinternals Suite** (notamment Sysmon et Process Explorer) pour surveiller les activités suspectes 🛠️.

En appliquant ces mesures, vous pouvez réduire considérablement le risque d’attaques utilisant des outils comme PowerShell-Empire et améliorer la résilience de vos systèmes face aux menaces similaires 💪.

<div align="center">
  <img src="https://capsule-render.vercel.app/api?type=waving&color=gradient&customColorList=27&height=120&section=footer&animation=fadeIn" width="100%" alt="Pied de page">
</div>
