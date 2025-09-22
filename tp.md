## TP Angular
**Par Marc-Arold Rosemond & Nicolas Dijoud**

### Introduction : C’est quoi Angular et TypeScript ?

**Angular** :
- Angular est un framework open-source développé par Google pour créer des applications web modernes, en particulier des **Single Page Applications (SPA)**.
- Il utilise une architecture basée sur des **composants** et offre des fonctionnalités comme le routage, la gestion des formulaires, et les appels HTTP.
- Points forts : structure modulaire, forte intégration avec TypeScript, outils CLI puissants, et prise en charge de la réactivité et des animations.

**TypeScript** :
- TypeScript est un langage similaire à JavaScript qui ajoute des types statiques, des interfaces, et d’autres fonctionnalités pour améliorer la maintenabilité et la robustesse du code. Il ressemble beaucoup, selon nous, à Java
- Avantages : détection des erreurs au moment de la compilation, meilleur support pour les gros projets, et intégration native dans Angular. Nous avons meme lu sur des forums que Angular est beaucoup plus interessant quand le projet commence a grandir.

**Pourquoi Angular + TypeScript ?**
- Angular utilise TypeScript pour structurer le code et faciliter la maintenance.
- TypeScript permet de mieux gérer les erreurs dans les projets complexes,surtout les erreurs de types, ce qui est idéal pour les applications SPA.

**Objectif du TP** :
- Découvrir Angular en créant une petite application SPA avec une navigation, des composants, des animations.
- Comprendre l’organisation d’un projet Angular et les outils associés.

---

### Plan du TP

#### 1. Installer Angular CLI
**Objectif** : Installer l’outil en ligne de commande Angular CLI pour créer et gérer des projets Angular.

**Prérequis** :
- **Node.js** et **npm** doivent être installés sur la machine (version recommandée : Node.js 18.x ou 20.x LTS, npm 8.x ou supérieur). j'ai galere avec l'installation parce que j'avais une version incompatible.
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
   Cela affiche la version d’Angular CLI, Node.js, et d’autres dépendances.


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
     - **CSS** : Format simple pour les styles (alternative : SCSS pour plus de flexibilité).
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
**Objectif** : Lancer l’application Angular par défaut et explorer l’organisation du projet.

**Étapes** :
1. Lancez le serveur de développement :
   ```bash
   ng serve
   ```
   - cliquer sur `http://localhost:4200`.


**Organisation d’un projet Angular** :
fichiers clés dans le projet:
- **`src/`** : Contient le code source de l’application
  - **`app/`** : Contient les composants, modules, et services principaux
    - `app.component.ts` ou `app.ts` : Composant racine de l’application
    - `app.component.html` ou `app.html`: Template HTML du composant racine
    - `app.component.css` ou `app.css`   : Styles CSS du composant racine
    - `app.module.ts` : Module principal qui déclare les composants et importe les modules nécessaires
  - **`assets/`** : Contient les fichiers statiques (images, JSON, etc.)
  - **`index.html`** : Point d’entrée HTML de l’application
  - **`main.ts`** : Point d’entrée TypeScript qui bootstrap l’application
- **`node_modules/`** : Contient les dépendances npm
- **`package.json`** : Liste les dépendances et scripts npm
- **`angular.json`** : Configuration d’Angular CLI (build, serve, etc.)


---

#### 4. Créer votre premier composant (une navbar)
**Objectif** : Créer un composant Angular pour une barre de navigation.

**Étapes** :
1. Générez un composant nommé `navbar` :
   ```bash
   ng generate component navbar
   ```
   - Cela va crée un dossier `src/app/navbar` avec les fichiers `navbar.component.ts`, `.html`, `.css`, et `.spec.ts`.

2. Modifiez le template de la navbar (`src/app/navbar/navbar.component.html` ou `src/app/navbar/navbar.html` ) :
   ```html
   <nav class="navbar">
     <h1>Mon Application</h1>
     <ul>
       <li><a href="/">Accueil</a></li>
       <li><a href="/about">À propos</a></li>
       <li><a href="/contact">Contact</a></li>
     </ul>
   </nav>
   ```

3. Ajoutez des styles (`src/app/navbar/navbar.component.css` ou  `src/app/navbar/navbar.css`) :
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

4. Intégrez la navbar dans le composant racine (`src/app/app.component.html` ou src/app/app.html`) :
   ```html
   <app-navbar></app-navbar>
   <router-outlet></router-outlet>
   ```

---

#### 5. Créer plusieurs routes en SPA avec le module Router
**Objectif** : Implémenter un système de navigation avec plusieurs pages dans une SPA.

**Étapes** :
1. Générez des composants pour les pages dans le navbar:
   ```bash
   ng generate component home
   ng generate component about
   ng generate component contact
   ```

2. Configurez le routage dans `src/app/app.module.ts` :
   ```typescript
   import { NgModule } from '@angular/core';
   import { BrowserModule } from '@angular/platform-browser';
   import { RouterModule, Routes } from '@angular/router';
   import { AppComponent } from './app.component';
   import { NavbarComponent } from './navbar/navbar.component';
   import { HomeComponent } from './home/home.component';
   import { AboutComponent } from './about/about.component';
   import { ContactComponent } from './contact/contact.component';

   const routes: Routes = [
     { path: '', component: HomeComponent },
     { path: 'about', component: AboutComponent },
     { path: 'contact', component: ContactComponent },
   ];

   @NgModule({
     declarations: [
       AppComponent,
       NavbarComponent,
       HomeComponent,
       AboutComponent,
       ContactComponent,
     ],
     imports: [
       BrowserModule,
       RouterModule.forRoot(routes),
     ],
     bootstrap: [AppComponent],
   })
   export class AppModule {}
   ```

3. Mettez à jour la navbar pour utiliser les routes (`src/app/navbar/navbar.component.html` ou `src/app/navbar/navbar.html`) :
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

4. Ajoutez du contenu aux composants :
   - `home.component.html` :
     ```html
     <h2>Bienvenue chez Marc et Nicolas TP</h2>
     ```
   - `about.component.html` :
     ```html

     <h2>À propos de nous</h2>
     <p>Nous sommes des etudiants de M2 DCISS </p>
     ``` 
   - `contact.component.html` :
     ```html
     <h2>Contactez-nous</h2>
     <p>Email : contact@monapp.com</p>
     ```

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

2. Créez une animation dans le composant `home` (`src/app/home/home.component.ts`) :
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
