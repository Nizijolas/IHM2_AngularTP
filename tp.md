## TP Angular
**Par Marc-Arold Rosemond & Nicolas Dijoud**

### Introduction : C’est quoi Angular et TypeScript ?

**Angular** :
- Angular est un framework open-source développé par Google pour créer des applications web modernes, en particulier des **Single Page Applications (SPA)**.
- Il utilise une architecture basée sur des **composants** et offre des fonctionnalités comme le routage, la gestion des formulaires, et les appels HTTP.
- Points forts : structure modulaire, forte intégration avec TypeScript, outils CLI puissants, et prise en charge de la réactivité et des animations.

**TypeScript** :
- TypeScript est un langage similaire à JavaScript qui ajoute des types statiques, des interfaces, et d’autres fonctionnalités pour améliorer la maintenabilité et la robustesse du code. Ce qui peut permet d'avoir un code plus clair et plus facile à débuguer.

**Objectif du TP** :
- Découvrir Angular en créant une petite application SPA avec une navigation, des composants, des animations.
- Comprendre l’organisation d’un projet Angular et les outils associés.

---

### Plan du TP

#### 1. Installer Angular CLI
**Objectif** : Installer l’outil en ligne de commande Angular CLI pour créer et gérer des projets Angular.

**Prérequis** :
- **Node.js** et **npm** doivent être installés sur la machine ( Node.js - v20.19.0 ou plus récent )
  - Vérifiez avec :
    ```bash
    node --version
    npm --version
    ```
  - Si Node.js n’est pas installé, téléchargez-le depuis [nodejs.org](https://nodejs.org).

**Étapes** :
1. Installez Angular CLI globalement :
   ```bash
   npm install -g @angular/cli
   ```
2. Vérifiez l’installation :
   ```bash
   ng --version
   ```
   Cela affiche la version d’Angular CLI.
   pour mener à bien ce TP il faut que la version ne soit pas plus ancienne que la version 18.0.0


---

#### 2. Créer un projet Angular
**Objectif** : Générer un projet Angular avec une configuration adaptée au TP.

**Étapes** :
1. Créez un nouveau projet :
   ```bash
   ng new projet_tp
   ```
2. Répondez aux questions de configuration :
   ```bash
   ✔ Do you want to create a 'zoneless' application without zone.js (Developer Preview)? No
   ✔ Which stylesheet format would you like to use? CSS
   ✔ Do you want to enable Server-Side Rendering (SSR) and Static Site Generation (SSG/Prerendering)? No
   ```
   - **Explication** :
     - **Zoneless** : Nouvelle approche expérimentale sans `zone.js` pour la détection des changements. Dans notre cas, on reste sur `No`.
     - **CSS** : Utilisation du CSS classique.
     - **SSR/SSG** : Non nécessaire pour aujourd'hui.

3. Accédez au dossier du projet :
   ```bash
   cd projet_tp
   ```

4. Ouvrez le projet dans un éditeur de code (ex. : VS Code) :
   ```bash
   code .
   ```

---

#### 3. Lancer le projet et comprendre son organisation
**Objectif** : Explorer l’organisation du projet, puis lancer le serveur de developpement.


**Organisation d’un projet Angular** :
fichiers clés dans le projet:
- **`src/`** : Contient le code source de l’application
  - **`app/`** : Contient le composant racine "app" & contient les composants, modules, et services principaux ( c'est ici que vous travaillerez la plupart du temps lors d'un projet Angular )
  - **`assets/`** : Contient les fichiers statiques (images, JSON, etc.)
  - **`index.html`** : Point d’entrée HTML de l’application
  - **`main.ts`** : Point d’entrée TypeScript qui bootstrap l’application
- **`node_modules/`** : Contient les dépendances npm
- **`package.json`** : Liste les dépendances et scripts npm
- **`angular.json`** : Configuration d’Angular CLI (build, serve, etc.)

#### Hello MAAARC si tu lis ça je pensais que l'arborescence des fichiers n'est pas bonne et correspond aux anciennes versions d'Angular.

**Utiliser ng serve** :
 Lancez le serveur de développement en éxécutant dans un terminal depuis la racine du projet :
   ```bash
   ng serve
   ```
   - cliquer sur `http://localhost:4200`.

Dans votre navigateur vous pourrez voir la page de base d'Angular, il s'agit de L'Index.html qui fait appel à app.html ( les composants peuvent appeler d'autres composants dans leur template html ce qui rend Angular très modulaire !).
Si on regarde dans Index.html on peut voir la balise :

```html
  <app-root></app-root>
```
Donc le navigateur charge Index.html qui fais lui même appel au composant principal app, grâce à la directive angular app-root.
Et donc ce que l'on fait dans Angular, c'est qu"à l'intérieur du composant app on fera appel à d'autres composants qui pourront eux même faire appel à d'autres composants etc, etc.!
Vous pouvez maintenant supprimer le contenu de app.html et le remplacer par :
```
<h1> Hello World ! </h1>
```

Et observez le changement dans votre navigateur !

#### 4. Créer votre premier composant (une navbar)
**Objectif** : Créer un composant Angular pour une barre de navigation.

**Étapes** :
1. Générez un composant nommé `navbar` , on peut générer directement des composants  avec Cli Angular :
   ```bash
   ng generate component navbar
   ```
   - Cela va crée un dossier `src/app/navbar` avec les fichiers `navbar.ts`, `navbar.html`, `navbar.css`, et `navbar.spec.ts`.
   - Les composants dans Angular sont tous composés d'un fichier ts qui encapsulent la logique, d'un fichier html, d'un fichier css ( ainsi que d'un fichier .spec.ts que l'on touche rarement ).

2. Modifiez le template de la navbar (`navbar.html` ) :
   - Pour l'instant on laisse toutes les routes à '/ ' on verra plus tard ce point.
   ```html
   <nav class="navbar">
     <h1>Mon Application</h1>
     <ul>
       <li><a href="/">Accueil</a></li>
       <li><a href="/">À propos</a></li>
       <li><a href="/">Contact</a></li>
     </ul>
   </nav>
   ```

3. Ajoutez des styles (`navbar.css`) :
   ```css
   .navbar {
     background-color: #333;
     padding: 1rem;
     color: white;
   }
   ul {
     list-style: none;
     display: flex;
     gap: 1rem;
   }
   a {
     color: white;
     text-decoration: none;
   }
   a:hover {
     text-decoration: underline;
   }
   ```


4. Intégrez la navbar dans le composant racine (`app.html`) :
- Pour savoir quel sera le nom de la balise à utiliser pour appeler navbar depuis d'autre composants il faut regarder dans **navbar.ts** ou l'on peut voir dans le code :

``` typescript
selector: 'app-navbar',
```
On sait maintenant que l'on peut faire appel à la navbar dans app.html comme ceci :
   ```html
   <app-navbar></app-navbar>
   ```

---

#### 5. Créer plusieurs routes en SPA avec le module Router
**Objectif** : Implémenter un système de navigation avec plusieurs pages dans une SPA.

L'idée  ici ça va être d'utiliser la navbar pour naviguer d'une page à l'autre mais sans que le navigateur charge réellement une autre page ( et donc faire vraiment une spa ) pour cela on va utilisé la fonctionnalité Router de Angular.
Ce que l'on va devoir faire c'est avoir un balise dynamique qui charge un composant ou un autre selon l'URL actuel sans recharger complétement la page !
Cette balise dynamique dans Angular c'est celle ci :

```html
<router-outlet></router-outlet>
```
Vous pouvez donc mettre cette balise dans le template app.html !
Cependant pour que cela fonctionne il faut importer le module correspondant dans app.ts
```typescript
import { RouterOutlet } from '@angular/router';
```

Et maintenant ce que l'on doit faire c'est faire comprendre à Angular quel composant charger dans router outlet selon la route.
Commençons par créer des composants à cette fin !

**Étapes** :
1. Générez des composants pour les pages dans le navbar:
   ```bash
   ng generate component home
   ng generate component about
   ng generate component contact
   ```

Pour que Angular sache que l'on veut charger home quand on est dans '/home', about dans '/about' 
Cela passe se passe dans app.routes.ts
2. Configurez le routage dans `app.route.ts` :
  Il faut modifier la variable routes qui associe un chemin à un componsant de tel manière :
   ```typescript
   const routes: Routes = [
     { path: '', component: HomeComponent },
     { path: 'about', component: AboutComponent },
     { path: 'contact', component: ContactComponent },
   ];
   ```
   **Attention on ne met pas le '/ '**

3. Mettez à jour la navbar pour utiliser les routes :
   - C'est presque finis mais pour que cela fonctionne on ne peut pas utiliser le classique href="/..."  qui reloaderais complétement page, on doit à la place utiliser une directive d'Angular :  **routerLink="/..."**. 

    - Pour ce faire il faut importer le module RouterLink dans le fichier navbar.ts :
   ```typescript
    import { RouterLink } from '@angular/router';
   ```
    - Puis s'en servir à la place de href, etmettre les routes que l'on avait renseigner dans app.routes.ts :
   ```html
   <nav class="navbar">
     <h1>Mon Application</h1>
     <ul>
       <li><a routerLink="/">Accueil</a></li>
       <li><a routerLink="/about">À propos</a></li>
       <li><a routerLink="/contact">Contact</a></li>
     </ul>
   </nav>
   ```

Vous pouvez maintenant naviguer entre les trois routes sans reload de la page mais avec seulement un changement du composant à l'intérieur de router outlet ! 

---

#### 6. Utiliser un module Angular pour faire une animation
**Objectif** : Ajouter une animation simple à l’application avec le module `BrowserAnimationsModule`.

**Étapes** :
1. Installez le module d’animations si ce n’est pas déjà fait :
   - Par défaut, il est inclus dans un projet Angular. Vérifiez dans `app.module.ts` :
     ```typescript
     import { BrowserAnimationsModule } from '@angular/platform-browser/animations';

     @NgModule({
       imports: [
         BrowserModule,
         RouterModule.forRoot(routes),
         BrowserAnimationsModule,
       ],
       // ici on aura le reste du fichier, on a choisi de rester succint
     })
     export class AppModule {}
     ```

2. Créez une animation dans le composant `home` (`app.ts`) :
   ```typescript
   import { Component } from '@angular/core';
   import { trigger, state, style, animate, transition } from '@angular/animations';

   @Component({
     selector: 'app-home',
     templateUrl: './home.component.html',
     styleUrls: ['./home.component.css'],
     animations: [
       trigger('fadeIn', [
         state('void', style({ opacity: 0 })),
         transition(':enter', [
           animate('1s ease-in', style({ opacity: 1 })),
         ]),
       ]),
     ],
   })
   export class HomeComponent {}
   ```

3. Appliquez l’animation dans `home.component.html` :
   ```html
   <div @fadeIn>
     <h2>Bienvenue sur la page d'accueil</h2>
     <p> ah ah Regarger la magie s'operer fade-in.</p>
   </div>
   ```

---
