# Angular with GoogleMaps integration. Show a SimpleMap.

Here's an Angular application that integrates the provided TypeScript code to show a simple Google Maps:

1.Create a new Angular blank application.
```
ng new googlemaps_simplemap
```

2.Install the required dependencies:
```
npm install @types/googlemaps
```

3.Create a new Angular component. Let's call it MapComponent:
ng generate component Map

4.Open the generated map.component.ts file and replace the content with the following code:
```typescript
import { Component, OnInit } from '@angular/core';

declare var google: any;

@Component({
  selector: 'app-map',
  template: `
    <div id="map" style="width: 100%; height: 400px;"></div>
  `,
  styles: [`
    #map {
      height: 100%;
    }
  `]
})
export class MapComponent implements OnInit {
  ngOnInit() {
    this.initMap();
  }

  async initMap(): Promise<void> {
    const { Map } = await google.maps.importLibrary("maps") as google.maps.MapsLibrary;
    const map = new Map(document.getElementById("map"), {
      center: { lat: -34.397, lng: 150.644 },
      zoom: 8,
    });
  }
}
```

5.Open the app.module.ts file and import the MapComponent:
```typescript
import { NgModule } from '@angular/core';
import { BrowserModule } from '@angular/platform-browser';

import { AppComponent } from './app.component';
import { MapComponent } from './map/map.component';

@NgModule({
  declarations: [
    AppComponent,
    MapComponent
  ],
  imports: [
    BrowserModule
  ],
  providers: [],
  bootstrap: [AppComponent]
})
export class AppModule { }
```

6.Open the app.component.html file and add the <app-map></app-map> tag:
```html
<h1>My Angular App</h1>
<app-map></app-map>
```

7.Open the tsconfig.app.json file in the root directory of your Angular project.
Add "node_modules/@types" to the "types" array. Your tsconfig.app.json file should look like this:
```json
{
  "extends": "./tsconfig.json",
  "compilerOptions": {
    "outDir": "./out-tsc/app",
    "types": [
      "node",
      "googlemaps"
    ]
  },
  "files": [
    "src/main.ts",
    "src/polyfills.ts"
  ],
  "include": [
    "src/**/*.d.ts"
  ]
}
```


