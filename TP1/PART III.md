# Part III : docker-compose
## 2. WikiJS

🌞 Installez un WikiJS en utilisant Docker
```sh
gustave@debian:mkdir ~/wikijs && cd ~/wikijs
gustave@debian:~/wikijs$
cat > docker-compose.yml << 'EOF'
services:
  db:
    image: postgres:15-alpine
    environment:
      POSTGRES_DB: wiki
      POSTGRES_PASSWORD: wikijsrocks
      POSTGRES_USER: wikijs
    restart: unless-stopped
    volumes:
      - db-data:/var/lib/postgresql/data

  wiki:
    image: ghcr.io/requarks/wiki:2
    depends_on:
      - db
    environment:
      DB_TYPE: postgres
      DB_HOST: db
      DB_PORT: 5432
      DB_USER: wikijs
      DB_PASS: wikijsrocks
      DB_NAME: wiki
    restart: unless-stopped
    ports:
      - "80:3000"

volumes:
  db-data:
EOF
```
```sh
gustave@debian:~/wikijs$ docker compose up -d
docker compose ps
[+] up 2/2
 ✔ Container wikijs-db-1   Started                                                         1.8s
 ✔ Container wikijs-wiki-1 Started                                                         2.7s
NAME            IMAGE                     COMMAND                  SERVICE   CREATED         STATUS         PORTS
wikijs-db-1     postgres:15-alpine        "docker-entrypoint.s…"   db        5 seconds ago   Up 4 seconds   5432/tcp
wikijs-wiki-1   ghcr.io/requarks/wiki:2   "docker-entrypoint.s…"   wiki      5 seconds ago   Up 3 seconds   3443/tcp, 0.0.0.0:80->3000/tcp, [::]:80->3000/tcp
gustave@debian:~/wikijs$
```

# 3. Make your own meow

🌞 Lets'GO
```sh
gustave@debian:~$ git clone https://gitlab.com/it4lik/b2e3-cloud.git
cd b2e3-cloud/tp/1/python-app
ls
Clonage dans 'b2e3-cloud'...
remote: Enumerating objects: 33, done.
remote: Counting objects: 100% (33/33), done.
remote: Compressing objects: 100% (29/29), done.
remote: Total 33 (delta 3), reused 0 (delta 0), pack-reused 0 (from 0)
Réception d'objets: 100% (33/33), 1.79 Mio | 1.29 Mio/s, fait.
Résolution des deltas: 100% (3/3), fait.
app.py  requirements.txt  templates
gustave@debian:~/b2e3-cloud/tp/1/python-app$
```

```sh
gustave@debian:~/b2e3-cloud/tp/1/python-app$ nano Dockerfile
text
FROM python:3.11-alpine

WORKDIR /app

COPY requirements.txt .
RUN pip install -r requirements.txt

COPY . .

CMD ["python3", "app.py"]
```

```sh
gustave@debian:~/b2e3-cloud/tp/1/python-app$ docker compose up -d --build
[+] Building 4.4s (12/12) FINISHED
 => [internal] load local bake definitions                                                0.0s
 => => reading from stdin 526B                                                            0.0s
 => [internal] load build definition from Dockerfile                                      0.1s
 => => transferring dockerfile: 175B                                                      0.0s
 => [internal] load metadata for docker.io/library/python:3.11-alpine                     0.8s
 => [internal] load .dockerignore                                                         0.1s
 => => transferring context: 2B                                                           0.0s
 => [1/5] FROM docker.io/library/python:3.11-alpine@sha256:f07e2ace46f560f09a6eeec7b4913  0.6s
 => => resolve docker.io/library/python:3.11-alpine@sha256:f07e2ace46f560f09a6eeec7b4913  0.5s
 => [internal] load build context                                                         0.3s
 => => transferring context: 199B                                                         0.0s
 => CACHED [2/5] WORKDIR /app                                                             0.0s
 => CACHED [3/5] COPY requirements.txt .                                                  0.0s
 => CACHED [4/5] RUN pip install -r requirements.txt                                      0.0s
 => CACHED [5/5] COPY . .                                                                 0.0s
 => exporting to image                                                                    1.3s
 => => exporting layers                                                                   0.0s
 => => exporting manifest sha256:4b3ae1cabca0ff9ac6b6a2fbd9dd2ac411d40375460e5eaa325cead  0.0s
 => => exporting config sha256:64a18124dcfa16002c435eab7f1165582a1ffff129dab2639d7bb7e7f  0.0s
 => => exporting attestation manifest sha256:a3d4f40dec46b5a4cec539f6328e775c991f19024f4  0.7s
 => => exporting manifest list sha256:6c29d71f2e8f6e49b84db9896f752000cc9a892bfd23af138c  0.1s
 => => naming to docker.io/library/python-app-app:latest                                  0.0s
 => => unpacking to docker.io/library/python-app-app:latest                               0.1s
 => resolving provenance for metadata file                                                0.1s
[+] up 3/3
 ✔ Image python-app-app       Built                                                        4.7s
 ✔ Container python-app-app-1 Started                                                      4.7s
 ✔ Container python-app-db-1  Started                                                      1.2s
gustave@debian:~/b2e3-cloud/tp/1/python-app$
```





