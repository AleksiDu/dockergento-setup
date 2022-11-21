# Dockergento Setup

___

## Install dockergento console

1. Clone the repo:  
   ``` git clone https://github.com/developersalliance/magento2-dockergento.git ```
2. Create links to the directory ```/usr/local/bin/```
    ``` sudo ln -s $(pwd)/magento2-dockergento/bin/dockergento /usr/local/bin/ ```
3. Open a new terminal tab/window and check that dockergento works:

    ```bash
    which dockergento  
    dockergento
    ```

## Create new project

```bash
    mkdir <project-name>
    cd <project-name>
    dockergento setup
    dockergento create-project
```

## Install the application

```bash
dockergento magento setup:install \
--base-url=http://my-magento.ge \
--db-host=db \
--db-name=magento \
--db-user=root \
--db-password=password \
--admin-firstname=admin \
--admin-lastname=admin \
--admin-email=admin@admin.com \
--admin-user=admin \
--admin-password=admin123 \
--language=en_US \
--currency=USD \
--timezone=America/Chicago \
--use-rewrites=1 \
--search-engine=elasticsearch7 \
--elasticsearch-host=elasticsearch \
--elasticsearch-port=9200 \
--elasticsearch-index-prefix=magento2 \
--elasticsearch-timeout=15
```

## Disable two factor authentication

``` dockergento magento module:disable Magento_TwoFactorAuth ```

## Sample data install

Enter bush : ``` dockergento bash ```

Inside bush run:

```bash
php -d memory_limit=-1 /usr/local/bin/composer install \
&& php -d memory_limit=-1 bin/magento sampledata:deploy \
&& php -d memory_limit=-1 bin/magento se:up \
&& php -d memory_limit=-1 bin/magento deploy:mode:set developer
