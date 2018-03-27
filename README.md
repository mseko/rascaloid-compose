# これはなに？
- a-channelチーム用のdocker-composeファイル

# 内容
- a-channel-development/docker-compose.yml  
  開発時に使用するdocker-compose.yml  
  postgreSQL + rascaloidを起動する。  
  起動すると3000番でAPIサーバが待ち受けます。

- a-channel-production/docker-compose.yml  
  デモ環境で使う想定のdocker-compose.yml  
  a-channel-development との違いは以下の通り。  
  - PostgreSQLのデータをボリュームに書き出す設定になっている。
  - APIサーバのポートをホストのポートと紐づけていない。

# 動作確認
## a-channel-development/docker-compose.yml

１． 以下のコマンドでdockerコンテナを起動します。
```
$ docker-compose up -d
```

２． 数十秒待ちます

３． 以下のコマンドを実行します。
```
$ curl -I -X GET "http://localhost:3000/projects" -H "accept: application/json" -H "X-Bouncr-Credential: eyJhbGciOiJub25lIiwidHlwIjoiSldUIn0.eyJzdWIiOiJ1c2VyMSIsIm5hbWUiOiJUZXN0IHVzZXIxIiwicGVybWlzc2lvbnMiOlsicHJvamVjdDpyZWFkIiwicHJvamVjdDpjcmVhdGUiLCJwcm9qZWN0OnVwZGF0ZSIsInByb2plY3Q6ZGVsZXRlIl19.lfegO1IXi1hlBETymqw8nqRaq7POrnriJU_5YK2R-PI"
```

４． ３のコマンドの実行結果として、以下のように `HTTP/1.1 200 OK` が返ってきたらAPIサーバを使用可能な状態になっています。
```
HTTP/1.1 200 OK
Date: Wed, 21 Mar 2018 08:27:04 GMT
Content-Type: application/json
Content-Length: 2
Server: Jetty(9.4.z-SNAPSHOT)
```


# 参考
以下にrascalodのAPIの仕様が存在します。
- https://github.com/kawasima/rascaloid/blob/master/src/main/resources/public/rascaloid_api.yaml
