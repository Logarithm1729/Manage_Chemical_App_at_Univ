# 研究室内廃液管理アプリ
- 研究を行う過程で排出される薬品を管理する
- 従来、研究室で使用されていたソフトが古く使用しづらいため作製した

# ログイン画面
![ログイン画面](https://user-images.githubusercontent.com/76026039/213667459-a1b997c1-9c91-4327-92a4-49eb2c5d4b38.png)
# 2022年10月の画面
![2022年10月の画面](https://user-images.githubusercontent.com/76026039/213667759-5d4d0549-42b1-4245-9b6d-56e9c873feda.png")
# 廃液の追加と編集
![薬品の追加・編集](https://user-images.githubusercontent.com/76026039/213668517-a3e7a0f4-9df6-4e6a-94e2-4e0e12d8e436.png)
# 通常ユーザーと管理者ユーザーでの権限の有無
![ユーザーの違い](https://user-images.githubusercontent.com/76026039/213668672-24fb7ddc-6027-461a-ba13-495c27c895d9.png)

# 環境
### バックエンド
- Python 3.x
- Django
- psycopg2
- djangorestframework
- djangorestframework-simplejwt
- djoser
- pillow
- django-cors-headers
- django-environ
- mysqlclient

### フロントエンド
- TypeScitpt
- React.js
- Material UI
- Redux tool kit

### インフラ関連
- 研究室にあるPCをAPサーバーとして使用
- docker
- docker-compose


# 使い方
1. 当アプリを起動
```zsh
docker-compose up -d
```
2. データベースのユーザーを作成し、権限を与える
```zsh
docker-compose exec db psql -U postgres
```
その後、Postgresqlが起動する
```sql
CREATE DATABASE データベース名;
CREATE USER ユーザー名 WITH PASSWORD 'パスワード';
GRANT ALL PRIVILEGES ON DATABASE データベース名 TO ユーザー名;
```
ctrl + d で終了する


3. secrets.pyファイルを作成する
./backend/config/secrets.py を作成し、以下の内容を2.で設定したデータベース名、ユーザー名、パスワードを入力する
```python
# SECURITY WARNING: keep the secret key used in production secret!
SECRET_KEY = 'シークレットキーを取得し、ペーストする'

# SECURITY WARNING: don't run with debug turned on in production!
DEBUG = True

ALLOWED_HOSTS = ["*"]

# Database
# https://docs.djangoproject.com/en/4.0/ref/settings/#databases

DATABASES = {
    'default': {
        'ENGINE': 'django.db.backends.postgresql',
        'NAME': 'データベース名',
        'USER': 'ユーザー名',
        'PASSWORD': 'パスワード',
        'HOST': 'db',
        'PORT': 5432 ,
    }
}
```

4. バックエンドの環境を設定
```zsh
# スーパーユーザーを作成
docker-compose exec backend python manage.py createsuperuser

# データベースの設定をmigrateする
docker-compose exec backend python manage.py migrate
```

# 作成時期
2022/6 ~
