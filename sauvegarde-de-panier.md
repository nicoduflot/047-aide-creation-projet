# Sauvegarde de panier

Plusieurs méthode ou façons de faire sont possibles pour la sauvegarde d'un panier.

Cela dépend tout d'abord des règles de gestion du site

**En général**

* Un visiteur non connecté à un site de e-commerce
    * on va créer un cookie (JS ou PHP) OU une entrée en sessionStorage (JS) OU en localStorage(JS) OU une entrée dans $_SESSION (PHP).
    
    **Cette entrée de données contiendra le panier actuel du visiteur**
>* **les plus****
>    * En combinant session et cookie, il devient facile de savoir si un visiteur est dékjà venu et s'il a déjà commencé à remplir un panier, de fait il est plus facile de le restaurer
>* **les moins**
>    * si seulement la session (PHP ou JS) est utilisée, quand le visiteur ferme le navigateur, le panier est normalement perdu
>    * Si le visiteur change de navigateur, il ne retrouve pas son panier

* Un visiteur non connecté à commencé a remplir son panier, il se connecte
    * possibilité de créer une entrée dans une table panier, qui contiendra généralement l'id du client enregistré et la session de panier qu'il était en train de remplir
    * Possibilité de vérifier, à la connexion du visiteur, si un ancien panier n'était pas déjà enregistré, et le recharger automatiquement si la session panier actuelle est vide (il s'est connecté avant de faire son shopping)
        * si un panier existe en bdd et qu'un panier a été commencé avant connexion, la vérification d'ancien panier enregistré peut proposer diverse options : garder l'ancien, garder l'actuel, fusion des deux panier, etc.
    * À chaque modification de la session panier, on met à jour le panier enregistré, pour s'assurer d'un synchronisation et une cohérence des deux paniers.

>Il n'existe pas de **meilleure méthode**, juste la méthode adaptée au contexte.
        
    