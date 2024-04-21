# ARKサーバーのインストール

- OS: Ubuntu 22.04.4 LTS
- size: Standard B2ms (2 vcpu 数、8 GiB メモリ)

## apt更新
```bash
sudo apt update && sudo apt upgrade
sudo apt install nano
```

## steamcmdインストール
```bash
sudo apt install software-properties-common
sudo add-apt-repository multiverse
sudo dpkg --add-architecture i386
sudo apt update
sudo apt install lib32gcc-s1 steamcmd
```

## ユーザー作成
```bash
sudo useradd -m steam
```

## ARKインストール
```bash
sudo su
steamcmd
login anonymous
force_install_dir /opt/steam/ARK/
app_update 376030 validate
quit
```

## サーバー設定変更
```bash
sudo nano /opt/steam/ARK/ShooterGame/Saved/Config/LinuxServer/GameUserSettings.ini

# 以下を追加
DifficultyOffset=1.000000
OverrideOfficialDifficulty=5.0
XPMultiplier=2.000000
TamingSpeedMultiplier=5.000000
DayCycleSpeedScale=0.5
NightTimeSpeedScale=4.0
ShowFloatingDamageText=true
alwaysNotifyPlayerLeft=True
alwaysNotifyPlayerJoined=True
```

## サービス化
https://qiita.com/AKYM21/items/bb52759eb51200a13d82

```bash
sudo nano /lib/systemd/system/arkserver.service
```

```bash
sudo chown -R steam:steam /opt/steam/
```

## サービス起動
```bash
sudo systemctl daemon-reload
sudo systemctl enable arkserver
sudo systemctl start arkserver
sudo systemctl status arkserver
```

## ポート設定
UDP 7777
UDP 27015

## セーブデータ
/opt/steam/ARK/ShooterGame/Saved/SavedArks/