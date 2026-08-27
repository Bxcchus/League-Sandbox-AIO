# État des champions

Dernière mise à jour : 27 août 2026

Ce document décrit l'état des scripts de champions dans cette copie du serveur
League Sandbox pour le client 4.20.

## Signification des statuts

- **Opérationnel pour les tests** : le serveur démarre avec le champion, ses
  quatre compétences principales sont présentes et le scénario courant a été
  vérifié en jeu ou par un test de démarrage complet.
- **Candidat opérationnel** : Q, W, E, R et un `CharScript` sont présents et les
  scripts compilent, mais le champion n'a pas encore passé toute la checklist
  en jeu.
- **Partiel** : les quatre compétences principales sont présentes, mais le
  passif, un `CharScript` ou des sorts auxiliaires sont manquants.
- **Incomplet** : une ou plusieurs compétences principales sont absentes.

Un champion marqué opérationnel n'est pas nécessairement une reproduction
exacte de son comportement officiel en 4.20. Le statut signifie seulement qu'il
est suffisamment fonctionnel pour les tests de ce projet.

## Opérationnel pour les tests

| Champion | Validation actuelle | Limites connues |
| --- | --- | --- |
| **Garen** | Chargement serveur, niveau 6, bot, Q/W/E/R et partie sur Map11 | Les scripts auxiliaires `GarenRPreCast`, certaines attaques de base et le passif génèrent encore des avertissements ; l'IA est une IA de test |

## Candidats opérationnels

Ces champions ont leurs quatre sorts principaux et un `CharScript`. Ils
compilent avec le paquet actuel, mais doivent encore être testés compétence par
compétence avant de passer dans la catégorie opérationnelle.

- Akali
- Amumu
- Blitzcrank
- Darius
- DrMundo
- Ezreal
- Fiora
- Gragas
- Hecarim
- Irelia
- Jax
- Kayle
- Kogmaw
- Poppy
- Renekton
- Sion
- Tristana
- Tryndamere
- Vayne
- Volibear
- Warwick

## Partiels

Les quatre compétences principales existent, mais il manque encore un
`CharScript`, un passif ou un sort auxiliaire important.

| Champion | Reste principal à vérifier ou implémenter |
| --- | --- |
| Annie | `CharScript`, passif Pyromania et invocation de Tibbers |
| Brand | `CharScript` et passif Brand |
| Cassiopeia | `CharScript` et passif |
| Cho'Gath | Valider le passif, les effets secondaires et le chargement réel |
| Fizz | `CharScript`, passif et copies héritées à nettoyer |
| Malphite | `CharScript` et bouclier passif |
| Nasus | `CharScript`, passif et attaque renforcée de Q |
| Pantheon | Voir la section dédiée ci-dessous |
| Ryze | `CharScript`, passif Arcane Mastery et sorts auxiliaires |
| Taric | `CharScript`, passif Gemcraft et projectile de E |
| XinZhao | `CharScript`, passif et attaques renforcées de Q |

## Incomplets

| Couverture des sorts principaux | Champions |
| --- | --- |
| 3 sorts sur 4 | Caitlyn, Gangplank, Lucian |
| 2 sorts sur 4 | Lulu, MasterYi, Yasuo |
| 1 sort sur 4 | Aatrox, Anivia, Corki, Graves, Karthus, Kassadin, LeeSin, Leona, Lux, Mordekaiser, Nidalee, Shaco, Sivir, Teemo, Zed |
| Aucun sort principal utilisable détecté | Diana, Evelynn, Kalista, Olaf |

Certains champions de la dernière ligne possèdent un `CharScript` ou des
fragments de sorts. Ils restent classés incomplets tant que les classes portant
les noms attendus par les données du client n'existent pas.

## Pantheon : travail restant

Pantheon démarre, apparaît au niveau 6 et possède ses scripts principaux Q, W,
E et R. Il n'est cependant pas encore considéré opérationnel à cause des
avertissements et dépendances suivantes :

1. ajouter `CharScripts.CharScriptPantheon` et gérer correctement son passif ;
2. ajouter ou renommer `Spells.PantheonEChannel` ;
3. sortir `PantheonRFall` de la classe imbriquée `PantheonRJump` afin que le
   chargeur puisse trouver `Spells.PantheonRFall` ;
4. compléter `PantheonBasicAttack`, `PantheonBasicAttack2` et
   `PantheonCritAttack`, ou confirmer explicitement l'utilisation du fallback
   générique ;
5. tester les dégâts, ratios, coûts, délais, étourdissement de W, canalisation
   de E, portée et arrivée de R ;
6. tester mort, résurrection, rappel, achat d'objets et reconnexion.

## Travail transversal restant

### Priorité 1 — fiabiliser le scénario courant

- terminer Pantheon ;
- supprimer les avertissements auxiliaires de Garen ;
- vérifier le combat réel Pantheon contre Garen avec les sbires sur Map11 ;
- ajouter un test empêchant la réapparition des classes de scripts dupliquées.

### Priorité 2 — valider les candidats

Pour chaque candidat opérationnel :

1. démarrer une partie sans erreur de chargement propre au champion ;
2. tester attaque de base, passif, Q, W, E et R ;
3. tester montée de niveau, cooldowns, mana ou ressource secondaire ;
4. tester dégâts, soins, boucliers, buffs et contrôles ;
5. tester mort, résurrection et reconnexion ;
6. noter les différences connues avec le patch 4.20 dans ce document.

### Priorité 3 — compléter les implémentations courtes

Commencer par Caitlyn, Gangplank et Lucian, auxquels il manque seulement un sort
principal, puis Lulu, MasterYi et Yasuo.

### Priorité 4 — serveur et carte

- compléter les scripts de tourelles `SRUAP_Turret_*` de Map11 ;
- compléter ou neutraliser proprement les talents manquants ;
- remplacer l'IA Garen spécifique par une IA de bot générique capable de jouer
  plusieurs champions ;
- ajouter des tests automatisés de chargement pour chaque champion.

## Checklist avant de changer un statut

Un champion ne doit passer en **opérationnel pour les tests** que si :

- la solution compile sans erreur ;
- les tests automatisés réussissent ;
- le paquet affiche `Loaded all C# scripts` ;
- aucun `ERROR` ou `FATAL` propre au champion n'apparaît ;
- les quatre sorts et le passif ont été essayés en jeu ;
- les avertissements encore acceptés sont inscrits dans ce document.

## Base technique actuellement validée

- build de la solution : réussi ;
- tests automatisés : 22 réussis ;
- chargement des scripts C# : réussi ;
- carte active : nouvelle Faille de l'invocateur (`Map11`) ;
- scénario actif : Pantheon niveau 6 contre Garen Bot avec les sbires.

