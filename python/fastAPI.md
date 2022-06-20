# Basis

## ausführen
uvicorn {main_file}:{instance_of_fastAPI} z.B. uvicorn main:app --reload --port 8000

## Docs
http://127.0.0.1:8000/docs <- documentation provided by swagger
http://127.0.0.1:8000/redoc <- documentation provided by redoc

http://127.0.0.1:8000/openapi.json <- raw OpenAPI schema


# Endpunkte
    ## Die Ordnung von Endpunkte macht unterschied

    @app.get("/users/me")

    @app.get("/users/{user_id}")
    async def read_user(user_id: str)