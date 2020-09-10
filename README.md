# Jagaad

* Non ho utilizzato nessun Docker registry per non rendere il codice pubblico, quindi il codice e il backup del database te li passo separatamente, oltre che a caricare il codice qui su Github :)
* Ho utilizzato PHP nativo, appena ho tempo lo faccio anche in Laravel giusto per mia conoscenza e te lo mando.
* Server Ubuntu



## HowTo


Carica i file `docker-compose.yml` / `.env` / `Dockerfile` / `src.tar`, nella root del nuovo progetto Docker ed esegui questi comandi:

```bash
docker-compose up -d
```

Estrai l'archivio `src.tar` contenente il codice sostituendo **CONTAINER** con il nome del tuo container:
````bash
docker run --rm --volumes-from CONTAINER_php_1 -v $(pwd):/backup php:7.4-apache bash -c "cd / && tar xvf /backup/src.tar"
````

* Importa il database ja_test.sql come preferisci: terminale/phpmyadmin/..
* Enjoy


## Export CSV

Essendo un test php ho pensato di creare una funzione per esportare il CSV utilizzando PHP e cURL:
```bash
curl -d 'act=export_csv' http://DOMAIN_OR_IP/jagaad/core/controller/wishlist.controller.php
```

In alternativa ho creato anche un CLI, sostituisci "CONTAINER" con il nome del tuo container:
```bash
docker exec -i CONTAINER_db_1 mysql -D ja_test -u root -p -e "SELECT count(w.id) as n_items_wishlist, u.email FROM wishlist AS w JOIN users AS u ON u.id=w.id_user GROUP BY u.id" | awk '{print $1";"$2}' > users.csv
```
# Footnotes

P.s: Scusa l'attesa ma sto creando un APP in AR molto simpatica, poi te la faccio vedere. Sono comunque contento di essere riuscito a rispettare il tempo di consegna lavorandoci alcune sere quando ero libero dal resto.
Qualsiasi feedback è ben accetto.
