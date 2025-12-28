FROM python:3.13.11-slim

COPY --from=ghcr.io/astral-sh/uv:latest /uv /bin/

WORKDIR /code

ENV PATH="/code/.venv/bin:$PATH"

COPY pyproject.toml .python-version uv.lock ./

RUN uv sync --locked

COPY ingest_data.py .

ENTRYPOINT ["python", "ingest_data.py"]

### command to run
# docker run -it --rm\
#   -e POSTGRES_USER="root" \
#   -e POSTGRES_PASSWORD="root" \
#   -e POSTGRES_DB="ny_taxi" \
#   -v $(pwd)/ny_taxi_postgres_data:/var/lib/postgresql \
#   -p 5432:5432 \
#   --network=pg-network \
#   --name postgresdb \
#   postgres:18


# docker run -it --rm\
#   --network=pipeline_default \
#   taxi_ingest:v001 \
#     --pg-user=root \
#     --pg-pass=root \
#     --pg-host=postgresdb \
#     --pg-port=5432 \
#     --pg-db=ny_taxi \
#     --target-table=yellow_taxi_trips_2021_2 \
#     --year=2021 \
#     --month=2 \
#     --chunksize=100000

# docker run -it \
#   -e PGADMIN_DEFAULT_EMAIL="admin@admin.com" \
#   -e PGADMIN_DEFAULT_PASSWORD="root" \
#   -v pgadmin_data:/var/lib/pgadmin \
#   -p 8085:80 \
#   --network=pg-network \
#   --name pgadmin \
#   dpage/pgadmin4