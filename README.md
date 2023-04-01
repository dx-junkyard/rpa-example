# rpa-example

## 使用する上での注意事項
設定ファイル中のパスワードは仮の簡単なものになっていますので、全て変更してください。

## 機能概要
実現できるもの
```
proxy(nginx) - API(SpringBoot) - CLOVA OCR APIの呼出 - DB(MySQL)
```
で構成されたドキュメントの読み取りとDBへの保存機能、スキャンしたドキュメントはユーザーごとに作成されるディレクトリに保存される


## 環境構築手順

1. 適当な作業場所でrepositoryをclone、取得したディレクトリに移動する
```
git clone https://github.com/dx-junkyard/rpa-example.git && cd rpa-example
```

2. templateをコピーして設定ファイルを作成
```
mv ./config/api-rpa-ocr-spring-application.yaml.template ./config/api-rpa-ocr-spring-application.yaml
```

3. xxx-application.yamlの書き換え
シークレットなど、各設定項目を適切なものに書き換える
エディタはviに限らず使いやすいものを選択してください
```
vi ./config/api-rpa-ocr-spring-application.yaml
```

4. ソースコードのビルドとdocker image作成、docker-compose.yamlの作成
```
sh build.sh
```

5. docker-composeでサービスを構成するdockerコンテナを起動する
```
docker-compose up -d
```

## 動作確認: APIの利用方法
1. CLOVA OCRのテンプレート設定は各自実施してください。

2. 読み取るフィアルを配置する（現在はpngのみ対応）

3. ファイルの読み取り実行
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

