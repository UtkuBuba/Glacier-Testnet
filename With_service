# Systemd Servis Dosyası ile Glacier Verifier Node Çalıştırma

Bu rehber, **screen** yerine daha stabil bir yöntem olan **systemd servis dosyası** ile Glacier Verifier Node’u çalıştırmayı açıklar. 

---

## **Adımlar**

### **1. Servis Dosyasını Oluşturun**
Servis dosyasını `/etc/systemd/system` dizininde oluşturun:
```bash
sudo nano /etc/systemd/system/verifier.service
```

---

### **2. Servis Dosyasının İçeriği**
Aşağıdaki içeriği dosyaya yapıştırın ve kaydedin:

```ini
[Unit]
Description=Glacier Verifier Node
After=network.target

[Service]
Type=simple
User=root
WorkingDirectory=/root
ExecStart=/root/verifier_linux_amd64
Restart=always
RestartSec=5

[Install]
WantedBy=multi-user.target
```

- **`WorkingDirectory=/root`**: Çalıştırmak istediğiniz dosyanın bulunduğu dizin (örneğin, `/root`).
- **`ExecStart=/root/verifier_linux_amd64`**: Çalıştırılacak dosyanın tam yolu.

---

### **3. Servisi Etkinleştirme ve Başlatma**
Servisi etkinleştirin ve başlatın:
```bash
sudo systemctl daemon-reload
sudo systemctl enable verifier.service
sudo systemctl start verifier.service
```

---

### **4. Servis Durumunu Kontrol Etme**
Servisin çalışıp çalışmadığını kontrol edin:
```bash
sudo systemctl status verifier.service
```

Çıktı şu şekilde olmalıdır:
```plaintext
● verifier.service - Glacier Verifier Node
   Loaded: loaded (/etc/systemd/system/verifier.service; enabled)
   Active: active (running) since ...
```

---

### **5. Servisi Durdurma veya Yeniden Başlatma**
- Servisi durdurmak için:
  ```bash
  sudo systemctl stop verifier.service
  ```
- Servisi yeniden başlatmak için:
  ```bash
  sudo systemctl restart verifier.service
  ```

---

### **6. Logları Görüntüleme**
Çalışma sırasında oluşan logları görmek için:
```bash
journalctl -u verifier.service
```

---

## **Notlar**
- Servis dosyası sistemin bir parçası olduğu için sunucu yeniden başlatıldığında otomatik olarak çalışır.
- `Restart=always` seçeneği sayesinde, servis hata durumunda otomatik olarak yeniden başlatılır.

Eğer kurulum sırasında sorun yaşarsanız, detaylı hata mesajını paylaşarak yardım alabilirsiniz.
