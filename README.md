# AngularCommunication2

## Comunicación a través del componente padre.
Se puede usar cuando es fácil controlar el estado compartido entre los componentes a través de su componente principal y no parece que desee crear un nuevo servicio o crear un código repetitivo, debido a una variable.
La implementación de este enfoque es casi la misma que la anterior, sin embargo, la barra lateral no recibe el componente de la barra lateral. En su lugar, el componente principal contiene la propiedad sideBarIsOpened que se pasa al componente de la barra lateral.

### app.component.html
```html
app component

<app-side-bar-toggle (toggle)="toggleSideBar()"></app-side-bar-toggle>
<app-side-bar [isOpen]="sideBarIsOpened"></app-side-bar>
```
### app.component.ts
```typescript
@Component({
  selector: 'my-app',
  templateUrl: './app.component.html',
  styleUrls: [ './app.component.css' ]
})
export class AppComponent {
  sideBarIsOpened = false;

  toggleSideBar(shouldOpen: boolean) {
    this.sideBarIsOpened = !this.sideBarIsOpened;
  }
}
```
### side-bar-toggle.component.ts
```typescript
@Component({
  selector: 'app-side-bar-toggle',
  templateUrl: './side-bar-toggle.component.html',
  styleUrls: ['./side-bar-toggle.component.css']
})
export class SideBarToggleComponent {

  @Output() toggle: EventEmitter<null> = new EventEmitter();

  @HostListener('click')
  click() {
    this.toggle.emit();
  }

}
```
### side-bar.component.ts
```typescript
@Component({
  selector: 'app-side-bar',
  templateUrl: './side-bar.component.html',
  styleUrls: ['./side-bar.component.css']
})
export class SideBarComponent {

  @HostBinding('class.is-open') @Input()
  isOpen = false;

}
```
Este proyecto se generó con [Angular CLI] (https://github.com/angular/angular-cli) versión 1.3.0.

## Development server

Ejecute `ng serve` para un servidor dev. Vaya a `http://localhost:4200/`. La aplicación se volverá a cargar automáticamente si cambia alguno de los archivos de origen.

## Code scaffolding

Ejecute `ng generar componente nombre-componente` para generar un nuevo componente. También puede usar`ng generate directive|pipe|service|class|guard|interface|enum|module`.

## Build

Ejecuta `ng build` para construir el proyecto. Los artefactos de compilación se almacenarán en el directorio `dist /`. Use la bandera `-prod` para una compilación de producción.

## Running unit tests

Ejecute `ng test` para ejecutar las pruebas unitarias a través de [Karma] (https://karma-runner.github.io).

## Running end-to-end tests

Ejecute `ng e2e` para ejecutar las pruebas de extremo a extremo a través de [Protractor] (http://www.protractortest.org/).
Antes de ejecutar las pruebas, asegúrese de que está sirviendo la aplicación a través de `ng serve`.

## Further help

Para obtener más ayuda sobre Angular CLI, use `ng help` o visite el [Angular CLI README] (https://github.com/angular/angular-cli/blob/master/README.md).
