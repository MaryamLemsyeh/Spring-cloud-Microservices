# Objectifs : 

Créer une application basée sur une architecture micro-service qui permet de gérer les factures contenant des produits et appartenant à un client.

# Consignes : 

1.Créer le micro-service customer-service qui permet de gérer les client

2.Créer le micro-service inventory-service qui permet de gérer les produits

3. Créer la Gateway Spring cloud Gateway avec une Configuration statique du système de routage

4. Créer l'annuaire Eureka Discrovery Service

5. Faire une configuration dynamique des routes de la gateway

6. Créer le service de facturation Billing-Service en utilisant Open Feign

7. Créer un client Web Angular (Clients, Produits, Factures)

8. Déployer le serveur keycloak :
     - Créer un Realm
     - Créer un client à sécuriser
     - Créer des utilisateurs
     - Créer des rôles
     - Affecter les rôles aux utilisateurs
     - Tester les différents modes d'authentification avec Postman en montrant les contenus de Access-Token, Refresh Token 

9. Sécuriser les micro-services et le frontend angular en déployant les adaptateurs Keycloak

# Outils : 

Spring cloud.

Intellij.

Navigateur de choix.

# Démarrer le projet :

-Clôner le projet sur la repositoy : https://github.com/MaryamLemsyeh/Architacture-MS---Spring-Cloud
-Démarrer les applications.
-Démarrer l'outil d'enregistrement Eureka Discovery Client.

# Explications et captures d'écran :

Créer le gatway qui va essayer de dispatcher les requettes vers les bons microservices.
##Méthode 1 :
pour configurer le gateway on peut utiliser un fichier de format .yml
![actuator 2](https://user-images.githubusercontent.com/105390951/206061225-90217f05-acfc-42f3-a0e2-61465400336b.PNG)
![beansactuator1](https://user-images.githubusercontent.com/105390951/206061219-63bd5439-a761-4512-aa20-d7690c86440a.PNG)
![product bdd](https://user-images.githubusercontent.com/105390951/208404878-85ce1a57-9fd4-425b-a469-b3ad3b1a6c25.PNG)
![bdd console](https://user-images.githubusercontent.com/105390951/208404876-94e0ba19-d746-4819-9fbc-b7b546a522df.PNG)

## Méthode 2 : 
on peut utiliser une configuration java, 
on créer une classe de configuration, une méthode qui retourne un bean (objet route locator) pour configurer les routes, ila  besoin d'un objet en parametres qui s'appelle route locator builder, 
On a besoin d'un rapidAPI countries c'est une service public connaissant l'adresse on peut l'utiliser, il est un service externe qui ne s'enregistre pas sur discovery.
on utilise le service d'enregistrement, on demande au service de s'enregistrer et on essaye de faire la gestion de maniere dynamique mais en exploitant le log balancer.
lorsqu'on utilise la configuration statique y'a pas de log balancer, si on a plusieurs instance du même microservice on peut pas l'utiliser.

![prod](https://user-images.githubusercontent.com/105390951/208405806-b95e53ab-0156-4fab-8b4b-e651f1ec3435.PNG)
![cust](https://user-images.githubusercontent.com/105390951/208405811-eac92f19-4c04-4ec0-8eab-e774b1dfa350.PNG)
![enable eureka all](https://user-images.githubusercontent.com/105390951/206061277-b518c321-e3b9-4e3f-a1ac-5ae20aa86ebc.PNG)

## Méthode 3 : 
on créer eureka server, pour activer eureka server il faut utiliser l'annotation EnableEurekaServer, on démarre.
on active spring.cloud.discovery.enabled sur true, on trouve 3 microservices enregistrés, customer-service, product-service et gateway-service.
dans gateway on modifie la configuration , au lieu de localhost, on utilise que le nom du microservice , lb = log balancer.
![products lb gateway](https://user-images.githubusercontent.com/105390951/206061484-3c307aae-9f2f-469c-b9fc-70c85caf90b9.PNG)
![customers gateway lb](https://user-images.githubusercontent.com/105390951/206061496-f8dd13ef-347d-4089-8098-349dcd694c56.PNG)
![customers url discovery](https://user-images.githubusercontent.com/105390951/206061502-ae019372-0ddf-4b80-80df-5933e3e49848.PNG)
![discovery products url](https://user-images.githubusercontent.com/105390951/206061504-4c03e830-4f10-42bb-a44f-d2c4fdd4d1a4.PNG)

Ajouter billing-service :
Créer class client sous billing-service, quand je consulte un customer, openfile deserialize, prend les données JSON et les stock dans objet. faut garder les mêmes nom sinon on ajoute des annotations JACKSON pour faire la correspondance entre les 
avoir le detail sur les produits et clients, on utilise OpenFeign qui permet de communiquer avec les microservices via rest.
![customer1](https://user-images.githubusercontent.com/105390951/206061536-d34c5dc3-8784-4828-924c-8685ea700c71.PNG)
![product1](https://user-images.githubusercontent.com/105390951/206061541-c4342635-9604-420f-af98-a80eef3f0603.PNG)


 Réalisé par : Lemsyeh Maryam 
 Encadré par : Mr.Youssfi Mohamed
