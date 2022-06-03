1. Create project / project id


2. Deveolop -> Authentication -> Sign-in method -> Google ->

3. Project Overview -> select your project -> Add an app to get started, select web ->
past the firebase config into  /src/environment/environment.ts


## Front end

```
  npm i @angular/fire firebase
```

```
import { AngularFireModule } from '@angular/fire';
import { AngularFireAuthModule } from '@angular/fire/auth';
import { environment } from '../environments/environment';

imports: [
  AngularFireModule.initializeApp(environment.firebase),
  AngularFireAuthModule,
],

```



## Back end
Project-> Service accounts ->  generate prievate key to credentials.json

```
  npm i firebase-admin
```

server.js
```
import * as admin from 'firebase-admin';
import credentials from '../credentials.json';

admin.initializeApp({
    credential: admin.credential.cert(credentials),
});

```