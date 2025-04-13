# Projet-git-
 Étapes du projet avec les commandes Git
🔹 1. Créer un nouveau projet
bash
Copier
Modifier
mkdir todo-app
cd todo-app
git init
🔹 2. Ajouter un fichier README
bash
Copier
Modifier
echo "# To-Do App CLI" > README.md
git add README.md
git commit -m "Ajout du fichier README"
🔹 3. Créer le script principal
bash
Copier
Modifier
touch todo.py
Tu peux commencer avec un code simple :

python
Copier
Modifier
# todo.py
tasks = []

while True:
    cmd = input("Commande (add/list/quit): ")
    if cmd == "add":
        task = input("Tâche à ajouter: ")
        tasks.append(task)
    elif cmd == "list":
        for i, task in enumerate(tasks):
            print(f"{i + 1}. {task}")
    elif cmd == "quit":
        break
Puis :

bash
Copier
Modifier
git add todo.py
git commit -m "Ajout du script de base"
🔄 4. Travailler avec des branches
Créons une branche pour ajouter la fonctionnalité "supprimer une tâche" :

bash
Copier
Modifier
git checkout -b feature/delete-task
Ajoute la fonctionnalité dans le script :

python
Copier
Modifier
elif cmd == "delete":
    index = int(input("Numéro de la tâche à supprimer: ")) - 1
    if 0 <= index < len(tasks):
        tasks.pop(index)
Puis :

bash
Copier
Modifier
git add todo.py
git commit -m "Ajout de la suppression de tâche"
Revenir à la branche principale et fusionner :

bash
Copier
Modifier
git checkout main
git merge feature/delete-task
🔁 5. Suivre l’historique
bash
Copier
Modifier
git log --oneline
git status
git diff
🌐 6. Lier à GitHub (optionnel)
bash
Copier
Modifier
git remote add origin https://github.com/ton-utilisateur/todo-app.git
git branch -M main
git push -u origin main
💡 Astuce Bonus : Simuler un bug et le corriger
Fais une erreur volontaire.

Utilise git status, git diff, git log, puis corrige avec :

bash
Copier
Modifier
git checkout <fichier>
# ou
git revert <commit>


python
Copier
Modifier
myrole/
├── defaults/
├── files/
├── handlers/
├── meta/
├── tasks/
├── templates/
├── tests/
├── vars/
└── README.md
C’est une excellente base pour faire un projet Git concret DevOps 👇

✅ Idée de projet Git : Créer un rôle Ansible de configuration Nginx
🔧 Objectif :
Un rôle Ansible myrole qui :

Installe nginx

Déploie un fichier de config via template

Active et démarre le service

Ajoute un index.html personnalisé

🗂️ Étapes concrètes avec Git
1. Initialise le projet Git
bash
Copier
Modifier
cd myrole
git init
git add .
git commit -m "Initialisation du rôle Ansible"
2. Remplis le dossier tasks/main.yml
yaml
Copier
Modifier
# tasks/main.yml
---
- name: Installer Nginx
  apt:
    name: nginx
    state: present
    update_cache: yes

- name: Copier la configuration Nginx
  template:
    src: nginx.conf.j2
    dest: /etc/nginx/sites-available/default

- name: Copier le fichier index
  copy:
    src: index.html
    dest: /var/www/html/index.html

- name: Redémarrer Nginx
  service:
    name: nginx
    state: restarted
    enabled: yes
3. Ajoute le template et le fichier HTML
templates/nginx.conf.j2
nginx
Copier
Modifier
server {
    listen 80;
    server_name localhost;
    root /var/www/html;
    index index.html;
}
files/index.html
html
Copier
Modifier
<!DOCTYPE html>
<html>
  <head><title>Page déployée par Ansible</title></head>
  <body><h1>Bienvenue sur le serveur NGINX</h1></body>
</html>
Puis commit :

bash
Copier
Modifier
git add tasks/main.yml templates/nginx.conf.j2 files/index.html
git commit -m "Ajout de la tâche d'installation Nginx avec configuration et page d'accueil"
🔀 Bonus Git : Branche de test
bash
Copier
Modifier
git checkout -b add-firewall-support
Tu ajoutes une tâche UFW :

yaml
Copier
Modifier
- name: Autoriser HTTP via UFW
  ufw:
    rule: allow
    name: "Nginx Full"
Commit et merge ensuite :

bash
Copier
Modifier
git add tasks/main.yml
git commit -m "Ajout de la règle UFW pour Nginx"
git checkout main
git merge add-firewall-support



ChatGPT a dit :
Oui, je vois que tu confirmes l’arborescence classique d’un rôle Ansible avec ce screenshot 👌

Tu as un projet bien structuré nommé myrole, parfait pour versionner avec Git et y appliquer un projet DevOps concret.

✅ Étapes à faire maintenant (si ce n'est pas encore fait)
🔹 1. Initialiser Git dans myrole
bash
Copier
Modifier
cd myrole
git init
git add .
git commit -m "Initialisation du rôle Ansible"
🎯 Exercice proposé : rôle Ansible pour installer et configurer NGINX
Tu peux maintenant faire évoluer ton rôle avec :

Des variables (dans defaults/main.yml ou vars/main.yml)

Des handlers (dans handlers/main.yml pour redémarrer Nginx)

Des templates dynamiques (dans templates/)

Un playbook de test (dans un dossier tests/)

📄 Exemple de README.md pour ton projet
markdown
Copier
Modifier
# Rôle Ansible : Installation de NGINX

## Description
Ce rôle installe et configure NGINX sur des serveurs Ubuntu. Il déploie une configuration personnalisée et une page d'accueil.

## Variables disponibles

| Variable       | Description                   | Valeur par défaut |
|----------------|-------------------------------|-------------------|
| `nginx_port`   | Port sur lequel écouter       | 80                |
| `nginx_root`   | Dossier racine du serveur     | /var/www/html     |

## Utilisation

```yaml
- name: Appliquer le rôle nginx
  hosts: webservers
  roles:
    - role: myrole
Structure
bash
Copier
Modifier
myrole/
├── defaults/
├── files/
├── handlers/
├── meta/
├── tasks/
├── templates/
├── tests/
├── vars/
└── README.md
Auteur
Sana Daassi

yaml
Copier
Modifier

---


