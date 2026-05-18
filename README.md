# Azure-Monitor-Alert-


## 概要
Azure VMに対して、Azure Monitorを利用した監視設定とAlert Ruleの作成を実施した学習用Repositoryです。

CPU使用率を監視し、設定した基準値を超えるとアラート表示され、Action Groupによりメール通知されることを確認しました。

---

# 構成図
```text
Internet
   ↓
vm-monitor-test
   ↓
Azure Monitor
   ↓
Metrics
   ↓
Alert Rule
   ↓
Action Group
   ↓
Email送信
```

---

# 使用サービス
| Service | Purpose |
|---|---|
| Resource Group | リソース管理 |
| Virtual Network | 仮想ネットワーク |
| Subnet | VM配置 |
| NSG | SSH通信制御 |
| Ubuntu VM | 監視対象 |
| Azure Monitor | メトリック監視 |
| Alert Rule | 異常検知 |
| Action Group | 通知管理 |
| Email Notification | メール通知 |

---

# 作成順序
1. Resource Group 作成
2. Virtual Network 作成
3. Subnet 作成
4. NSG 作成・SSH許可
5. Ubuntu VM 作成
6. SSH 接続
7. Azure Monitor 確認
8. Metrics 確認
9. CPU負荷テスト
10. Alert Rule 作成
11. Action Group 作成
12. メール通知確認

---

# Verification

### CPU Metrics

Azure Monitor にて CPU使用率上昇を確認。

---

### CPU Load Test

```bash
yes > /dev/null &
yes > /dev/null &
```

---

### Alert Fired

CPU使用率閾値超過時に Alert Rule 発火を確認。

---

### Email Notification

Action Group によりメール通知されることを確認。

---

### Recovery

CPU負荷停止後、CPU使用率低下を確認。

```bash
pkill yes
```

---

# 苦労したこと
## Percentage CPU が見つからなかった

### Cause
監視対象リソースを誤って選択。

### Resolution
VMリソースを選択し解決。

---

## メール通知が届かなかった

### Cause
Azure Monitor の通知反映遅延。

### Resolution
数分待機し解決。

---

## CPU使用率が下がらなかった

### Cause
バックグラウンドプロセスが残存。

### Resolution
`pkill yes` を実施し解決。

---

# 学んだこと
- Azure Monitor の基本
- Metrics の確認方法
- Alert Rule の作成
- Action Group の利用
- CPU監視
- メール通知設定
- Azure Monitor の反映遅延
- Linux による負荷テスト
- 監視・異常検知・復旧の流れ
