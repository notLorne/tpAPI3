#ÉNONCÉ

    À remettre le 13 juin 2023 avant 23h59 | Équipe de 2 (30%)
    TP1 : Rapide & Dangereux (Édition ville de Montréal)

    Introduction
    Vous devez construire votre propre RestAPI qui fournira des informations supplémentaires pertinentes aux utilisateurs de votre système à partir de celui offert par la ville de Montréal (https://donnees.montreal.ca/dataset/collisions-routieres). Ce qui vous distinguera de vos concurrents est la pertinence des données fournies. Voici la liste des fonctionnalités requises :

    Cas 1 : Récupérer/Convertir les données (20 points)
    D’abord, il faut pouvoir récupérer les données de l’API de la ville de Montréal et de les afficher de la méthode que vous voulez. Ensuite, assurez-vous que si l’API de la ville n’est pas disponible, que vous soyez en mesure de convertir les données du CSV fourni sur leur site en JSON afin de les afficher, encore une fois, de la méthode que vous voulez.

    Cas 2 : Insérer les données dans MongoDB (20 points)
    Il s’agit d’insérer le contenu que vous récupérer dans votre base de données. On doit pouvoir y retrouver toutes les informations reçues par l’API ou le fichier CSV.

    Cas 3 : Gérer les données obsolètes (20 points)
    Il s’agit ici d’implémenter une mécanique de « cache ». Lorsque l’on fait appel à votre API, il faut faire en sorte de retourner des données récentes. Dans certains APIs, on a une limite sur le nombre de fois que l’on peut l’interroger. Même si ce n’est pas le cas ici, trouvez une manière de de minimiser les appels vers l’API de la ville de Montréal. Une donnée est considérée récente si elle a moins d’une journée (24h) depuis le dernier appel à l’API externe de la ville.

    Cas 4 : Visualiser les données (20 points)
    Il faut pouvoir visualiser les données qui nous intéresse. On n’affichera pas tous les éléments contenus dans notre base de données. Il faut donc afficher uniquement 10 informations au total. Affichez les 5 données descriptives que vous trouvez les plus pertinentes et affichez 5 métriques d’agrégations (statistiques) représentant des faits saillants. Par exemple, l’année où il y a eu le moins de mort. Présentez les résultats sous formes de deux tableaux.

    Cas 5 : Ajouter un repère « marker » sur une carte (20 points)
    Il faut utiliser l’API de Google (Maps) ou un autre de votre choix. Vous devrez effectuer vos recherches et lire la documentation pour savoir comment l’utiliser. Choisissez la métrique du cas 4 que vous trouvez la plus intéressante et afficher un repère sur ce lieu. Par exemple, affichez un repère à l’endroit où il y a eu le maximum de morts.

#TO DO

    Rechercher to do dans le code pour trouver les choses à faire
    Si vous ajouter un to do faites le dans le code et ici dans le readme
     
    1. Trouver le problème de connection BD aprés un nombre x de insertOne soit mongodb timeout ou la requête axios lance une erreur
        C'est pourquoi pour l'instant on limit à 100 le nombre d'objets axios.get() (fetcher) et à 1000 total les insertOne() dans la bd
        car avec des axios.get() de 1000 à la fois et un nombre illimité d'insertOne() dans la bd (possiblité de plus de 218,000) le programme fini par
        générer une erreur d'exécution

        Est-ce que c'est réglé pour de bon?

    2. Format en minutes plutôt qu'en milliseconde. Ds express.js -> console.log("APRÈS le chargement des données le serveur se mettera en attente pour [ " + timeoutDelay + " ] millisecondes")
    3. rm! siginifie remove à vérifier avant de remettre
    4. Du au fonctionnement async/await ou des Promise et de setInterval, pas moyen pour l'instant d'afficher un msg comme quoi le serveur se met en attente pour 24h au bon endroit
    5. S'entendre sur ce qu'on met pour let dataLimit = 100; let dataLimitTotal = 1000; dans express.js

#NOTES IMPLANTATION

    Cas 4: 
        Données descriptives (5)

        DT_ACCDN
            Date de l’accident (AAAA-MM-JJ).
        BORNE_KM_ACCDN
            lieu est marquée par des bornes kilométriques, le numéro
            de la borne située le plus près du site de l’accident sera
            inscrit.
        CD_LOCLN_ACCDN
            Localisation longitudinale (le long de la route) du premier fait 
            physique (impact).
        CD_PNT_CDRNL_REPRR
            Code du point cardinal pour la distance du repère:
            L’accident est survenu au nord, au sud, à l’est ou à l’ouest du
            numéro d’immeuble, de la borne kilométrique, de l’intersection
            ou du repère.
        CD_ASPCT_ROUTE
            Aspect de la route sur le lieu de l’accident au moment de Alph 2
            l’impact et dans son entourage immédiat en fonction du champ
            de vision d’un conducteur assis au volant de son véhicule.


        Métriques d’agrégations (5)

            1. Le jour de la semaine (JR_SEMN_ACCDN) où il y a le plus d'accident et que CD_COND_METEO=Pluie/bruine
            2. Le jour de la semaine (JR_SEMN_ACCDN) où il y a le plus d'accident avec CD_GENRE_ACCDN=43(arbre)
            3. Le jour de la semaine (JR_SEMN_ACCDN) où il y a le plus d'accident et que GRAVITE=Léger
            4. Rue (RUE_ACCDN) où il y a le plus d'accident à Montréal
            5. Vitesse autorisée (VITESSE_AUTOR) où il y a le plus d'accident

    Cas 5:
        Le choix est dérivé de la métriques d’agrégations "Rue (RUE_ACCDN) où il y a le plus d'accident à Montréal"
        Un repère unique sur la rue en question sera placé sur la carte. 
        Il s'agit seulement de prendre un accident qui a eu lieu sur cette rue comme point de repère (Long-Lat)

#ENTÊTE
   
    Projet: Rapide & Dangereux (Édition ville de Montréal)
    Codeurs: Joseph, Isabelle, Mathieu
    Cours : Programmation Web côté serveur (420-289-AH)
    
