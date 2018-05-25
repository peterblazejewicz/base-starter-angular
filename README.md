# Base Starter for Vaadin components with Angular

## Instructions

### Install all dependencies

Run `yarn install` to install all the necessary dependencies. After this you can run the development server.

### Development server

Run `ng serve` for a dev server. Navigate to `http://localhost:4200/`. The app will automatically reload if you change any of the source files.

### Code scaffolding

Run `ng generate component component-name` to generate a new component. You can also use `ng generate directive|pipe|service|class|guard|interface|enum|module`.

### Build

Run `ng build` to build the project. The build artifacts will be stored in the `dist/` directory. Use the `-prod` flag for a production build.

### Running unit tests

Run `ng test` to execute the unit tests via [Karma](https://karma-runner.github.io).

### Running end-to-end tests

Run `ng e2e` to execute the end-to-end tests via [Protractor](http://www.protractortest.org/).

### Further help

To get more help on the Angular CLI use `ng help` or go check out the [Angular CLI README](https://github.com/angular/angular-cli/blob/master/README.md).


## Recreating this project

This project was generated with [Angular CLI](https://github.com/angular/angular-cli) version 1.6.5 with additional steps to include Vaadin components. You can recreate the project by following along these steps:

First [install yarn](https://yarnpkg.com/lang/en/docs/install)

``` bash
$ yarn install -g @angular/cli
$ ng new hello-angular
$ cd hello-angular

# We will use a third-party helper library https://github.com/hotforfeature/origami
$ yarn install --save @codebakery/origami

$ yarn install --save @polymer/polymer@next
$ yarn install --save @vaadin/vaadin-button
$ yarn install --save @vaadin/vaadin-text-field
$ yarn i --save @webcomponents/webcomponentsjs@latest
```

Open `src/main.ts`
  In the `import` section, add:
``` typescript
import { webcomponentsReady } from '@codebakery/origami';
```
	Wrap `platformBrowserDynamic` code with:
``` typescript
webcomponentsReady().then(() => {
  platformBrowserDynamic().bootstrapModule(AppModule)
    .catch(err => console.log(err));
}).catch(error => {
  // No WebComponent support and webcomponentsjs is not loaded
  console.error(error);
});
```

Open `src/polyfills.ts` and add webcomponents import in the end of the file:
``` typescript
import '@webcomponents/webcomponentsjs/bundles/webcomponents-sd-ce.js';
```

Open `src/app/app.module.ts`
	Update the `import` section:
``` typescript
import { NgModule, CUSTOM_ELEMENTS_SCHEMA } from '@angular/core';
import { PolymerModule } from '@codebakery/origami';
```
  Inside the `@NgModule` definition, add:
``` typescript
schemas: [CUSTOM_ELEMENTS_SCHEMA],
```
  Inside the `@NgModule` definition, add this to the `imports` array:
``` typescript
PolymerModule.forRoot(),
```

Open `src/app/app.component.html` and replace all the HTML code with:
``` html
<vaadin-text-field #textField placeholder="Type Something"></vaadin-text-field>
<vaadin-button (click)='title=textField.value'>Click Me!</vaadin-button>
<h2>Hello {{title}}!</h2>
```

Open `src/app/app.component.ts` and in the `import` section, add:
``` typescript
import '@vaadin/vaadin-button/vaadin-button.js';
import '@vaadin/vaadin-text-field/vaadin-text-field.js';
```

