## QuickStart


## 1. Server : create new Model
```
cd server
lb model ...
```

## 2. Client : create Api-client

 Api-client allow request server loopback API
 Api-client is generate via [Fireloop] commande line.

```
> npm run fireloop

? What do you want to do?
> Generate Angular2 SDK

? For which application do you want to build an SDK?
> webapp

? What SDK features do you want to include?
 ◉ Generate ONLY FireLoop SDK + Auth Services
 ◉ Enable NGRX functionality

? In what directory should the SDK be created? (webapp/src/app/shared/sdk) 
 > enter
...
... loopbackSDK Builder
...
Enjoy!!!

>
```

## 3. Client : create new UI
 * Create new Service from you model : ```src/app/services/mymodel.service.ts```
 
    ```
    constructor(
        private mymodelApi: MyModelApi
      ) 
    ```

 * Create new component
 
  ```cd src/app/components/myapp && ng generate component MyComponent```
  
 * Create route for new component
 
Add section on ```src/app/app.routing.module.ts```
```
{
    path: 'mymodels', // path of this route
    component: MyComponent, // component call 
    canActivate: [AdminGuard],  // roles restriction options [AdminGuard, AgentGuard, AuthGuard]
    data: {
      title: { en: 'Label', fr: 'Libellé' },
    },
  },
```


## 4. Client Samples
 * Component List ( with datasources, tests) 
 
    ```src/app/components/federal/cities```
    
 * Component Form
 
    ```src/app/components/federal/city```

[FireLoop]: http://fireloop.io