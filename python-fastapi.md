# Installation

Install basic packages for using FastAPI
```
pip install fastapi "uvicorn[standard]"
```


# Basic setup

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

## Uvicorn
Launch command
```
uvicorn main:app --host 0.0.0.0 --port 8080 --reload
```

The reload option only works for changes in the python file. This can be overcome by using the `watchfiles` package of `uvicorn`, and running:
```
uvicorn main:app --host 0.0.0.0 --port 8080 --reload --reload-include *

```