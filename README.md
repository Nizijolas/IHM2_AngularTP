## TP Angular
**Par Marc-Arold Rosemond & Nicolas Dijoud**

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

 
>Ps : à la fin de ce tp pour désinstaller Angular, si vous ne souhaitez pas conserver les paquets sur votre machine :
```bash
    npm uninstall -g @angular/cli
```


---

#### 2. Créer un projet Angular
**Objectif** : Générer un projet Angular avec une configuration adaptée au TP.

**Étapes** :
1. _**Créez un nouveau projet :**_
   ```bash
   ng new projet_tp
   ```
2. _**Répondez aux questions de configuration :**_
   ```bash
   ✔ Do you want to create a 'zoneless' application without zone.js (Developer Preview)? No
   ✔ Which stylesheet format would you like to use? CSS
   ✔ Do you want to enable Server-Side Rendering (SSR) and Static Site Generation (SSG/Prerendering)? No
   ? Which AI tools do you want to configure with Angular best practices? None
   ```
   - **Explication** :
     - **Zoneless** : Nouvelle approche expérimentale sans `zone.js` pour la détection des changements. Dans notre cas, on reste sur `No`.
     - **CSS** : Utilisation du CSS classique.
     - **SSR/SSG** : Non nécessaire pour aujourd'hui.
     - **AI tools** : Pas besoin

> Vous pouvez maintenant ouvrir le dossier `projet_tp` depuis un éditeur de Code

---

#### 3. Lancer le projet et comprendre son organisation
**Objectif** : Explorer l’organisation du projet, puis lancer le serveur de developpement.


**Organisation d’un projet Angular** :
fichiers clés dans le projet:
- **`src/`** : Contient le code source de l’application
  - **`app/`** : Contient le composant racine "app" & contient les composants, modules, et services principaux ( c'est ici que vous travaillerez la plupart du temps lors d'un projet Angular )
  - **`index.html`** : Point d’entrée HTML de l’application
  - **`main.ts`** : Point d’entrée TypeScript qui bootstrap l’application
  - **`angular.json`** : fichier de configuration d'Angular

**Utiliser ng serve** :
 Lancez le serveur de développement en éxécutant dans un terminal depuis la racine du projet :
   ```bash
   ng serve
   ```
   - cliquer sur `http://localhost:4200`.

Dans votre navigateur vous pourrez voir la page de base d'Angular, il s'agit de L'Index.html.
Si on regarde dans Index.html on peut voir la balise :

```html
  <app-root></app-root>
```
Donc le navigateur charge Index.html qui fais lui même appel au composant principal app, grâce à la directive angular app-root.
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
   - Cela va créer un dossier `src/app/navbar` avec les fichiers `navbar.ts`, `navbar.html`, `navbar.css`, et `navbar.spec.ts`.
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
     text-align: center;
   }
   ul {
     list-style: none;
     display: flex;
     justify-content: center;
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

**Attention il est necessaire d'import Navbar dans app.ts, à la fois en haut du fichier et dans l'attribut imports de @Component:**

```ts
  import { Navbar } from "./navbar/navbar";
  @Component({
    ...
    imports: [Navbar],
    ...
  })

```

---

#### 5. Créer plusieurs routes en SPA avec le module Router
**Objectif** : Implémenter un système de navigation avec plusieurs pages dans une SPA.

L'idée  ici ça va être d'utiliser la navbar pour naviguer d'une page à l'autre mais sans que le navigateur charge réellement une autre page ( et donc faire vraiment une spa ) pour cela on va utilisé la fonctionnalité Router de Angular.
Ce que l'on va devoir faire c'est avoir une balise dynamique qui charge un composant ou un autre selon l'URL actuel sans recharger complétement la page !
Cette balise dynamique dans Angular c'est celle ci :

```html
<router-outlet></router-outlet>
```
Vous pouvez donc mettre cette balise dans le template app.html !
Attention encore a bien import le module correspondant dans app.ts (il faut aussi le mettre dans l'attribut imports de @Component).
```typescript
import { RouterOutlet } from '@angular/router';
```

Et maintenant ce que l'on doit faire c'est faire comprendre à Angular quel composant charger dans router outlet selon la route.
Commençons par créer des composants à cette fin !

**Étapes** :
1. _**Générez des composants pour les pages dans le navbar:**_
   ```bash
   ng generate component home
   ng generate component about
   ng generate component contact
   ```

Pour que Angular sache que l'on veut charger home quand on est dans '/home', about dans '/about' 
Cela passe se passe dans app.routes.ts

2. _**Configurez le routage dans `app.route.ts` :**_
  Il faut modifier la variable routes qui associe un chemin à un composant de tel manière :
   ```typescript
   import { Routes } from '@angular/router';
   import { Home } from './home/home';
   import { About } from './about/about';
   import { Contact } from './contact/contact';

    export const routes: Routes = [
    { path: '', component: Home },
    { path: 'about', component: About },
    { path: 'contact', component: Contact },
   ];
   ```
   **Attention on ne met pas le '/ '**

3. _**Mettez à jour la navbar pour utiliser les routes :**_
   - C'est presque finis mais pour que cela fonctionne on ne peut pas utiliser le classique href="/..."  qui reloaderais complétement page, on doit à la place utiliser une directive d'Angular :  **routerLink="/..."**. 

    - Pour ce faire il faut importer le module RouterLink dans le fichier navbar.ts :
   ```typescript
   
    import { RouterLink } from '@angular/router';
   @Component({
     ...
    imports: [RouterLink],
     ...
    })
   ```
    - Puis s'en servir à la place de href, et mettre les routes que l'on avait renseigner dans app.routes.ts :
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

Vous pouvez maintenant naviguer entre les trois routes sans reload de la page mais avec seulement un changement du component à l'intérieur de router outlet ! 


---

#### 6. Bind une propriété du TypeScript au template
**Nous allons ajouter une image dans le component home dont la source sera une variable décrite dans le typescript**

**Étapes** :
1. _**Récupérer l'image 'angular.jpg'**_

Récupérer l'image 'angular.jpg' présente sur ce dépôt github et mettez la dans le dossier 'public' du projet Angular.

2. _**Créer une variable dans home.ts**_

Créons une variable qui correspond à la source de l'image dans le code typescript:

```ts
    sourceImage: string = "angular.jpg";
```

2. _**Modifier home.html et home.css**_

On modifie home.html (on vient bind src à la variable créée en amont).

```html
  <div id="cadreImage">
  <img [src]="sourceImage" alt="">
  </div>
```
On modifie home.css

```css

  #cadreImage{
      width: 400px;
      height: 400px;
      margin: auto;
  }
  #cadreImage > img {
      object-fit: contain;
      width: 100%;
      height: 100%;
  }

```

La directive **[src]** indique que src est bind à du code typescript, donc Angular va aller chercher la variable correspondante dans home.ts, notre image s'affiche bien dans notre navigateur.


