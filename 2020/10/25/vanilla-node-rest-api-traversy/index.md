---
title: vanilla node rest api
date: "2020-10-25"
description: notes from traversy media
---

```javascript
const http = require('http')
const products = require('./data/products')

const server = http.createServer((req, res) => {
  if(req.url === '/api/products' && req.method === 'GET') {
    res.writeHead(200, { 'Content-Type': 'application/json' })
    res.end(JSON.stringify(products))
  } else {
    res.writeHead(404, { 'Content-Type': 'application/json' })
    res.end(JSON.stringify({ message: 'Route Not Found' }))
  }
})

const PORT = process.env.PORT || 5000

server.listen(PORT, () => console.log(`Server running on port ${PORT}`))
```

```javascript
const products = require('../data/products')

function findAll() {
  return new Promise((resolve, reject) => {
    resolve(products)
  })
}

module.exports = {
  findAll
}
```

```javascript
const Product = require('../models/productModel')

async function getProducts(req, res) {
  try {
    const products = await Product.findAll()

    res.writeHead(200, { 'Content-Type': 'application/json' })
    res.end(JSON.stringify(products))
  } catch (error) {
    console.log(error)
  }
}

module.exports = {
  getProducts
}
```

```javascript
const { getProducts } = require('./controllers/productController')

const server = http.createServer((req, res) => {
  if(req.url === '/api/products' && req.method === 'GET') {
    getProducts(req, res)
  } else {
    res.writeHead(404, { 'Content-Type': 'application/json' })
    res.end(JSON.stringify({ message: 'Route Not Found' }))
  }
})
```

```javascript
const server = http.createServer((req, res) => {
  if(req.url === '/api/products' && req.method === 'GET') {
    getProducts(req, res)
  } else if(req.url.match(/\/api\/products\/([0-9]+)/) && req.method === 'GET') {
    const id = req.url.split('/')[3]
    getProduct(req, res, id)
  } else {
    res.writeHead(404, { 'Content-Type': 'application/json' })
    res.end(JSON.stringify({ message: 'Route Not Found' }))
  }
})
```