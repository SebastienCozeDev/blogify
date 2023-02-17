# Blogify

## Mise en route

### Créer un environnement virtuel.

```shell
python3 -m venv .env
```

### Sourcer l'environnement virtuel.

```shell
source .env/bin/activate
```

### Installer les packages utilisés par le projet.

```shell
pip install Django==4.1.7
pip install psycopg2==2.8.6
```

Pour le package `psycopg2`, assurez-vous d'avoir `libpq-dev` à jour avec le commande suivante.

```shell
sudo apt install libpq-dev
```

### Configurer la base de données.

Vous pouvez installer PostgreSQL à l'aide de [ce lien](https://www.postgresql.org/download/).

```shell
su - postgres
psql -c "CREATE DATABASE blog;"
psql -c "CREATE USER blogadmin WITH ENCRYPTED PASSWORD '2zBWdK55j6mB2q';"
psql -c "ALTER ROLE blogadmin SET client_encoding TO 'utf8';"
psql -c "ALTER ROLE blogadmin SET default_transaction_isolation TO 'read committed';"
psql -c "GRANT ALL PRIVILEGES ON DATABASE blog TO blogadmin;"
psql -d blog -c "CREATE SCHEMA djangoschema AUTHORIZATION blogadmin;"
```

Remplacez `2zBWdK55j6mB2q` par le mot de passe souhaité. Faites le aussi dans [`settings.py`](/src/blog/settings.py) à la ligne **85**.

### Faire les migrations.

```shell
cd src
python manage.py makemigrations
python manage.py migrate
```

### Créer un super utilisateur.

```shell
cd src
python manage.py createsuperuser
```

### Démarrer le serveur web.

```shell
cd src
python manage.py runserver
```
