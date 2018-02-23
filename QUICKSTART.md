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

## 5. Datasources

 Datasource is mandatory for displaying List of items via Table.

> A DataSource provides data to the table by emitting an Observable stream of the items to be rendered. Each emit includes the entire set of items that should be displayed. The table, listening to this stream, will render a row per item. Any manipulation of the data being displayed (e.g. sorting, pagination, filtering) should be captured by the DataSource, ultimately emitting a new set of items to reflect any changes.

 You can use your generic datasource that facilitate gestion of filters, pagination, sort and nbItems.

 
 ```ts
 export class CityDataSource extends MatTableDataSource<City, CityCriteria> {
 
   /**
    * Inject Service
    * @param {CityService} cityService
    */
   constructor(
     private cityService: CityService,
   ) {
     super();
   }
 
   /**
    * Abstract Method that return Array of Items
    * @param {LoopBackFilter} pageFilter
    * @returns {Observable<City[]>}
    */
   protected getData(pageFilter: LoopBackFilter): Observable<City[]> {
     return this.cityService.getCities(pageFilter);
   }
 
   /**
    * Abstract Method that return total number of Items 
    * @param {CityCriteria} criteria
    * @returns {Observable<number>}
    */
   protected countData(criteria: CityCriteria): Observable<number> {
     return this.cityService.countCities(criteria);
   }
 
 }
 
 
 export interface CityCriteria {
   code?: string;
   postalCode?: string;
   name?: string;
 }
 ```
 
 Utilisation datasource on component list 
 
 ```ts 
 @Component({
   ...
   providers: [CityDataSource],
 })
 export class MyComponent implements OnInit {
 
   private _criteria: CityCriteria;
   ...
   @ViewChild(MatPaginator) paginator: MatPaginator;
   @ViewChild(MatSort) sorter: MatSort;
   ...
   constructor(
     public dataSource: CityDataSource,
   ) {
   }
 
   ...
   get totalElements() {
     return this.dataSource.totalElements;
   }
 
   set criteria(value: CityCriteria) {
     this._criteria = value;
     this.dataSource.changeCriteria(this.criteria);
   }
 
   ngOnInit(): void {
     this.dataSource.init(this.paginator, this.sorter, this.criteria);
   }
 
   export(): boolean {
     this.csvExportService.exportCities(this.dataSource.pageFilter);
   }
 
 }
 ```
 For more sample see ```src/app/components/federal/cities/cities.component.ts```
 


[FireLoop]: http://fireloop.io