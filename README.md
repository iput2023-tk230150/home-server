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
