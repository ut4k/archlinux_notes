# archlinux_notes  

archlinuxの自分用メモ。ASUS e200ha用。

## インストール系  

[ArchLinuxのインストール(3つのブート方式ごとの設定)](https://qiita.com/Gen_Arch/items/da296b7cbe5d87abc5a4)　　
ここらへんを参照

`UEFIブート`のほうを見る!

### パーティショニング

`cfdisk`だとなぜかファイルシステムの種類がNGで作れないのでインストール手順のリンクにあるように`pareted`を使ったほうがいいみたい。  

| ディレクトリ | 容量 | マウント | ファイルシステム |
| --- | --- | --- | --- |
| /boot | 200MiB | /dev/mmcblk0p1 | fat32 | 
| / | 10GiB | /dev/mmcblk0p2 | ext4 |
| /var | 8GiB | /dev/mmcblk0p3 | ext4 |
| /home | 残り全部 | /dev/mmcblk0p4 | ext4 |

`/boot`は`fat32`ファイルシステムを使わないとだめっぽい。  

`mkdir /mnt/boot`  
`mount /dev/mmcblk0p1 /mnt/boot`  
`mount /dev/mmcblk0p2 /mnt`
`mkdir /mnt/var`  
`mount /dev/mmcblk0p3 /mnt/var`
`mkdir /mnt/var`
`mount /dev/mmcblk0p4 /mnt/home`  

`/mnt`以下のフォルダは自分で分けるディレクトリをちゃんと`mkdir`しないといけない。

## 緊急

### エマージェンシーシェルに落とされたら

`ESC`連打しながら起動する。どうしようもなくなったらブートUSBさしてログイン。
`SysRq`キーとかもバインドしておくといざというときに使えるらしい。

## 音を出す

`alsa`パッケージを全部いれる。
ユーザーを`audio`グループにいれるのがポイント。

## 電源管理

ユーザーを`power`?のグループにいれる。と`sudo`なしで再起動できる。

## WM

dwmが軽くてよい。  
設定を変えたいときは`/download/dwm/src/dwm-6.x/config.h`(一番最下層のconfig.h）をいじってリコンパイルする。  
ここのconfig.h以外をいじっても効果なしみたい。  
再コンパイルは`mkpkg -efi`でやるとエラーなくいける。  

 - e : noextract。ソースファイルを展開しない。
 - f : force。上書き。
 - i : install。ビルドが成功したあとにインストール。
 
 
