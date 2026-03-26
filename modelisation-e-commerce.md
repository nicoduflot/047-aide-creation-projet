# Modèle E-commerce

Voilà un exemple de modèle de données pour un site e-commerce



client
-------
id_client PK
raison sociale
type_client (btc - personne physique ou btb - personne morale, champs siret et tva_intracommunautaire doivent être saisie lors de la commande, fonction a implémenter côté applicatif)
siret
tva_intracommunautaire
nom
prenom
email (unique)
login (unique)
motdepasse_hash
telephone
date_naissance (CGV et vé&rification d'âge)
actif (booleen si le compte est actif ou non, RGPD la destruction d'un compte ne peut être généralement demande que par le client lui-même, soit suppression physique des données ou anonymisation des champs personnels nom, prenom, email en conservant les lignes de commandes pour les obligations comptables, a implémenter côté applicatif)
cree
modifie

produit
---------
id_produit PK
id_tva FK vers taux_tva
reference_produit (référence produit en interne, doit être unique)
prix_unitaire_ht
description
dimension
poids
publie (booleen sur la présence du produit en ligne)
cree
modifie

taux_tva
--------
id_tva PK
libelle
taux
cree
modifie

image_produit
-------------
id_image_produit PK
id_produit FK vers produit
fichier
cree
modifie

promotion
(une promotion peut concerner plusieurs produit, un produit peut avoir plusieurs promotion)
----------
id_promotion PK
type_promotion (promo, destockage, soldes, etc)
taux
date_debut
date_fin
cree
modifie

promotion_produit
-----------------
id_promotion_produit PK (pour l'évolution des promotions, par exemple taux spécifique par produit dans une promotion)
id_promotion FK vers promotion
id_produit FK vers produit

commande
--------
id_commande PK
id_client FK vers client
date_commande
id_adresse_facturation FK vers adresse
id_adresse_livraison FK vers adresse
id_statut_commande FK vers statut_commande
cree
modifie

statut_commande
----------------
id_statut_commande PK
libelle (en atente, payée, expédiée, annulée, etc. liste contrainte a définir)


ligne_commande
(on pourrait calculer le coût ht et ttc à la volée, mais dans l'idée de faire des audits, on va les écrires en dur dans les lignes de commande)
---------------
id_ligne_commande PK
id_commande FK vers commande
id_produit FK vers produit
prix_unitaire_ht
tva (figée, récupère la TVA du produit au moment de la création de la ligne de commande)
quantite_commande
cout_total_HT
cout_total_TTC

stock
------
id_stock PK
id_produit FK vers produit
stock_produit
min (quand le stock_produit est inférieur ou égal à min, alerte restock)
cree
modifie

adresse
-------
id_adresse PK
id_client FK vers client
type_adresse (facturation ou livraison rien d'autre)
ligne_adresse_1 (numero + voie)
ligne_adresse_2 (bâtiment, escalier)
ligne_adresse_3 (lieux-dit, BP, etc.)
code_postal
ville
pays
detail
cree
modifie

exemple étiquette adresse la poste
35 caractères maximum (en 2014)

A implémenter côté applicatif (impression de l'étiquette normalisée) et pas du côté BDD

Maxime De la Veulerie
987 avenue de la liberté menant le 
peuple batiment b escalier c
75001 Paris 
France