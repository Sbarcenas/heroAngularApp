#Notas de Angular:

## Obtener datos por medio de RxJs Observable

Al obtener datos por medio de un servicio, desde una base de datos cualquiera, por http, devuelven
RxJs Observables. y esto se puede simular con la of() funcion.

Para esto, import { Observable, of } from 'rxjs'; se importan los elementos.
y la función por la cual recuperamos los datos de la consulta http se veria de la siguiente forma:

getHeroes(): Observable<Hero[]> {
  return of(HEROES);
}

## Leer datos de un servicio

Para leer datos RxJs Observable, utilizamos la función, que declaramos para esto:
getHeroes(): void {
  this.heroService.getHeroes()
      .subscribe(heroes => this.heroes = heroes);
}
--> Concatenamos la funcion subscribe que recibe como argumento un parametro que esperamos recibir,
y luego dentro del cuerpo de la funcion asignamos, ese parametro a nuestro campo deseado en la clase de lectura.


## Rutas en Angular

Dato curioso de las rutas en Angular:

Es buena practica crear un enrutador separado de todo, y esto es un modulo con en comando

´´´
ng generate module app-routing --flat --module=app
´´´
y reemplazamos el contenido de ese archivo por esto:


´´´
import { NgModule } from '@angular/core';
import { RouterModule, Routes } from '@angular/router';
import { HeroesComponent } from './heroes/heroes.component';
 
const routes: Routes = [
  { path: 'heroes', component: HeroesComponent }
];
 
@NgModule({
  imports: [RouterModule.forRoot(routes)],
  exports: [RouterModule]
})
export class AppRoutingModule { }
´´´
### <router-outlet></router-outlet> 
En el html que va a cargar las vistas colocamos:
en vez de las rutas a lo componentes como etiquetas.<router-outlet></router-outlet>
Una buena practica es redireccionar a una ruta desde tu app-routin-module.ts

Ejmeplo:

´´´
<nav>
        <a routerLink="/heroes">Heroes</a>// Esta cabecera siempre aparece
</nav>

<router-outlet></router-outlet>  // Esto lo reemplaza la ruta 


<app-messages></app-messages>// Este Footer siempre aparece
´´´

Este es un redirect a un view = { path: '', redirectTo: '/dashboard', pathMatch: 'full' },

Por aquí quedamos.https://angular.io/tutorial/toh-pt5#routable-herodetailcomponent


## Trabajar con rutas que traen paramtros variables

Para esto necesitamos importar:
import { ActivatedRoute } from '@angular/router';
Que guarda los datos de la url.

import { Location } from '@angular/common';

Location es un servicio para interactuar con el navegador.



## Obtener datos de la url 
Algo mas de sintaxis (+) Delante de una variable convierte en numero el elemento.

´´´
getHero(): void {
  const id = +this.route.snapshot.paramMap.get('id'); --> En esta instrucción  de tipo ActivatedRoute.snapshot-> Traemos un foto de la url.
  this.heroService.getHero(id)
    .subscribe(hero => this.hero = hero);
}
´´´

##Leer datos Https

importamos para nuestro app.module.ts el httpClientModule

import { HttpClientModule }    from '@angular/common/http';

Agregamos el import 

@NgModule({
  imports: [
    HttpClientModule,
  ],
})


### Leer de un cliente Http en un componentes/Servicio

1. Importamos:
import { HttpClient, HttpHeaders } from '@angular/common/http';

2.
Creacemos variables donde almacenar Url de los elementos que vamos a obtener de la api.

3. obtenemos datos con el metodo this.http.get<dtaTipe>(url) que previamente debimos haber injectado

## Manejo de errores Http
