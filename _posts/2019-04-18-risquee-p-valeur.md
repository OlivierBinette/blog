---
layout: post
title: Risquée p-valeur!
categories: [Pédagogie]
---

On enseigne dans le cours de STT1000 à l'UQÀM qu'une p-valeur c'est le « plus petit risque à encourir pour rejeter $H_0​$ ».

Qu'est-ce que ça veut dire? Le professeur affirme que l'idée est de contracter la phrase que la « p-valeur est le plus petit seuil sous lequel on rejete $H_0$ ». Il faudrait plutôt dire que « la p-valeur est le plus petit seuil sous lequel on *aurait* rejeté $H_0$ », puisque le test nécéssite la spécification du seuil avant d'avoir observé les données, mais passons… Pour effectuer la contraction, il faut ensuite identifier le seuil au risque de première espèce. Problème: comme ce seuil dépend maintenant des données, il n'a plus rien avoir avec le risque de quoi que ce soit.

<!--more-->

Bon, entre statisticiens, on se comprend. Du moins je l'espère. Le professeur veut seulement éviter ici de se fatiguer la langue. Mais pas tous les étudiants ne savent décortiquer le (non-)sens de cette interprétation de la p-valeur. Ils m'arrivent donc dans leurs devoirs - je suis auxiliaire d'enseignement pour ce cours - avec toutes sortes de variantes complètement fausses. Voici à quoi ça ressemble:

- On a obtenu une p-valeur de $1\%$, et l'étudiant conclue qu'*il y a uniquement un risque de $1\%$ d'erreur [?] à déclarer $H_1​$*.
- *La p-valeur est la plus petite valeur observée [?] où il est possible d'accepter $H_1​$.*
- *La p-valeur est la chance [?] de se tromper en acceptant $H_1​$.*

Quoi faire? Est-ce que je devrais leur enlever des points en corrigeant leurs devoirs, lorsqu'ils répètent que « la p-valeur est le risque d'accepter $H_1​$ à tort » ? C'est le professeur qui va décider au final, mais je ressens quand même l'obligation de pointer l'absurdité du doigt.