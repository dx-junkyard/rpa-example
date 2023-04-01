# rpa-example

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

