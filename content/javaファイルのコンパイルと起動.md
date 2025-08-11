【前提】
javaがインストールされていること

## 1行でコンパイル+実行
```bash
javac -d dst *.java && java -cp dst Game
```

## コンパイル
```bash
javac -d dst *.java
```

>[!INFO] オプション
>`-d`: 出力先ディレクトリ(ここでは`dst`)
>
>他のオプションは`javac`実行で確認可能

## 実行
```bash
java -cp dst Game
```

>[!INFO] オプション
>`-cp`: クラスパス(ファイルの場所が`./dst/path/to/entry/Game.class`だったら，`java -cp dst path.to.entry.Game`らしい)

【エントリポイントについて】
実行している`Game`はエントリポイント

【実行対象ファイル】
実行するファイルは`*.class`
※ javaはjavaファイルからclassファイルにコンパイルし，classファイルを仮想マシン上で動的に処理することによって実行する
