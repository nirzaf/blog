---
title: "Building an Angular Project With Bootstrap 4 and Firebase"
date: 2019-10-18T12:51:54+05:30
draft: false
tags : ["angular"]
---

!["Angular App With Firebase"](https://res.cloudinary.com/dw0ygv1p9/image/upload/v1571642424/1_ocLdKFc0yd5cIZz_oIP_hg_zgvgef.png)

This post has been published first on <a href="https://https://codingthesmartway.com/">CodingTheSmartWay.com.</a>

### Part 1: Setting Up The Project

In this tutorial I’ll show you how to start your Angular 5 Project from scratch and add Bootstrap 4 and the Firebase library to your application. This is the perfect application skeleton for your web application project.

{{< youtube 5gT0-9vifuc >}}

### Setting Up The Angular Project

First we need to setup an Angular project. This is done by using Angular CLI (https://cli.angular.io/). If you have not installed Angular CLI on your system first make sure that the command line interface is installed by executing the following command:

`$ npm install -g @angular/cli@latest`

Having installed Angular CLI you can now make use of the ng command. By using this command we’re able to initiate a new Angular project:

`$ ng new ng4fbbootstrap --skip-install`

To initiate a new project we need to use the command line parameter new and specify the name of the new project. Furthermore the option --skip-install is used to avoid that NPM dependencies are installed automatically. This is needed because Angular 5 should be used for our application. At the time of writing Angular 5 is not released yet and only available as a Release Candidate version, so that we have to update our package.json file first.

<p>Change into the newly created project folder:</p>

`$ cd ng4fbbootstrap`
<p>Open package.json in your code editor and make sure to update the version information for all Angular packages in the dependencies and devDependencies section to the latest version (e.g. ^5.0.0-rc.1). Furthermore make sure that the version of the typescript package in the devDependencies section is set to version ~2.4.1 as well. The relevant part of package.json should now look like the following:</p>

{{< highlight typescript>}}
"dependencies": {
    "@angular/animations": "^5.0.0-rc.1",
    "@angular/common": "^5.0.0-rc.1",
    "@angular/compiler": "^5.0.0-rc.1",
    "@angular/core": "^5.0.0-rc.1",
    "@angular/forms": "^5.0.0-rc.1",
    "@angular/http": "^5.0.0-rc.1",
    "@angular/platform-browser": "^5.0.0-rc.1",
    "@angular/platform-browser-dynamic": "^5.0.0-rc.1",
    "@angular/router": "^5.0.0-rc.1",
    "@ng-bootstrap/ng-bootstrap": "^1.0.0-beta.5",
    "angularfire2": "^5.0.0-rc.2",
    "bootstrap": "^4.0.0-beta",
    "core-js": "^2.4.1",
    "firebase": "^4.4.0",
    "jquery": "^3.2.1",
    "popper.js": "^1.12.5",
    "rxjs": "^5.4.2",
    "zone.js": "^0.8.14"
  },
  "devDependencies": {
    "@angular/cli": "^1.5.0-beta.4",
    "@angular/compiler-cli": "^5.0.0-rc.1",
    "@angular/language-service": "^5.0.0-rc.1",
    "typescript": "~2.4.1"
  }
{{< /highlight >}}
Execute the package installation via
`$ npm install`

Note: Once the final release of Angular 5 is available you can skip the step of manually updating packaging.json and executing the package installation as an additional step. You can then use `ng new ng4fbbootstrap` to create a new project (dependencies are installed automatically).

In the project folder you can execute the following command to launch the development web server:

`$ ng serve`

The server is started and the application can be accessed on http://localhost:4200 as you can see in the following screenshot:

!["Angular Initial Project"](https://res.cloudinary.com/dw0ygv1p9/image/upload/v1571643329/0_4M8XkLRUw5w5pFno_skifc2.png)

### Setting up Firebase

Next step is to include the Firebase in our project. Two steps are needed here:
<ul>
<li>First, a new Firebase project has to be created in the Firebase back-end and the corresponding project settings have to be made available within the Angular application</li>
<li>Second, the Firebase and AngularFire2 libraries have to be added to the project</li>
</ul>

### Creating A Firebase Project

To create a new Firebase project go to the Firebase website https://firebase.google.com and create a new account / sign in with your Google credentials. After you’re being logged in successfully you can click on the link Go To Console to access the Firebase back-end:

!["firebase console"](https://res.cloudinary.com/dw0ygv1p9/image/upload/v1571643484/0_zm1HADJJQ0WSeU1v_rgsxdg.png)

Here you can click on Add project to add a new Firebase project or select one of the existing projects. You’re taken to the project console next:

!["firebase"](https://res.cloudinary.com/dw0ygv1p9/image/upload/v1571643554/0_ygF0hbDRLFfeixF6_gvqinv.png)

Click on the link Add Firebase to your web app to access the following dialog:

!["firebase"](https://res.cloudinary.com/dw0ygv1p9/image/upload/v1571643616/0_uFrkSuE9BqR_KP8c_kjjqm1.png)

Here you can find the JavaScript code which is needed to initialize the Firebase project for your website. However, to include this Firebase configuration in the Angular project we do only need a part of that code snippet. Copy the key-value pairs inside the config object and insert those pairs inside the file `environments/environment.ts` in the following way:

{{< highlight typescript>}}
export const environment = {
  production: false,
  firebase: {
    apiKey: "[...]",
    authDomain: "[...]",
    databaseURL: "[...]",
    projectId: "[...]",
    storageBucket: "[...]",
    messagingSenderId: "[...]"
  }
};
{{</ highlight >}}


The key-value pairs are inserted into a new property named firebase. The same needs to be inserted into `environments/environment.prod.ts:`

{{< highlight typescript>}}
export const environment = {
  production: true,
  firebase: {
    apiKey: "[...]",
    authDomain: "[...]",
    databaseURL: "[...]",
    projectId: "[...]",
    storageBucket: "[...]",
    messagingSenderId: "[...]"
  }
};
{{< /highlight>}}

That’s needed to make the Firebase settings available whether we’re building during development or for production.

### Adding Libraries

Next, let’s add the libraries to our project by executing the following command:

`$ npm install --save firebase@^4.4.0 angularfire2@^5.0.0-rc.2`

That command is downloading and installing both packages, `firebase` and `angularfire2`, into the node_modules folders and adding the dependencies to the package.json file.

Insert the following import statements into `app.module.ts`:

{{< highlight typescript>}}
import { AngularFireModule } from 'angularfire2';
import { AngularFireDatabaseModule } from 'angularfire2/database';
import { AngularFireAuthModule } from 'angularfire2/auth';
{{< /highlight>}}

Also add the modules AngularFireModule, AngularFireDatabaseModule, and AngularFireAuthModule to the imports aray of the @NgModule decorator in the following way:

{{< highlight typescript>}}
@NgModule({
  declarations: [
    AppComponent,
    AppNavbarComponent
  ],
  imports: [
    BrowserModule,
    AngularFireModule.initializeApp(environment.firebase),
    AngularFireDatabaseModule,
    AngularFireAuthModule
  ],
  providers: [],
  bootstrap: [AppComponent]
})
export class AppModule { }
{{< /highlight>}}

Please note, that for module AngularFireModule the method initilizeApp is called and that the Firebase configuration (available via environment.firebase) is passed into that method. To gain access to the environment object you need to add the following import statement as well:

`import { environment } from './../environments/environment';`

### Adding Bootstrap 4

Let’s add the Bootstrap 4 library to our project by using NPM again:

`$ npm install --save bootstrap@next`

We need to add @next to the package name because at the time of writing this post Bootstrap 4 is still in beta. The @next addition makes sure that version 4 of Bootstrap is installed, not version 3.
<p>

The NPM command installs Bootstrap 4 into the folder `node_modules/bootstrap` and at the same time makes sure that the dependency is added into the package.json file.</p>
<p>
To make the Bootstrap CSS classes available for the components in our project we need to include the Bootstrap CSS file from `node_modules/bootstrap/dist/css/bootstrap.css` in our project. To do so add the following line in file styles.css:

`@import "~bootstrap/dist/css/bootstrap.css"`
</p>
<p>

</p>
<p></p>
<p></p>






