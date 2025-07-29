【発生事例】
```
mv source-dir/* target-dir/
```

【原因】
source-dirの中身が多すぎて、ワイルドカード展開で生成されるファイル名の数がシステムの上限(ARG_MAX)を超えたため。

【対処】
`rsync`を利用して、以下のように実行
```
rsync -a --remove-source-files --info=progress2 source-dir/ target-dir/
find source-dir -mindepth 1 -type d -empty -delete
```

高速化する場合、`xargs`を利用して以下のように実行
```
find source-dir/ -type f -print0 \
| xargs -0 -n10 -P8 \
rsync -a --remove-source-files --files-from=- --from0 source-dir/ target-dir/
find source-dir -mindepth 1 -type d -empty -delete
```

>[!NOTE] オプション
>`find`コマンド
>- `-type f`：ファイルのみを対象とする
>- `-print0`：検索結果をヌル文字(\0)区切りで出力(スペースや特殊文字への対応)
>
>`xargs`コマンド
>- `-n10`：10ファイルずつ
>- `-P8`：8プロセス並列
>- `-0`：検索結果をヌル文字(\0)区切りで出力
>
 >`rsync`コマンド
 >- `-a`：再帰的コピー。また、シンボリックリンク、パーミッション、タイムスタンプ、グループ・オーナー情報などを保持
 >- `--files-from=-`：標準入力（`-`）で渡された10個のパスを、rsync の「転送リスト」として読む

または，以下を実行
```
rsync -aHAXW --remove-source-files --info=progress2 source-dir/ target-dir/
find source-dir -mindepth 1 -type d -empty -delete
```
