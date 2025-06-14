# ngx-slick-carousel

[![npm version](https://badge.fury.io/js/ngx-slick-carousel.svg)](https://badge.fury.io/js/ngx-slick-carousel)
[![Build Status](https://travis-ci.com/leo6104/ngx-slick-carousel.svg?branch=master)](https://travis-ci.com/leo6104/ngx-slick-carousel)

1. Support Angular 17 (not compatible with <= 16, if you want, use 15.0.0 release)
2. Support Server side rendering
3. Support Re-initialize case
4. Fastest slick init/unslick implementation in Angular

## Installation

To install this library, run:

```bash
$ npm install jquery @types/jquery --save
$ npm install ngx-slick-carousel-ver2 --save
```

## Consuming your library

Once you have published your library to npm, you can import your library in any Angular application by running:

```bash
$ npm install ngx-slick-carousel-ver2 --save
```

and then from your Angular standalone component:

```typescript
import { Component } from '@angular/core';

// Import your library
import { SlickCarouselModule } from 'ngx-slick-carousel-ver2';

@Component({
  ...,
  standalone: false,
  imports: [
    SlickCarouselModule, // Put in here
  ],
})
export class ExampleComponent {
  ...
}
```

- Include slick css in "styles" at your `angular.json` file  :
```
  "styles": [
    ...
    "node_modules/ngx-slick-carousel-ver2/slick/slick.scss",
    "node_modules/ngx-slick-carousel/slick-ver2/slick-theme.scss",
    ...
  ]
```

- Include jquery and slick js in "scripts" at your `angular.json` file  :
```
  "scripts": [
    ...
    "node_modules/jquery/dist/jquery.min.js",
    "node_modules/ngx-slick-carousel-ver2/slick/slick.min.js",
    ...
  ]
```

Once your library is imported, you can use its components, directives and pipes in your Angular application:
```html
  <!-- You can now use your library component in app.component.html -->
    <ngx-slick-carousel class="carousel" 
                        #slickModal="slick-carousel" 
                        [config]="slideConfig" 
                        (init)="slickInit($event)"
                        (breakpoint)="breakpoint($event)"
                        (afterChange)="afterChange($event)"
                        (beforeChange)="beforeChange($event)">
        @for (slide of slides; track slide.img) {
            <div ngxSlickItem class="slide">
                  <img src="{{ slide.img }}" alt="" width="100%">
            </div>
        }
    </ngx-slick-carousel>
    
    <button (click)="addSlide()">Add</button>
    <button (click)="removeSlide()">Remove</button>
    <button (click)="slickModal.slickGoTo(2)">slickGoto 2</button>
    <button (click)="slickModal.unslick()">unslick</button>
```

```typescript
@Component({
  ...,
  standalone: true,
  imports: [
    SlickCarouselModule, 
  ],
})
class ExampleComponent {
  slides = [
    {img: "http://placehold.it/350x150/000000"},
    {img: "http://placehold.it/350x150/111111"},
    {img: "http://placehold.it/350x150/333333"},
    {img: "http://placehold.it/350x150/666666"}
  ];
  slideConfig = {"slidesToShow": 4, "slidesToScroll": 4};
  
  addSlide() {
    this.slides.push({img: "http://placehold.it/350x150/777777"})
  }
  
  removeSlide() {
    this.slides.length = this.slides.length - 1;
  }
  
  slickInit(e) {
    console.log('slick initialized');
  }
  
  breakpoint(e) {
    console.log('breakpoint');
  }
  
  afterChange(e) {
    console.log('afterChange');
  }
  
  beforeChange(e) {
    console.log('beforeChange');
  }
}
```

**(IMPORTANT)** If `slides` variable will be changed dynamically, use `trackBy` in `*ngFor` syntax. It will minimize `ngxSlickItem` directive recreation.

## Development

To generate all `*.js`, `*.d.ts` and `*.metadata.json` files:

```bash
$ npm run build
```

To lint all `*.ts` files:

```bash
$ npm run lint
```

## License

MIT © [leo6104](mailto:heo@mpaghq.com)
