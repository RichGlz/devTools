# Angular con lectura Firebase (Guía rápida)

Basado en la [documentación](https://github.com/angular/angularfire/blob/master/docs/install-and-setup.md) oficial de angularfire.

## 0. Detener la ejecución de tu servidor

Ve a la consola desde donde ejecutas el servidor y presiona la combinación de teclas `ctrl + C` en por lo menos 2 ocasiones.

## 1. Instalar Angularfire y Firebase

El nuevo comando de *Angular CLI* para agregar estos paquetes.

``` shell
ng add @angular/fire
```

> Puedes iniciar el servidor desde este punto con el comando `ng serve -o`, o puedes hacerlo en el paso 5.

## 2. Agregar la configuración en el archivo `environments.ts`

Dentro de `src/environments/environments.ts` :

**Antes:**

``` jsx
...
  export const environment = {
    production: false
  };
...
```


**Después:**

``` jsx
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

## 3. Configurar `@NgModule` para el `AngularFireModule` :

Open `/src/app/app.module.ts`, inyecta los proveedores de Firebase, y especifica tu configuración de Firebase.

**Antes:**

``` jsx
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

``` jsx
import { BrowserModule } from '@angular/platform-browser';
import { NgModule } from '@angular/core';
import { AppComponent } from './app.component';
import { AngularFireModule } from '@angular/fire';
import { AngularFirestoreModule } from '@angular/fire/firestore';
import { AngularFireAnalyticsModule } from '@angular/fire/analytics';
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

## 4. Aplica *Data binding* desde la colección de Firestore a una lista

**TypeScript** - En el componente: `/src/app/app.component.ts` :

**Antes:**

``` jsx
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

``` jsx
import { Component } from '@angular/core';
import { AngularFirestore } from '@angular/fire/firestore';
import { Observable } from 'rxjs';

@Component({
  selector: 'app-root',
  templateUrl: 'app.component.html',
  styleUrls: ['app.component.scss']
})
export class AppComponent {
  // Se declara 'items', que es donde se almacenarán los datos provenientes de la Base de datos.
  items: Observable<any[]>;

  constructor(db: AngularFirestore) {
    // 'items' es el nombre de la colección dentro de la base de datos de Firestore (no confundir con la variable 'this.items').
    this.items = db.collection('items').valueChanges();
  }
}
```

>El nombre de la colección llamada desde la base de datos, en este caso 'items', se puede cambiar según se requiera.

**HTML** - En el componente `/src/app/app.component.html`:

``` html
<ul>
  <li class="text" *ngFor="let item of items | async">
    {{item.name}}
  </li>
</ul>
```

> Si ya tienes instalado **Bootstrap**, puedes agregar esta [plantilla](https://github.com/RichGlz/devTools/blob/main/angular/firebase/plantilla-sencilla/plantilla1.md) a tu proyecto para que se vea mejor.

## 5. Iniciar el servidor

``` shell
ng serve -o
```
