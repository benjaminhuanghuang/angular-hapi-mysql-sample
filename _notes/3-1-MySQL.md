## setup
```
npm i mysql
```

create src/database.js

```
import mysql from 'mysql';

const connection = mysql.createConnection({
  host: 'localhost',
  user: 'hapi-server',
  password: 'abc123!',
  database: 'buy-and-sell',
});

export const db = {
  connect: () => connection.connect(),
  query: (queryString, escapedValues) =>
      new Promise((resolve, reject) => {
          connection.query(queryString, escapedValues, (error, results, fields) => {
              if (error) reject(error);
              resolve({ results, fields });
          })
      }),
  end: () => connection.end(),
}
```

## Query
```
import { db } from '../database';

export const addViewToListingRoute = {
  method: 'POST',
  path: '/api/listings/{id}/add-view',
  handler: async (req, h) => {
    const id = req.params.id;
    await db.query(
        'UPDATE listings SET views=views+1 WHERE id=?',
        [id],
    );
    const { results } = await db.query(
        'SELECT * FROM listings WHERE id=?',
        [id],
    );
    const updatedListing = results[0];
    return updatedListing;
  }
}
```