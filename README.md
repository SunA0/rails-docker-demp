## 基于docker部署的Rails项目
```
ruby-version: 2.5.8
Rails-version: 5.2.4.4
database: postgres
```
### 开始
1.下载项目
```
$ git clone myapp.git
$ cd myapp
```

2.根据gemfile 创建项目
```
$ docker-compose run web rails new . --force --database=postgresql
```

3.如果网不好 修改gemfile的源
```
# myapp/gemfile

-source 'https://rubygems.org'
+source 'https://gems.ruby-china.com/'
```

4.搭建镜像
```
$ docker-compose build
```

5.修改数据库配置
```
# config/database.yml

default: &default
  adapter: postgresql
  encoding: unicode
  pool: <%= ENV.fetch("RAILS_MAX_THREADS") { 5 } %>
  username: root
  password: admin
development:
  <<: *default
  database: app_development
  host: db
test:
  <<: *default
  database: app_test
  host: db
```
6.启动rails进程
```
$ docker-compose up
或
$ docker-compose up -d 
```

### 开发
```
$ docker-compose run web rails db:create
$ docker-compose run web rails db:migrate
```
