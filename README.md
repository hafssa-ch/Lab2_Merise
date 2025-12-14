# Lab 2 — Gestion de Stock (Sortie)
### Modélisation des Systèmes d’Information avec Merise

---

##  Objectifs pédagogiques

Ce laboratoire a pour objectif de former l’étudiant à :
- analyser un énoncé métier,
- identifier les entités et les associations,
- construire un **Modèle Conceptuel de Données (MCD)**,
- déduire un **Modèle Logique de Données (MLD)**,
- appliquer correctement les règles de transformation Merise.

---

##  Énoncé

Le magasin vend des produits à des clients.

- Les produits possèdent une référence (code), un libellé et un prix unitaire.
- Les clients ont une identité, un nom, un prénom et une adresse.
- Les clients passent des commandes.
- Pour chaque commande, on mémorise la date et une adresse de livraison.
- Une commande concerne plusieurs produits.
- Pour chaque produit commandé, une quantité est précisée.

---

##  Analyse de l’énoncé (repérage métier)

### Entités identifiées
- **Produit**
- **Client**
- **Commande**

### Relation importante
- Une commande contient plusieurs produits
- Pour chaque produit, on mémorise une **quantité**

 Il s’agit d’une **association N–N avec attribut (Quantité)** entre **Commande** et **Produit**.

---

## Dictionnaire de données

| Nom | Description | Nature | Type | Contraintes | Entité / Association |
|----|------------|-------|------|------------|---------------------|
| CodeProd | Référence du produit | NC | Alphanumérique | Unique, obligatoire | PRODUIT |
| LibProd | Libellé du produit | NC | Alphanumérique | Obligatoire | PRODUIT |
| PrixUnit | Prix unitaire du produit | NC | Numérique (Décimal) | > 0, obligatoire | PRODUIT |
| IdClient | Identifiant du client | NC | Numérique (Entier) | Unique, obligatoire | CLIENT |
| NomClient | Nom du client | NC | Alphanumérique | Obligatoire | CLIENT |
| PrenomClient | Prénom du client | NC | Alphanumérique | Obligatoire | CLIENT |
| AdresseClient | Adresse du client | NC | Alphanumérique | Obligatoire | CLIENT |
| NumCmd | Numéro de commande | NC | Numérique (Entier) | Unique, obligatoire | COMMANDE |
| DateCmd | Date de la commande | NC | Date | Obligatoire | COMMANDE |
| AdresseLiv | Adresse de livraison | NC | Alphanumérique | Obligatoire | COMMANDE |
| QteCmd | Quantité commandée d’un produit | NC | Numérique (Entier) | > 0, obligatoire | CONTENIR |

### Remarques pédagogiques
- **AdresseLiv** dépend de la commande, pas du client.
- **QteCmd** dépend du couple *(Commande, Produit)* → attribut d’association.

---

##  Règles de gestion

- **RG1** : Un client peut passer 0 à N commandes.
- **RG2** : Une commande est passée par un seul client.
- **RG3** : Une commande possède une date obligatoire.
- **RG4** : Une commande possède une adresse de livraison obligatoire.
- **RG5** : Une commande concerne au moins un produit (1..N).
- **RG6** : Un produit peut apparaître dans 0 à N commandes.
- **RG7** : Pour chaque produit commandé, une quantité est saisie.
- **RG8** : La quantité commandée doit être strictement supérieure à 0.
- **RG9** : Le prix unitaire d’un produit doit être strictement supérieur à 0.
- **RG10** : Les identifiants **IdClient**, **NumCmd** et **CodeProd** sont uniques.

---

##  MCD (Modèle Conceptuel de Données)

<img width="1299" height="583" alt="image" src="https://github.com/user-attachments/assets/2d74403c-b5ee-42e1-b9d1-828b4d96707f" />

---

##  MPD 

<img width="1320" height="594" alt="image" src="https://github.com/user-attachments/assets/5854ddd2-79f3-45d5-a747-d0b9c4fa78c1" />

## Modèle relationnel

CLIENT(IdClient, NomClient, PrenomClient, AdresseClient)

PRODUIT(CodeProd, LibProd, PrixUnit)

COMMANDE(NumCmd, DateCmd, AdresseLiv, IdClient#)

LIGNE_COMMANDE(NumCmd#, CodeProd#, QteCmd)
