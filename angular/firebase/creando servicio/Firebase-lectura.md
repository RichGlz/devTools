# Angular con servicio y lectura de IDs en Firebase (Guía rápida)

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

> Sustitúyela con tu propia información desde tu [Consola de firebase](https://console.firebase.google.com/u/0).

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

## 4. Crear el servicio

### 1. Detener el servidor presionando `ctrl + C` en, por lo mejor, dos ocasiones

### 2. Crea un servicio con comando

> Para este se considera usando el comando, aunque también se podría hacer manualmente.

> Se recomienda hacer una carpeta llamada 'services', para mantener más ordenado el código.

``` md
ng g s services/fsConfig
```

> Opcional: Borrar el archivo generado `fs-config.service.spec.ts` *(archivo de pruebas)*.

## 5. Configurar el servicio (sin lectura de IDs)

``` jsx
import { Injectable } from '@angular/core';
import { AngularFirestore, AngularFirestoreCollection } from '@angular/fire/firestore';
import { Observable } from 'rxjs';
/* //Activar para la clase map para Lecturas de IDs
import { map } from 'rxjs/operators'; */

export interface Item { name: string; }

@Injectable({
  providedIn: 'root'
})
export class FsConfigService {

  /* //Activar para la clase map para Lecturas de IDs
  private itemsCollection: AngularFirestoreCollection<Item>; */

  items: Observable<Item[]>;

  // ----- Constructor SIN lectura de IDs -----
  constructor(private db: AngularFirestore) {
    this.itemsCollection = db.collection<Item>('items');
    this.items = this.itemsCollection.valueChanges();
  }

  /*
  // ----- Constructor CON lectura de IDs -----

  constructor(private db: AngularFirestore) {
    this.itemsCollection = db.collection<Item>('items');
    this.items = this.itemsCollection.snapshotChanges().pipe(
      map(actions => actions.map(a => {
        const data = a.payload.doc.data() as Item;
        const id = a.payload.doc.id;
        return { id, ...data };
      }))
    );
  }
  */

  getItems(): any {
    return this.items;
  }
}
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
import { FsConfigService } from './services/fs-config.service';

@Component({
  selector: 'app-root',
  templateUrl: './app.component.html',
  styleUrls: ['./app.component.scss']
})
export class AppComponent {
  title = 'AnguFirestore';
  version = 'v2.0';
  items: any;

  constructor(private config: FsConfigService){
    this.config.getItems().subscribe( item => {
      this.items = item;
      console.log(this.items);
    });
  }
}
```

>En este caso, el nombre de la colección en la base de datos es 'items'.

**HTML** - En el componente `/src/app/app.component.html`:

``` html
<ul>
  <li
    *ngFor="let item of items"
    class="text">

    <!-- Descomente para lectura de IDs -->
    <!-- {{ item.id }} - -->

    {{item.name}}
  </li>
</ul>
```

> Si ya tienes instalado **Bootstrap**, puedes agregar esta [plantilla](https://github.com/RichGlz/devTools/blob/main/angular/firebase/plantilla-sencilla/plantilla1.md) a tu proyecto para que se vea mejor 👌🏻.

## 5. Iniciar el servidor

``` shell
ng serve -o
```

# Nota final - Datos en Cloud FireStore

Recuerda que la estructura en [**Cloud FireStore**](https://console.firebase.google.com/u/0) debe ser de la forma:

``` vim
┌/
└┬'items'
 └┬<ID-de-documento>
  └┬'name'
   └<valor>
```

> Puede leer otros datos aparte de 'name' agregándolos al HTML (al final del paso 4.), por ejemplo:

```  vim
En FireStore:

  ┌/
  └┬'items'
   └┬<ID-de-documento> //Puede ser autogenerado.
    ├─┬'name'
    │ └─<valor>
    └─┬'edad'
      └<valor>

```

``` HTML
En el HTML:

  {{item.name}} - {{item.edad}}
```
