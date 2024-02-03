Installation
===

Install basic packages for using FastAPI
```
pip install fastapi "uvicorn[standard]"
```


Basic setup
===
Create instance of FAstAPI app to which we'll add all the routes,
```
app = FastAPI()
```

Create pydantic object class,
```
class Object(BaseModel):
    name: str
```
and callback function for the url routing
```
@app.get("/")
def index() -> dict[str, Object]:
    return {"objects": object}
```

