FROM python:3.9.1

RUN apt-get install wget
RUN pip install pandas sqlalchemy psycopg2 psycopg2-binary
RUN pip install jupyter

WORKDIR /app
COPY ingest_data.py ingest_data.py 

ENTRYPOINT [ "python", "pipeline.py" ]


#docker postgres init w/o network
docker run -it -e POSTGRES_USER="root" -e POSTGRES_PASSWORD="root" -e POSTGRES_DB="ny_taxi" -v /workspaces/data-engineering-zoomcamp/01-docker-terraform/2_docker_sql/ny_taxi_postgres_data:/var/lib/postgresql/data -p 5432:5432 postgres:13

#docker pgadmin init w/o network
docker run -it -e PGADMIN_DEFAULT_EMAIL='admin@admin.com' -e PGADMIN_DEFAULT_PASSWORD='root' -p 8080:80 dpage/pgadmin4

#docker network init w postgres
docker network create pg-network

#docker init postgres w/network
docker run -it -e POSTGRES_USER="root" -e POSTGRES_PASSWORD="root" -e POSTGRES_DB="ny_taxi" -v /workspaces/data-engineering-zoomcamp/01-docker-terraform/2_docker_sql/ny_taxi_postgres_data:/var/lib/postgresql/data -p 5432:5432 --network=pg-network --name pg-database4 postgres:13

#docker pgadmin init w/network
docker run -it -e PGADMIN_DEFAULT_EMAIL='admin@admin.com' -e PGADMIN_DEFAULT_PASSWORD='root' -p 8080:80 --network=pg-network --name pg-database3 dpage/pgadmin4

