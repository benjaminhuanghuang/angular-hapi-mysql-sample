# Angular services
Angular services are objects that get instantiated just once during the lifetime of an application. 
They contain methods that `maintain data` throughout the life of an application.


## Inject service into component
```
  constructor(private service: MyDataService,) 
  { }

  ngOnInit: void() {
    this.data = this.sercvice.getData();
  }
```