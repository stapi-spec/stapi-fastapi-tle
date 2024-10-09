# STAPI FastAPI - TLE

This is an example implementation for https://github.com/stapi-spec/stapi-fastapi generating opportunity previews based on a TLE.

## Configuration

The mock backend uses SQLite/Spatialite as storage, therefore the
`SPATIALITE_LIBRARY_PATH` env var must be set to load the spatialite extension:

```bash
export DATABASE=sqlite:///order.sqlite
export SPATIALITE_LIBRARY_PATH=/path/to/mod_spatialite.dylib
```

### Linux (Debian)

If you installed spatialite, for example, through `apt` you can reference it like so:

```bash
export SPATIALITE_LIBRARY_PATH=mod_spatialite.so
```

## Running locally

```
poetry run tle
```

## Some useful curl commands to test the service

_GET all products_

```
curl http://127.0.0.1:8000/products
```

_POST to opportunities_

```
curl -d '{"datetime":"2014-10-01T13:00:00Z/2014-10-10T15:30:00Z","product_id":"mock:standard","geometry":{"type":"Point","coordinates":[-115.06855238269905,31.987811301701587]},"properties":{"off_nadir":{"minimum":0,"maximum":35}},"filter":{}}'  -H 'Content-Type: application/json' -X POST http://127.0.0.1:8000/opportunities
```
