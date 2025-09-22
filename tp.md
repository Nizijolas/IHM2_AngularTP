# TP Angular
Marc-Arold Rosemond & Nicolas Dijoud
#### Intro c'est quoi Angular et c'est quoi TypeScript

#### TP :
1. Installer Angular Cli
2. Créer un projet Angular
3. Lancer Angular voir la page de base, comprendre l'organisation d'un projet
4. créer votre premier component(une nav-bar) grâce à la ligne de commande
5. Créer plusieurs route en SPA grâce au module Router.
6. Utiliser un module  Angular pour faire une animation facilement.
7. Pour aller plus loin si vous avez le temps connexion à une Api Externe à l'aide d'un service et d'Http Provider.



#### 1 Installer Angular Cli (command line interface)

Premièrement il faut avoir npm sur votre machine, et Ensuite dans un terminal éxécuter cetter commande : 

```bash
npm install -g @angular/cli
```

Puis pour vérifer qu'Angular est bien installé :

```bash
ng --version
```

Voilà vous avez pu installer Angular Cli grâce à npm, à chaque fois que vous utiliserez Angular Cli vous commencerez vos commandes par "ng".



#### 2 Créer un projet Angular

Pour créer un nouveau projet Angular dans un terminal éxécuter la commande suivante 

```bash
ng new [nomSouhaité]
```
Lors de la génération du projet vous aller devoir choisir certaines options, voici quoi choisir pour ce tp:
 
```bash
✔ Do you want to create a 'zoneless' application without zone.js (Developer 
Preview)? No
✔ Which stylesheet format would you like to use? CSS             [ 
https://developer.mozilla.org/docs/Web/CSS                     ]
✔ Do you want to enable Server-Side Rendering (SSR) and Static Site Generation 
(SSG/Prerendering)? No

```

Cela va créer un projet dans un dossier portant le nom que vous avez écrit.

**Vous pouvez maitenant ouvrir le dossier généré avec un éditeur de code**
