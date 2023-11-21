# ERPNext-V14-dev-using-container

# Bootstrap Containers for development

```
git clone https://github.com/frappe/frappe_docker.git
cd frappe_docker
cp -R devcontainer-example .devcontainer
cp -R development/vscode-example development/.vscode
```

## Download VS Code & Remote Container Extenstion

```
code .
```

# Setup first bench

```
sudo chmod 777 /workspace/development
bench init --skip-redis-config-generation --frappe-branch version-14 frappe-bench
```

# Setup hosts

```
bench set-config -g db_host mariadb
bench set-config -g redis_cache redis://redis-cache:6379
bench set-config -g redis_queue redis://redis-queue:6379
bench set-config -g redis_socketio redis://redis-queue:6379
```

# reate a new site with bench

```
bench new-site --mariadb-root-password 123 --admin-password admin --no-mariadb-socket development.localhost
```

# Set bench developer mode on the new site

```
bench --site development.localhost set-config developer_mode 1
bench --site development.localhost clear-cache
```

# Install an app

```
bench get-app --branch version-14 --resolve-deps erpnext
bench --site development.localhost install-app erpnext
```
# Start Frappe without debugging

`bench start`

