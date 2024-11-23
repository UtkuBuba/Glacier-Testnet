# Glacier Verifier Node Kurulum Rehberi

Bu rehber, **Glacier Verifier Node**'u Linux CLI üzerinde kurmanız ve çalıştırmanız için adım adım talimatlar içermektedir.

---

## **Donanım Gereksinimleri**

### Minimum:
- 1+ Çekirdek CPU
- 2GB RAM
- 4 MBit/sn internet bağlantısı

### Önerilen:
- 2+ Çekirdek CPU
- 4GB+ RAM
- 8+ MBit/sn internet bağlantısı

> Not: Verifier node'un sabit IP adresine veya büyük bir depolama alanına ihtiyacı yoktur. Yazılım ve yapılandırma için 100MB’den az bir alan yeterlidir.

---

## **1. Ortam Hazırlığı**

### **Sistemi Güncelleme**
```bash
sudo apt-get update && sudo apt-get upgrade -y
```

### **Gerekli Araçları Kurma**
```bash
sudo apt-get install -y curl wget screen
```

---

## **2. OpBNB Testnet için Hazırlık**

### **Adımlar:**
1. **Cüzdan Oluşturun:** MetaMask veya benzeri bir cüzdan kullanabilirsiniz.
2. **OpBNB Testnet’e Bağlanın:** [OpBNB Testnet RPC Ayarları](https://chainlist.org/chain/5611).
3. **tBNB Tokenları Alın:** [OpBNB Faucet](https://thirdweb.com/opbnb-testnet) kullanarak test tokenları alın.
4. **Private Key’i Dışa Aktarın:**
   - MetaMask Ayarları'na gidin.
   - **Ayarlar > Güvenlik ve Gizlilik > Private Key'i Dışa Aktar** yolunu izleyin.

---

## **3. Node Binary ve Config Dosyasını İndirin**

### **Binary Dosyasını İndirme**
```bash
wget https://github.com/Glacier-Labs/node-bootstrap/releases/download/v0.0.1-beta/verifier_linux_amd64
```

### **Config Template İndirme**
```bash
wget https://glacier-labs.github.io/node-bootstrap/config.yaml
```

---

## **4. Config Dosyasını Düzenleme**

`nano config.yaml` komutu ile yaml dosyasını açarak şu şekilde yapılandırın:
```yaml
Http:
  Listen: "127.0.0.1:10801"
Network: "testnet"
RemoteBootstrap: "https://glacier-labs.github.io/node-bootstrap/"
Keystore:
  PrivateKey: "YourPrivateKey"
TEE:
  IpfsURL: "https://greenfield.onebitdev.com/ipfs/"
```

**YourPrivateKey** kısmını kendi private key’inizle değiştirin.

---


## **5. Node’u Arka Planda Çalıştırma**

Node’un kesintisiz çalışmasını sağlamak için `screen` kullanabilirsiniz:

1. **Screen Kurulumu:**
   ```bash
   sudo apt-get install screen
   ```

2. **Screen Oturumu Başlatma:**
   ```bash
   screen -S glacier-node
   ```

3. **Node’u Screen İçinde Çalıştırma:**
   ```bash
   ./verifier_linux_amd64
   ```

4. **Ekran Oturumunu Arka Plana Alma:**
   `Ctrl-a` ardından `d` tuşlarına basın.

5. **Screen Oturumuna Geri Dönme:**
   ```bash
   screen -r glacier-node
   ```

---

## **6. Node Durumunu Kontrol Etme**

Node’un online durumunu aşağıdaki bağlantıdan kontrol edebilirsiniz:
[Glacier Node Explorer](https://testnet.nodes.glacier.io/status)

---

## **7. Sözleşme Adresleri**

### **NodeCtrl Contract**
[0x1F59347c5998a8Bb5E5f3ba8ec20c030CA5dd1D2](https://testnet.opbnbscan.com/address/0x1F59347c5998a8Bb5E5f3ba8ec20c030CA5dd1D2)

### **License NFT Contract**
[0xb813466384c915280f5b8ffa005fcc2cb5cf5b87](https://opbnb-testnet.bscscan.com/token/0xb813466384c915280f5b8ffa005fcc2cb5cf5b87)

---

## **Ek Notlar**
- Node lisans NFT'si, node’unuz ilk defa smart contract üzerinde kaydedildiğinde otomatik olarak mint edilir.
- OpBNB Testnet üzerinde yeterli tBNB'ye sahip olduğunuzdan emin olun.

---
