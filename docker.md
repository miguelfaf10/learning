# Docker


## Basic Dockerfile configuration
Example of `Dockerfile` for running container with Python FastAPI app:
```
FROM python:3.11.0

# set the working directory
WORKDIR /app

# install dependencies
COPY ./requirements.txt /app
RUN pip install --no-cache-dir --upgrade -r requirements.txt

# copy the scripts to the folder
COPY . /app

# start the server
CMD ["uvicorn", "main:app", "--host", "0.0.0.0", "--port", "80"]
```


Building docker image
```
docker build -t <image-name> .
```

Runnin docker image with port forwarding:
```
docker run -p 8080:80 <image-name>
```

## Using Docker-compose
With previous setup, everytime code is changed one needs to rebuild and restart the image.

Docker-compose has two features to help with this:
- Use a custom RUN command that restarts the app when a file has been changed;
- Sync a folder on machine by mounting it as a volume inside container

Docker-compose is configured via a `.yaml` file

Example of `docker-compose.yaml` for running container with Python FastAPI app locally, with auto-reload:
```
services:
    app:
        build: .
        container_name: app
        command: uvicorn main:app --host 0.0.0.0 --port 80 --reload
        ports:
            - 8080:80
        volumes:
            - .:/app
```
The custom `command` overwrites the `CMD` in Dockerfile, and the `volumes` command replaces the `COPY` one.

To run the new configuration use, where we build the image in the beginning:
```
docker-compose up --build
```