

Create proxy.config.json
```
{
  "/api/*": {
    "target": "https://localhost:8080",
    "secure": false,
    "logLevel": "debug",
    "changeOrigin": true
  }
}
```


Run front end with proxy.
```
  "start": "ng serve --proxy-config proxy.config.json",
```