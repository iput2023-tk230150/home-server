# ハードウェア構成
## システム概要
- モデル: FUJITSU FMVWSD2B7
- OS: Ubuntu 24.04 LTS
- 用途: NASサーバ、サーバリソース監視、ゲーム用マルチサーバ（Minecraft）
## プロセッサ
- CPU: Intel Core i5-4590 @ 3.30GHz
- アーキテクチャ: 4コア/4スレッド
- キャッシュ: L1 256KB / L2 1MB / L3 6MB
## メモリ
- 容量: 16GB
- 規格: DDR3-1600 (PC3-12800)
- 構成: 4GB × 4枚
## ストレージ
- メインディスク: WD Blue SA510 1TB SSD (/dev/sdb) 
  - システムパーティション: /dev/sdb2 (930GB EXT4)
  - EFIパーティション: /dev/sdb1 (1GB FAT32)
- データディスク: Seagate ST2000DM008 2TB HDD × 2台 (/dev/sda, /dev/sdc) 
  - RAID1構成: /dev/md0 (1.8TB) → /mnt/raid1
## グラフィック
- GPU: NVIDIA GeForce GT 635 (GK208)
- 接続: PCI Express x16
## ネットワーク
- 有線LAN: Realtek RTL8111 Gigabit Ethernet (enp3s0)
- 無線LAN: Intel Wireless 7260 (wls3)
- VPN: Tailscale (P2P通信)
## マザーボード・チップセット
- チップセット: Intel B85 Express
- 世代: Intel 8 Series/C220 Series
## 接続デバイス
- USB: USB 3.0/2.0 対応 (xHCI/EHCI)
- 音声: Intel HDA + NVIDIA HDMI Audio
- カードリーダー: RTS5229 PCI Express
- 入力: Logitech USBレシーバー対応
## 運用構成
- SSH: Termius経由でリモート管理
- VPN: Tailscaleネットワーク内で運用
# 運用サービス一覧

## サービス概要

現在運用中のサービス。

## 1. Nextcloud
- **用途**: プライベートクラウドストレージ・ファイル同期
- **構成**: Docker (Apache + MySQL)
- **特徴**:
  - iPhoneからのHEIC写真アップロード対応
  - カスタムDockerfileでHEIF/HEICライブラリを追加
  - rcloneでファイル同期

## 2. Zabbix
- **用途**: サーバー監視・メトリクス収集
- **構成**: nginx + PHP-FPM
- **認証**: HTTPS必須
- **機能**:
  - システムリソース監視
  - アラート通知
  - パフォーマンス分析

## 3. Grafana
- **用途**: データ可視化・ダッシュボード
- **構成**: nginx リバースプロキシ経由
- **機能**:
  - メトリクス可視化
  - カスタムダッシュボード
  - データ分析

## 4. Minecraft サーバー群
- **用途**: ゲームサーバー運用
- **構成**: Docker Compose
- **サービス**:
  - **Paper Server**：Vanillaサーバ
  - **Mistgale Server**：RPG風アドベンチャーの配布ワールド
  - **Discord Bot**: Python製管理Bot（ステータス確認、起動、停止）

## ネットワーク構成

### SSL証明書
- **方式**: Tailscale cert (Let's Encrypt)
- **ドメイン**: ubuntu-server.dab-ladon.ts.net
- **自動更新**: 対応

### アクセス制御
- **対象**: Tailscaleネットワーク内のみ
- **許可IP**: 
  - 100.103.135.58 (サーバー)
  - 100.64.0.0/10 (Tailscaleネットワーク全体)

### nginx設定
- **HTTP → HTTPS リダイレクト**: 有効
- **リバースプロキシ**: Grafana, Nextcloud
- **PHP-FPM**: Zabbix

## データ管理

### Nextcloud
- **データディレクトリ**: `./nextcloud_data`
- **データベース**: MySQL 8.0 (`./dbdata`)
- **HEIC対応**: カスタムDockerfile

### Minecraft
- **Paper データ**: `./paper`
- **Mistgale データ**: `./mistgale`
- **設定ファイル**: `./opt`, `./discordsrv-config`
