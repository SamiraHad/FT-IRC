# FT-IRC
ft_irc
<img width="1637" height="981" alt="Screenshot From 2026-06-23 13-30-28" src="https://github.com/user-attachments/assets/67f443ba-fde3-4b85-8e5b-81ba30d37a07" />

<img width="1024" height="1536" alt="ChatGPT Image Jun 23, 2026, 01_12_09 PM (2)" src="https://github.com/user-attachments/assets/3be80cc9-1c18-4643-a1d1-1e56346cfad0" />

1. Classe Server
   
Définition : La classe Server représente le serveur IRC. C'est le cœur de l'application.

Rôle:

Son rôle est de gérer toutes les connexions entre le serveur et les clients. Elle crée le socket serveur, accepte les nouvelles connexions, surveille les événements avec poll(), reçoit les commandes des clients et les redirige vers le traitement approprié.

Elle gère notamment :

le socket serveur ;

les sockets des clients (file descriptors) ;

poll() ;

accept() ;

recv() / send() ;

les objets Client et Channel.

2. Classe Client
   
Définition : La classe Client représente un utilisateur connecté au serveur IRC.

Rôle : 

Son rôle est de stocker toutes les informations concernant un client afin que le serveur puisse l'identifier et communiquer avec lui.

Elle contient :

le file descriptor (fd) ;
le nickname ;

le username ;

le buffer de réception ;

l'état de l'authentification (PASS, NICK, USER).


3. Classe Channel

Définition: La classe Channel représente une channel IRC dans laquelle plusieurs clients peuvent communiquer.

Rôle : 

Son rôle est de gérer les informations et les règles propres à une channel.

Elle contient :

le nom de la channel ;
le topic ;

les membres ;

les operators ;

les invités ;

les modes (+i, +t, +k, +l).

*Pourquoi séparer ces classes ?

Respecter le principe de responsabilité unique (Single Responsibility Principle). Chaque classe possède un rôle bien défini :

Server : gérer le fonctionnement du serveur et les communications réseau.

Client : représenter un utilisateur connecté et stocker ses informations.

Channel : représenter une channel IRC et gérer ses membres ainsi que ses règles.


*Le serveur crée une socket et écoute sur un port (par exemple 6667). Plusieurs clients peuvent se connecter à ce port. À chaque nouvelle connexion, le serveur obtient une nouvelle socket (un nouveau file descriptor) pour communiquer avec ce client. Chaque client se connecte en utilisant l'adresse IP et le port du serveur. Une fois connecté, il doit s'authentifier avec PASS, choisir un pseudo avec NICK et s'identifier avec USER. Après cette authentification, le serveur accepte les autres commandes (JOIN, PRIVMSG, MODE, etc.) et fait circuler les messages entre les clients.


<img width="1086" height="1448" alt="image" src="https://github.com/user-attachments/assets/eb3636c8-ebfc-4f06-b376-65ffe6dbda6e" />




