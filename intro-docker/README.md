# Comands Essencials

- docker run hello-world
- docker run -it ubuntu bash
- rm -rm /
- docker run -it python:3.9 (image:specific version)

## Construir una imagen con su respectiva versión.
- docker build -t test:pandas .
## execute containers
- docker run -it test:pandas
- docker run -it test:pandas 2021-10-12 hello 123
## control contenedores
- docker ps
- docker stop containersId
- docker start containerID
- docker kill containerId
- docker container prune (Elimina all stop containers)

# Docker compose
- docker-compose up
- docker-compose up -d
- docker-compose down


## execute postgres
docker run -it -e POSTGRES_USER="root" -e POSTGRES_PASSWORD="root" -e POSTGRES_DB="ny_taxi"  -v $(pwd)/ny_taxi_postgres_data:/var/lib/postgresql/data --network=pgadmindb --name pgdatabasedb  -p 5432:5432  postgres:13

# Create network
- docker network  create pgadmindb

# Jupyter Notebook
- jupyter nbconvert --to=script name_notebook.ipynb

# To access the database you can use pgcli
- pip install pgcli
- pgcli -h localhost -p 5432 -u root -d ny_taxi 
    - Enter password
    - \dt (listar las tablas)
    - \d yellow_taxi_data (tableName)
- selects
    - SELECT COUNT(1) FROM yellow_taxi_data
    - DROP TABLE TABLE_NAME

- pg Admin
    - portHost:portContainer 
    - docker run -it -e PGADMIN_DEFAULT_EMAIL="admin@admin.com" -e PGADMIN_DEFAULT_PASSWORD="root" --network=pgadmindb --name pgadmindatabase  -p 8090:80 dpage/pgadmin4

# run python ingest
URL="https://github.com/DataTalksClub/nyc-tlc-data/releases/download/yellow/yellow_tripdata_2021-01.csv.gz"

python ingest_data.py \
    --user=root \
    --password=root \
    --host=localhost \
    --port=5432 \
    --db=ny_taxi \
    --table_name=yellow_taxi_trips \
    --url=${URL}

docker run -it \
    --network=pgadmindb \
    taxi_ingest:v001 \
    --user=root \
    --password=root \
    --host=pgdatabasedb \
    --port=5432 \
    --db=ny_taxi \
    --table_name=yellow_taxi_trip \
    --url=${URL}

# Create server directory, python
python -m http.server 

# samples
- !head -n 100 yellow_tripdata_2021-01.csv > yellow_head.csv
- !wc -l yellow_tripdata_2021-01.csv # para listar número de líneas del archivo
- history
