---
tags:
  - WSL
  - setting
---
## 1. WSLの設定ファイルを記述
Windows上の`C:\User\(ユーザ名)\.wslconfig`に以下の内容を記述する．
```
[wsl2]
memory=8GB
processors=4
```
>[!INFO] 設定項目について
>memoryはホストのRAMの半分程度にする．


## 2. WSLの再起動
記述した後，以下のコマンドを実行し，WSLをシャットダウンする．
```
wsl --shutdown
```
WSLはシャットダウン後，自動で再起動する．
