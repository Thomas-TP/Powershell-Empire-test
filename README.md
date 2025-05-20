<div align="center">
  <a href="#">
    <img src="https://capsule-render.vercel.app/api?type=waving&color=gradient&customColorList=27&height=300&section=header&text=Thomas%20P.&fontSize=90&fontAlignY=38&desc=%20%20%7C%20Informaticien%20%7C%20&descAlignY=60&animation=fadeIn" width="100%" alt="Bannière Thomas P.">
  </a>
</div>

# Voici la procédure/démonstration de Powershell-empire (cours de Cybérsecurité Satom IT)
---
# Installation de PowerShell-Empire sur Kali Linux

## Ouvrir un terminal
Ouvrez un terminal sur votre machine Kali Linux.

## Mettre à jour le système
```bash
sudo apt update && sudo apt upgrade -y
```

## Installer PowerShell-Empire
```bash
sudo apt install powershell-empire -y
```

# Configuration et démarrage de PowerShell-Empire

## Configuration initiale (première utilisation)
Lors de la première utilisation, vous devez configurer les répertoires de données pour Empire :
```bash
sudo powershell-empire setup
```

## Démarrage du serveur PowerShell-Empire
Pour lancer le serveur PowerShell-Empire, utilisez la commande :
```bash
sudo powershell-empire server
```
Cette commande démarre le serveur Empire et l'interface web Starkiller. Vous verrez un message indiquant que "Starkiller served at http://localhost:1337/" et "Uvicorn running on http://0.0.0.0:1337".
![image](https://hackmd.io/_uploads/SkCqFxtZgx.png)

## Accès à l'interface web Starkiller
- Laissez le terminal avec le serveur en cours d'exécution (ne le fermez pas).
- Ouvrez un navigateur web sur votre machine Kali Linux.
- Accédez à l'URL : [http://localhost:1337/](http://localhost:1337/).
- Connectez-vous avec les identifiants par défaut :
  - Nom d'utilisateur : `empireadmin`
  - Mot de passe : `password123`
![image](https://hackmd.io/_uploads/ryAaceFZgx.png)

*Note : Ces identifiants peuvent varier selon votre installation. Si les identifiants par défaut ne fonctionnent pas, consultez la documentation de votre version spécifique.*

## Configuration d'un listener via Starkiller
Un listener est un composant qui attend les connexions entrantes des agents installés sur les machines cibles.

1. Dans l'interface Starkiller, cliquez sur l'onglet "Listeners" dans le menu de gauche.
![image](https://hackmd.io/_uploads/HJVEixtZxe.png)

2. Cliquez sur le bouton "Create" ou "+" pour créer un nouveau listener.
3. Sélectionnez le type de listener "HTTP" dans le menu déroulant.
4. Configurez les paramètres suivants :
   - Name : Donnez un nom à votre listener (par exemple "HTTP_9080").
   - Host : Laissez l'adresse IP de votre machine Kali (détectée automatiquement).
   - Port : Entrez un port disponible (par exemple "9080").
5. Laissez les autres paramètres par défaut ou ajustez-les selon vos besoins.
6. Cliquez sur le bouton "Submit" pour créer le listener.
7. Vérifiez que votre listener apparaît dans la liste des listeners actifs avec le statut "Active".
![image](https://hackmd.io/_uploads/ryhcieKZee.png)

## Création d'un stager via Starkiller
Un stager est un petit morceau de code qui sera exécuté sur la machine cible pour établir une connexion avec votre listener.

1. Dans l'interface Starkiller, cliquez sur l'onglet "Stagers" dans le menu de gauche.
![image](https://hackmd.io/_uploads/SJJZnlYZle.png)

2. Cliquez sur le bouton "Create" ou "+" pour créer un nouveau stager.
3. Sélectionnez le type de stager "multi/launcher" dans le menu déroulant.
4. Configurez les paramètres suivants :
   - Listener : Sélectionnez le listener que vous avez créé précédemment (par exemple "HTTP_9080").
5. Laissez les autres paramètres par défaut ou ajustez-les selon vos besoins.
6. Cliquez sur le bouton "Generate" pour créer le stager.
7. Une fois généré, copiez le code PowerShell affiché (il s'agit d'une commande encodée en base64).
![image](https://hackmd.io/_uploads/rk5V3xKWlx.png)

## Exécution du stager sur la machine cible
Dans un environnement réel, vous devriez trouver un moyen d'exécuter ce code sur la machine cible (via une vulnérabilité, un document malveillant, etc.). Pour ce guide, nous supposons que vous avez un accès direct à la machine cible.

1. Sur la machine Windows cible, ouvrez PowerShell.
2. Collez et exécutez le code du stager que vous avez copié précédemment.
![image](https://hackmd.io/_uploads/HylGq2lKbeg.png)

3. Retournez à l'interface Starkiller et cliquez sur l'onglet "Agents" dans le menu de gauche.
4. Vous devriez voir un nouvel agent apparaître dans la liste avec un nom généré automatiquement.
![image](https://hackmd.io/_uploads/H1JanxtZlx.png)

## Interaction avec l'agent via Starkiller
1. Dans l'onglet "Agents", cliquez sur l'agent avec lequel vous souhaitez interagir.
2. Vous accéderez à la page de détails de l'agent qui affiche plusieurs onglets :
   - Overview : Informations générales sur l'agent.
   - Interact : Pour exécuter des commandes sur l'agent.
   - Files : Pour gérer les fichiers sur la machine cible.
   - Credentials : Pour gérer les identifiants récupérés.
   - Screenshots : Pour prendre des captures d'écran.
3. Dans l'onglet "Overview", vérifiez la valeur de "High Integrity" - si elle est "false", cela signifie que vous n'avez pas encore les privilèges administrateur.
![image](https://hackmd.io/_uploads/H1HlTxK-eg.png)

## Escalade de privilèges via Starkiller
Pour effectuer une escalade de privilèges et obtenir des droits administrateur sur la machine cible :

1. Dans l'interface Starkiller, cliquez sur l'onglet "Modules" dans le menu de gauche.
2. Utilisez la barre de recherche pour trouver "bypassuac" ou naviguez dans la catégorie "powershell/privesc".
3. Cliquez sur le module "bypassuac" pour le sélectionner.
![image](https://hackmd.io/_uploads/HkMIagYWle.png)

4. Configurez les paramètres suivants :
   - Agent : Sélectionnez l'agent sur lequel vous souhaitez effectuer l'escalade de privilèges.
   - Listener : Sélectionnez le listener que vous avez créé précédemment.
5. Laissez les autres paramètres par défaut ou ajustez-les selon vos besoins.
6. Cliquez sur le bouton "Submit" pour exécuter le module.
7. Si l'opération réussit, un nouvel agent avec des privilèges administrateur sera créé.
8. Retournez à l'onglet "Agents" et recherchez le nouvel agent (il aura un nom différent).
9. Vérifiez que la valeur "High Integrity" est maintenant "true" dans les détails de l'agent.
![image](https://hackmd.io/_uploads/ByOdpeY-le.png)

## Mise en place de la persistance via Starkiller
Pour que l'agent se reconnecte automatiquement à votre serveur PowerShell-Empire après un redémarrage de la machine cible :

1. Dans l'interface Starkiller, cliquez sur l'onglet "Modules" dans le menu de gauche.
2. Utilisez la barre de recherche pour trouver "schtasks" ou naviguez dans la catégorie "persistence/elevated".
3. Cliquez sur le module "schtasks" pour le sélectionner.
![image](https://hackmd.io/_uploads/HJDhTgFbgg.png)

4. Configurez les paramètres suivants :
   - Agent : Sélectionnez l'agent administrateur (celui avec "High Integrity" à "true").
   - Listener : Sélectionnez le listener que vous avez créé précédemment.
   - OnLogon : Cochez cette option pour activer la connexion automatique à la connexion de l'utilisateur.
5. Laissez les autres paramètres par défaut ou ajustez-les selon vos besoins.
6. Cliquez sur le bouton "Submit" pour exécuter le module.
7. Vous devriez voir un message de confirmation indiquant que la tâche planifiée a été créée avec succès.
![image](https://hackmd.io/_uploads/BJxlRxt-ll.png)

## Utilisation de l'agent via Starkiller
Une fois que vous avez un agent avec des privilèges administrateur et un mécanisme de persistance, vous pouvez effectuer diverses actions sur la machine cible :

### Exécuter des commandes shell :
1. Dans l'onglet "Interact" de l'agent, sélectionnez "Shell" dans le menu déroulant.
2. Entrez votre commande (par exemple "calc.exe" pour lancer la calculatrice).
3. Cliquez sur "RUN" pour exécuter la commande.
![image](https://hackmd.io/_uploads/HJ3mAxFbgx.png)

### Récupérer des informations système :
1. Dans l'onglet "Interact" de l'agent, sélectionnez "Sysinfo" dans le menu déroulant.
2. Cliquez sur "Submit" pour récupérer les informations système.
![image](https://hackmd.io/_uploads/Sy-cAeK-gx.png)

### Capturer les frappes clavier :
1. Dans l'onglet "Modules", recherchez "keylogger".
2. Sélectionnez le module "collection/keylogger".
3. Configurez l'agent cible.
4. Cliquez sur "Submit" pour démarrer la capture des frappes clavier.
![image](https://hackmd.io/_uploads/Byc20gtZge.png)

### Extraire des mots de passe :
1. Dans l'onglet "Modules", recherchez "mimikatz".
2. Sélectionnez le module "credentials/mimikatz/command".
3. Configurez l'agent cible.
4. Cliquez sur "Submit" pour exécuter Mimikatz et extraire les mots de passe.
![image](https://hackmd.io/_uploads/HyNlJZt-gl.png)


### Vidéo de demonstration
https://vimeo.com/1085791100/a588dbfdf3?share=copy

<div style="position: relative; padding-bottom: 56.25%; height: 0;"><iframe id="js_video_iframe" src="https://jumpshare.com/embed/GPN6ip8bwlDWcJv84HpS" frameborder="0" webkitallowfullscreen mozallowfullscreen allowfullscreen style="position: absolute; top: 0; left: 0; width: 100%; height: 100%;"></iframe></div>

### Powerpoint presentation
<iframe src="https://gamma.app/embed/9b4oxogok1i92pq" style="width: 700px; max-width: 100%; height: 450px" allow="fullscreen" title="Installation et utilisation de PowerShell-Empire sur Kali Linux"></iframe>



<div align="center">
  <img src="https://capsule-render.vercel.app/api?type=waving&color=gradient&customColorList=27&height=120&section=footer&animation=fadeIn" width="100%" alt="Pied de page">
</div>
