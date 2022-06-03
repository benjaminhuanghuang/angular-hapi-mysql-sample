## HttpClient: Call API
app.module.ts
```
  import { HttpClientModule } from '@angular/common/http';

  ...

  imports: [
    HttpClientModule,
  ],
```

## Rxjs: Async call
instead of return data directly, the methond in the service returns a Observable<T>
```
import { Injectable } from '@angular/core';
import { HttpClient, HttpHeaders } from '@angular/common/http';
import { Observable, observable } from 'rxjs';

@Injectable({
  providedIn: 'root'
})
export class ListingsService {
  // Use the http client injected
  constructor(
    private http: HttpClient,
  ) { }

  getListings(): Observable<Listing[]> {
    return this.http.get<Listing[]>('/api/listings');
  }
}
```


## Use service in component

```
 ngOnInit(): void {
  this.listingsService.getListings()  // return a observable
    .subscribe(listings => this.listings = listings);
}
```

