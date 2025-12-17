# Voici une liste des commandes de base utilisées par un sysadmin sur linux

Dans ce guide vous trouverez les fonctions:

- SSH
- GPG/PGP
- Pass
- Gitolite
- Git

## SSH = Secure Shell

Le protocole SSH permet une connexion sécurisé entre deux postes. Voici comment l'utiliser avec un serveur linux.

Dans le terminal du client:
>ssh test@192.168.0.1
>
>yes

Le système va vous demander le mot de passe de l'utilisateur sur lequel vous vous connecté.

## GPG/PGP 

GPG/PGP = Pretty Good Protection

GPG permet de d'encryter et de décrypter des fichiers en utilisant des clées publics et privés.

Installation:

>sudo apt install gpg

Comment générer une clée gpg:
>gpg --full-generate-key
choisir la clé (1, 2, 3 ou 4)
>1
le bit size de ta key:
>2048

date d'expiration :
>0

Ensuite vous aurez un résumé des informations de votre clé.
Choisir une passphrase

la clé sera sauvegardé dans  ~/.gnupg/pubring.kbx

Pour encrypter un fichier:

>gpg -k 

nous donne la notre clé public

et si on veut encrypter le fichier test.txt voici la ligne de commande

>gpg -r clépublictest -e test.txt

ceci va créer test.txt.gpg

Si on veut partager des informations avec quelqu'un il nous faut sa clé public alors sur son ordinateur:

>gpg --export "client2@test.com" > client2.pgp

Sur notre ordinateur:

>gpg --import client2.pgp

maintenant le fichier serait decryptable car on a la clé de "test" dans notre keychain.

pour décrypter:

>gpg -d test.txt.pgp > test.txt


## PASS

Pass est un password manager. Il contient vos mot de passe.
pour l'installer:
sudo apt-get install pass

Il faut une clé GPG

>pass init "banque de mdp"

Pour générer un mdp

>pass generate -c firefox/youtube 21  (-c va copier le mdp et 21 est la longueur)

>pass show firefox/youtube (pour voir le mdp, vous allez devoir entrer votre mdp GPG)

OpnSense installation:

Lorsque vous avez boot à partir de votre clé USB avec le iso de opnsense, vous allez être dans un live environment. 
Pour démarrer l'installtion écrivez installer au login et le mdp sera opnsense.

1. keymap selection : Default
2. Install ZFS
3. Partionning ZFS > Si il y a seulement un disque, le paramètre par défaut sera parfait
4. Disk Selection On choisit le périphérique de stockage: da0 ou nvd0
5. Yes
6. Si le périphérique de stockage est plus grand que 16gb, faites oui.
7. Entrez votre mdp
8. Complete install.

Ensuite à partir de la machine opnsense il faut configurer les ports internet.
Le port WAN = le fil qui se rend dans votre modem
Le port LAN = le fil que se rend dans votre switch ou réseau fermé.

## Gitolite

Gitolite est une application serveur de repos git

Pour installer gitolite j'utilise ce [guide](https://gitolite.com/gitolite/fool_proof_setup.html)

## Git

Git est un outil pour faire travailler plusieurs personnes sur le même projet tout en ayant un historique des modifications faites par chacuns. C'est vraiment l'outil par excellence pour gérer des données et du code.

Installation:

>sudo apt-get git

### Les commandes de base de Git

Cette commande va créer le repo "repotest".
>git init repotest

Cette commande va cloner un repo à partir de gitolite ou github.
>git clone git@gitoliteserveur:repotest

Cette commande va ajouter les modifications faites au repo.
>git add .
>git add fichiertest

Cette commande va sauvegarder les changements annoncés dans la commande add. Chaque commit crée un snapshot, on peut donc y retourner quand on veut.
>git commit -m "il faut laisser des traces de son travail"

Cette commande va synchroniser le repo avec les derniers changements.
>git push origin main

Si on veut ajouter un repo à distance:
>git remote add super_bon_repo git@github.com:test/test.git

Si on veut vérifier nos remotes:
>git remote -v
