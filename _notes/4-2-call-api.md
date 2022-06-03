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
```
  npm i rxjs
```

instead of return data directly, the methond in the service returns a Observable<T>
```
import { Injectable } from '@angular/core';
import { HttpClient, HttpHeaders } from '@angular/common/http';
import { Observable, observable } from 'rxjs';

const httpOptions = {
  headers: new HttpHeaders({
    'Content-Type': 'application/json',
  })
};

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

  addViewToListing(id: string): Observable<Listing> {
    return this.http.post<Listing>(
      `/api/listings/${id}/add-view`,
      {},
      httpOptions,
    );
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


## Loading status
template
```
<div class="content-box" *ngIf="!isLoading">
</div>
<div class="content-box" *ngIf="isLoading">
    <h3>Loading...</h3>
</div>
```   

component
```
export class MyComponent implements OnInit {
  isLoading: boolean = true;
  listing: Listing;

  constructor(
    private route: ActivatedRoute,
    private listingsService: ListingsService,
  ) { }

  ngOnInit(): void {
    const id = this.route.snapshot.paramMap.get('id');
    this.listingsService.getListingById(id)
      .subscribe(listing => {
        this.listing = listing;    // <-- change loading status
        this.isLoading = false;
      });
    this.listingsService.addViewToListing(id)
      .subscribe(() => console.log('Views updated!'));
  }

}
```