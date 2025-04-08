📄 **Read this file in:**  
🇵🇱 Polski • 🇬🇧 English • 🇯🇵 日本語

⬇️ Scroll down to see all language versions.

---

# 🚀 Projekt IT: Zdalny dostęp do kamer IP za CGNAT-em (VPN vs. Port Forwarding)

## 🇵🇱 Opis projektu

Celem było przetestowanie różnych metod zdalnego dostępu do kamer IP znajdujących się za CGNAT-em. Przeprowadzono trzy warianty konfiguracji: tunel VPN WireGuard z bramą (Plan A), tunelowanie portu przez VPN (Plan B) oraz klasyczne przekierowanie portów RTSP (Plan C).

### 🛠️ Sprzęt i środowisko
- 💻 Komputer DELL XPS L702X z Ubuntu  
- 📡 Router Huawei H122-373 (T-Mobile, CGNAT)  
- 🌐 Router światłowodowy z publicznym IP  
- ☁️ Serwer AWS EC2 z WireGuard  
- 📷 Kamery IP: ścienna (Overmax 4.4), obrotowa (Overmax 3.3)  
- 📱 iPhone X (LTE) – zdalne testy

### 📊 Testowane scenariusze

| Plan | Metoda                     | Kamery           | Status    | Uwagi                                      |
|------|----------------------------|------------------|-----------|--------------------------------------------|
| A    | WireGuard z bramą (VPN)    | żadna            | ❌ Nieudany  | Rozjazd routingu, zawieszenia routera     |
| B    | Przekierowanie przez VPN   | żadna            | ❌ Nieudany  | RTSP nie przechodził przez `socat`        |
| C    | Port forwarding (światłowód)| obrotowa działa  | ✅ Udany     | Proste i skuteczne, brak potrzeby VPN     |

### 🗂️ Struktura projektu
```
rtsp-vpn-tunnel/
├── docker-compose.yml       # Konfiguracja kontenera rtsp-simple-server
├── mediamtx.yml             # Ścieżki do kamer RTSP
├── docs/                    # Dokumentacja techniczna projektu
└── screenshots/             # Zrzuty ekranu z testów i terminala
```

### 🖼️ Zrzuty ekranu

Zobacz [screenshots](./screenshots/) dla wizualnego potwierdzenia konfiguracji i działania.

### ✅ Status: Ukończony (Plan C)

---

## 🇬🇧 Project: Remote Access to IP Cameras Behind CGNAT (VPN vs. Port Forwarding)

This project compares three methods for accessing IP cameras located behind a CGNAT router: VPN gateway (Plan A), RTSP port tunneling over VPN (Plan B), and direct port forwarding (Plan C).

### 🛠️ Equipment and Environment
- 💻 Dell XPS L702X running Ubuntu  
- 📡 Huawei H122-373 router (T-Mobile, CGNAT)  
- 🌐 Fiber router with public IP  
- ☁️ AWS EC2 instance (WireGuard server)  
- 📷 IP cameras: wall (Overmax 4.4), PTZ (Overmax 3.3)  
- 📱 iPhone X with LTE – remote access testing

### 📊 Comparison Table

| Plan | Method                   | Cameras         | Status   | Notes                                  |
|------|--------------------------|------------------|----------|----------------------------------------|
| A    | VPN Gateway (WireGuard)  | none             | ❌ Failed   | Routing broken, router freeze          |
| B    | RTSP via VPN tunnel      | none             | ❌ Failed   | RTSP did not pass through `socat`      |
| C    | Direct Port Forwarding   | PTZ camera works | ✅ Success  | Simple and effective, no VPN required  |

### 🗂️ Project Structure
```
rtsp-vpn-tunnel/
├── docker-compose.yml       # RTSP proxy container configuration
├── mediamtx.yml             # RTSP stream definitions
├── docs/                    # Technical documentation
└── screenshots/             # Screenshots from terminal and iPhone tests
```

### 🖼️ Screenshots

See [screenshots](./screenshots/) for visual confirmation of setup and results.

### ✅ Status: Completed (Plan C)

---

## 🇯🇵 プロジェクト：CGNATの裏のIPカメラへのリモートアクセス（VPN vs. ポートフォワーディング）

CGNATの裏にあるIPカメラへリモートアクセスする3つの方法（VPNゲートウェイ、VPN経由のRTSPトンネル、直接ポート開放）を比較したプロジェクトです。

### 🛠️ 環境
- 💻 Ubuntu搭載のDell XPS L702X  
- 📡 T-Mobile（CGNAT）のHuawei H122-373ルーター  
- 🌐 公開IP付き光回線ルーター  
- ☁️ AWS EC2 + WireGuardサーバー  
- 📷 IPカメラ：Overmax 4.4（壁固定）、Overmax 3.3（回転型）  
- 📱 iPhone X（LTE） – リモート確認用

### 📊 比較表

| プラン | 方法                     | 動作カメラ       | 結果    | 注記                                  |
|--------|--------------------------|------------------|---------|----------------------------------------|
| A      | WireGuard VPNゲートウェイ | なし              | ❌ 失敗     | ルーティング問題＋ルーターフリーズ     |
| B      | VPNでRTSPトンネル        | なし              | ❌ 失敗     | socat + RTSPが不完全                   |
| C      | ポートフォワーディング    | 回転カメラ動作    | ✅ 成功     | シンプルかつ有効、VPN不要              |

### 🗂️ 構成
```
rtsp-vpn-tunnel/
├── docker-compose.yml       # RTSPサーバーのDocker構成
├── mediamtx.yml             # カメラのRTSP配信設定
├── docs/                    # 技術記録
└── screenshots/             # スクリーンショット
```

### 🖼️ スクリーンショット

[スクリーンショット](./screenshots/) を参照してください。

### ✅ ステータス：Plan Cで完了

---

### 👤 Author
**Mateusz Wawrzonkiewicz**  
[LinkedIn](https://www.linkedin.com/in/mateusz-wawrzonkiewicz-0a92a5163) • `cryptohyptron@gmail.com`  
📍 Poland • 🌐 Remote-friendly

