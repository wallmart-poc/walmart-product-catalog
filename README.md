# walmart-product-catalog · Product Catalog Service

Product listing and lookup gRPC service. Acts as the single source of truth for all product data, loaded from a static JSON catalog at startup.

## Stack
- **Language:** Go 1.21
- **Framework:** gRPC

## API
Implements `ProductCatalogService` from `demo.proto`:
- `ListProducts(Empty) → ListProductsResponse`
- `GetProduct(GetProductRequest) → Product`
- `SearchProducts(SearchProductsRequest) → SearchProductsResponse`

Product data is loaded from `products.json` at startup and held in memory.

## Running locally
```bash
go mod vendor
go run .
```
Service listens on port `3550` by default (`PRODUCT_CATALOG_SERVICE_PORT`).

Set `DISABLE_STATS=1` to suppress stats output during local development.

## Known behaviors
- **Dynamic reload:** Sending `USR1` triggers catalog reload on every request (intentional bug for profiling demos). Send `USR2` to disable.
- **Latency injection:** Set `EXTRA_LATENCY=5s` to add artificial delay to every response.

## Dependencies
None — all data is served from the local `products.json` file.

