## Ruby on Rails 7 docker template with postgresql

1. First clone the project

```
 git clone https://github.com/Mashpy/rails-7-docker-template-with-postgresql.git
```

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

10. Browse http://localhost:3000
    ![Ruby on rails 7.0.3 docker with mysql](https://i.ibb.co/Z19FNSJ/Screenshot-2022-07-30-at-9-11-24-PM.png)

11. You can also login on pgadmin. Browse http://localhost:5050/
username: admin@admin.com
password: password

12. Add database connection on pgadmin. You need your postgres_container IP address.

```
docker ps
```
copy hash code of postgres_container. 

```
docker inspect fcc97e066cc8 | grep IPAddress
```

13. after login on pgadmin add connection. Write host IP address.
username: postgres
password: password

14. Open another terminal and create a database -
```
docker-compose exec app rake db:create
```
15. now you can start work on your project.