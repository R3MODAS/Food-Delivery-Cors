# Food Delivery Cors Issue ✌
### This helps with the issue of cors which is caused between our frontend and swiggy's api and has been blocked by our browser to prevent from using data from someone else's backend. so here we are just bypassing that Cors issue by making our own proxy server 😉🤞

There is a middleware that sets up CORS headers to allow requests from any origin (*), with specific HTTP methods (GET, POST, PUT, DELETE), and specific headers (Content-Type, Authorization)
```
app.use((req, res, next) => {
  res.header('Access-Control-Allow-Origin', '*');
  res.header('Access-Control-Allow-Methods', 'GET, POST, PUT, DELETE');
  res.header('Access-Control-Allow-Headers', 'Content-Type, Authorization');
  next();
});
```
and `createProxyMiddleware` helps to create proxy requests as any requests made to `/api/proxy/swiggy/dapi` on the server will be proxied to `https://www.swiggy.com/dapi`
```
app.use('/api/proxy/swiggy/dapi', createProxyMiddleware({
  target: 'https://www.swiggy.com',
  changeOrigin: true,
  pathRewrite: {
    '^/api/proxy/swiggy/dapi': '/dapi',
  },
}));
```
