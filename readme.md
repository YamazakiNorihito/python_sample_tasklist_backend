### Server

* python

参考サイト
- [【初心者向け】Anacondaで仮想環境を作ってみる](https://qiita.com/ozaki_physics/items/985188feb92570e5b82d)
- [Anaconda環境にpipでパッケージをインストールする](https://qiita.com/mckeeeen/items/d4cbe4a16a102157f40c)
- [Anaconda環境でのvenv](https://www.python.jp/install/anaconda/conda_and_venv.html#u9FTA)

1. 仮想環境の確認
```bash
$ conda info -e
```
2. 仮想環境の作成
```bash
$ conda create -n py38_nextjs_restapi_tasklist python=3.8
```
   1. 仮想環境削除
      ```bash
        $ conda remove -n py38_nextjs_restapi_tasklist --all
      ```
3. 仮想環境の起動
```bash
$ source activate py38_nextjs_restapi_tasklist
```
    1. 仮想環境を終了
    ```bash
    $ source deactivate
    ```
4. 仮想環境にライブラリを追加
```bash
$ pip install <パッケージ名>
```
  - install
    - Django==3.1
    - django-cors-headers==3.4.0
    - djangorestframework==3.11.1
    - djangorestframework-simplejwt==4.6.0
    - djoser==2.0.3
    - python-decouple
    - dj-database-url
    - dj_static

4. django create project

```bash
$ django-admin startproject rest_api .
```

```bash
$ django-admin startapp api
```
- run
  ```bash
  $ manage.py runserver
  ```

5. superuser create
```bash
$ winpty python manage.py createsuperuser
```

#### deploying

```bash
$ pip freeze > requirements-dev.txt
```


1. HEROKUアカウント作成
   https://signup.heroku.com/
1. https://dashboard.heroku.com/apps
   1. NEW
   1. Create app
1. HEROKU CLI Install
   1. [Heroku CLI](https://devcenter.heroku.com/ja/articles/heroku-cli)
   1. exe install
   1. cmd
      ```bash
       $ heroku --version
          »   Warning: Our terms of service have changed: https://dashboard.heroku.com/terms-of-service
          heroku/7.53.0 win32-x64 node-v12.21.0
       $ heroku update
       $ heroku plugins:install heroku-config
          Installing plugin heroku-config... installed v1.5.4
       $ heroku login
      ``` 
1. deploying
   1. cmd
      ```bash
        $ heroku git:remote -a nextjs-tasklist-api
          set git remote heroku to https://git.heroku.com/nextjs-tasklist-api.git
        $ heroku config:push
          Successfully wrote settings to Heroku!
      ``` 
    2. site
       1. https://dashboard.heroku.com/apps/nextjs-tasklist-api/settings
          1. settings
             1. Config Vars
                1. djangoで設定していた環境数が設定されていることを確認
    1. cmd
       ```bash
        $ git add .
        $ git commit -m "****"
        $ git push heroku main
       ```
    1. migrate
       ```bash
         $ heroku run python3 manage.py migrate
         $ heroku run python3 manage.py createsuperuser
               Running python3 manage.py createsuperuser on ⬢ nextjs-tasklist-api... up, run.2009 (Free)
               Username (leave blank to use 'u47412'): admin
               Email address:
               Password:
               Password (again):
               This password is too short. It must contain at least 8 characters.
               This password is too common.
               Bypass password validation and create user anyway? [y/N]: y
               Superuser created successfully.
       ```  
  