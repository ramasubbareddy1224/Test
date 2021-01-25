# run mysql container
```
db:
    image: mysql:5.7
    env_file: .env
    ports:
      - ${MYSQL_HOST_PORT}:${MYSQL_PORT}
    expose:
      - ${MYSQL_PORT}
    volumes:
      - ./db/initscript:/docker-entrypoint-initdb.d 

```
# load docker image
``` 
docker load < pdfextractordocker.tar
```
# container bind mounting
```
app:
    build: .
    env_file: .env
    depends_on:
      - db
    volumes:
      - ./input:/code/input
    command: sh -c "/code/wait-for-it.sh --timeout=0 db:3306 && cron -f"
```

    
