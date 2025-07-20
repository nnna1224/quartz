---
tags:
  - setup
  - setting
  - archlinux
  - WSL
---
## 1. pacman-keyの初期化と鍵の設定
```
pacman-key --init
pacman-key --populate archlinux
```

## 2. 基本パッケージのインストール
```
pacman -Syyu
pacman -S base base-devel git wget reflector neovim openssh
```

## 3. デフォルトエディタの設定
```
export EDITOR="$(which nvim)"
```

## 4. reflectorでミラーリストを最適化
```
reflector --country Japan --age 12 --protocol https --sort rate --save /etc/pacman.d/mirrorlist
```

## 5. ユーザ設定
以下のコマンドでrootユーザのパスワードを設定する．
```
passwd
```

続いて，以下のコマンドで一般ユーザを追加する．
このとき，`sudo`を使用できるようwheelグループに追加しておく．
※ `{USERNAME}`は任意のユーザ名に置き換える．
```
useradd -m -G wheel -d /home/{USERNAME} {USERNAME}
passwd {USERNAME}
```
> [!INFO] オプションの説明
>* -m： ホームディレクトリ作成
>* -G グループ名： グループに追加
>* -d ホームディレクトリのパス： ホームディレクトリのパスを指定

## 6. sudo権限の付与
`sudoedit /etc/sudoers`を実行して`/etc/sudoers`ファイルを開き，以下のコメントアウトを解除する．
```
%wheel ALL=(ALL:ALL) ALL
```

## 7. ロケールの設定
`sudoedit /etc/locale.gen`で`/etc/locale.gen`を開き，以下の行をコメントアウトを解除する．
```
ja_JP.UTF-8 UTF-8
```
 
保存してエディタを抜けた後，以下を実行する．
```
locale-gen
echo LANG=ja_JP.UTF-8 > /etc/locale.conf
```

## 8. WSL特有の設定
`sudoedit /etc/wsl.conf`で`/etc/wsl.conf`を開き，以下を記述する．
※ `{USERNAME}`は先ほど作成したユーザ名に置き換える．
```
[boot]
systemd = true

[user]
default={USERNAME}
```

## 9. yayのインストール
AUR(Arch User Repository)インストールのため，以下のコマンドを実行してヘルパーであるyayをインストールしておく．
```
git clone https://aur.archlinux.org/yay.git
cd yay
makepkg -si
cd ..
rm -rf yay
```


以上でWSLにおけるArch Linuxの設定は完了である．
以降はSSH設定などを行う．