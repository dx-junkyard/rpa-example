# rpa-example

## 使用する上での注意事項
設定ファイル中のパスワードは仮の簡単なものになっていますので、全て変更してください。

## 環境構築手順

1. templateをコピーして設定ファイルを作成
```
mv ./config/api-rpa-ocr-spring-application.yaml.template ./config/api-rpa-ocr-spring-application.yaml
```

2. xxx-application.yamlの書き換え
シークレットなど、各設定項目を適切なものに書き換える
エディタはviに限らず使いやすいものを選択してください
```
vi ./config/api-rpa-ocr-spring-application.yaml
```

3. ソースコードのビルドとdocker image作成、docker-compose.yamlの作成
```
sh build.sh
```

4. docker-composeでサービスを構成するdockerコンテナを起動する
```
docker-compose up -d
```
## 動作確認: APIの利用方法
```
curl -XPOST -F 'file=@./koyouhoken.png' http://localhost/rpa-ocr/v1/api/health-insurance-card
```

## 動作確認（DBの内容確認）
1. dockerコンテナへの接続
```
docker ps
docker exec -it mysqlのCONTAINER_ID /bin/bash
```

2. mysqlへの接続
```
mysql -h rpa-mysql -P 3306 -u root -p
# passwordはデフォルトではroot
use rpadb;
show tables;
```

