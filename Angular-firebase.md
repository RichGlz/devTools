# Angular con lectura Firebase (Guía rápida)

Basado en la [documentación](https://github.com/angular/angularfire/blob/master/docs/install-and-setup.md) oficial de angularfire.

## 1. Crear un nuevo proyecto:

  **En Windows:**

  1. Vaya a la carpeta donde creará el proyecto.
  2. Presione `shift + clic derecho`
  3. Seleccione ` Abrir la ventana de PowerShell aquí `

## 2. En el PowerShell

``` shell
npm install -g @angular/cli
ng new <nombre-del-proyecto>
cd <nombre del proyecto>
```

> En cuanto a **estilos** prefiero utilizar *SCSS*; es similar a *CSS* pero con más opciones. 👌🏻

## 3. Instalar Angularfire y Firebase

El nuevo comando de *Angular CLI* para agregar estos paquetes.

``` shell
ng add @angular/fire
```

## 4. Instalar Bootstrap

El nuevo comando de *Angular CLI* para agregar estos paquetes.

``` shell
npm i jquery bootstrap @popperjs/core --save
```

### 4.1 Instalar boostrap `angular.json`

**Antes:**

``` ts
...
  "styles": [
  "src/styles.scss"
  ],
  "scripts": []
...
```

**Después:**

``` ts
...
  "styles": [
  "src/styles.scss",
  "./node_modules/bootstrap/dist/css/bootstrap.min.css"
  ],
  "scripts": [
    "./node_modules/jquery/dist/jquery.slim.min.js",
    "./node_modules/bootstrap/dist/js/bootstrap.min.js",
    "./node_modules/popper.js/dist/umd/popper.min.js"
  ]
...
```

## 5. Agregar la configuración en el archivo `environments.ts`

Dentro de `src/environments/environments.ts` :

**Antes:**

``` ts
...
  export const environment = {
    production: false
  };
...
```


**Después:**

``` ts
...
  export const environment = {
    production: false,
    config: {
      apiKey: '...',
      authDomain: '...',
      databaseURL: '...',
      projectId: '...',
      storageBucket: '...',
      messagingSenderId: '...',
      appId: '...',
    }
  };
...
```

> Sustitúyela con tu propia información desde la [Consola de firebase](https://console.firebase.google.com/u/0).

## 6. Configurar `@NgModule` para el `AngularFireModule` :

Open `/src/app/app.module.ts`, inyecta los proveedores de Firebase, y especifica tu configuración de Firebase.

**Antes:**

``` ts
import { BrowserModule } from '@angular/platform-browser';
import { NgModule } from '@angular/core';
import { AppComponent } from './app.component';

@NgModule({
  imports: [
    BrowserModule
  ],
  declarations: [ AppComponent ],
  bootstrap: [ AppComponent ]
})
export class AppModule {}
```

**Después:**

``` ts
import { BrowserModule } from '@angular/platform-browser';
import { NgModule } from '@angular/core';
import { AppComponent } from './app.component';
import { AngularFireModule } from '@angular/fire';
import { environment } from '../environments/environment';

@NgModule({
  imports: [
    BrowserModule,
    AngularFireModule.initializeApp(environment.config),
    AngularFireAnalyticsModule,
    AngularFirestoreModule
  ],
  declarations: [ AppComponent ],
  bootstrap: [ AppComponent ]
})
export class AppModule {}
```

## 7. Aplica *Data binding* desde la colección de Firestore a una lista

**TypeScript** - En el componente: `/src/app/app.component.ts` :

**Antes:**

``` ts
import { Component } from '@angular/core';

@Component({
  selector: 'app-root',
  templateUrl: 'app.component.html',
  styleUrls: ['app.component.scss']
})
export class AppComponent {
  title: 'nombre-de-la-app'
}
```

**Después:**

``` ts
import { Component } from '@angular/core';
import { AngularFirestore } from '@angular/fire/firestore';
import { Observable } from 'rxjs';

@Component({
  selector: 'app-root',
  templateUrl: 'app.component.html',
  styleUrls: ['app.component.scss']
})
export class AppComponent {
  items: Observable<any[]>;
  constructor(db: AngularFirestore) {
    this.items = db.collection('items').valueChanges();
  }
}
```

**HTML** - En el componente `/src/app/app.component.html`:

``` html
<ul>
  <li class="text" *ngFor="let item of items | async">
    {{item.name}}
  </li>
</ul>
```

>También puedes descargar esta [plantilla HTML](https://github.com/RichGlz/AnguBase-project/blob/master/src/app/app.component.html) con **Bootstrap** para que se vea mejor tu proyecto.

## 8. Ejecuta el servidor:

``` shell
ng serve
```
