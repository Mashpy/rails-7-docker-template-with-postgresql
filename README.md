## Ruby on Rails 7 docker template with postgresql

1. Download the project first or git clone.

```
 git clone https://github.com/Mashpy/rails-7-docker-template-with-postgresql.git
```
If you clone you have to change your repo name later from .git/config file

2. Rename the project name as your wish

```
 mv rails-7-docker-template-with-postgresql your_project_name
```

3. Change directory -

```
 cd your_project_name
```

4. Update your rails version on the Gemfile -

```
source 'https://rubygems.org'
gem 'rails', '7.0.3'
```

5. Update Ruby version on Dockerfile -

```
FROM  ruby:3.1.2-slim
```

6. Now install new rails app -

```
 docker-compose run app rails new . --force --database=postgresql --skip-bundle
```

7. Build the docker image -

```
 docker-compose build
```

8. Update database details on config/database.yml file.

```
default: &default
  adapter: postgresql
  encoding: unicode
  host: postgres
  username: postgres
  password: password
  pool: 5

development:
  <<: *default
  database: dev


test:
  <<: *default
  database: dev
```

9. Run -

```
 docker-compose up
```
10. wait little bit see your eyes on the console, it should show -
```
Puma Listening on http://0.0.0.0:3000
Pg admin Listening at: http://[::]:80 (1)
```
It will take time to load. Keep patient. After then then open another terminal and create a database -
```
docker-compose exec app rake db:create
```
11. Browse http://localhost:3000.
    ![Ruby on rails 7.0.3 docker with mysql](https://i.ibb.co/Z19FNSJ/Screenshot-2022-07-30-at-9-11-24-PM.png)

12. Browse http://localhost:5050/ . You can login on pgadmin. 
username: admin@admin.com
password: password

13. Add database connection on pgadmin. You need your postgres_container IP address.

```
docker ps
```
copy hash code of postgres_container. 

```
docker inspect fcc97e066cc8 | grep IPAddress
```

14. after login on pgadmin add connection. Write host IP address.
username: postgres
password: password

15. now you can start work on your project.