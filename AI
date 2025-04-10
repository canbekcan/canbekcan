Süper! O zaman sana özel, **uçtan uca bir dağıtık AI eğitim ve servis altyapısı** kuracağız. Aşağıda sistemin tüm yapı taşlarını bulacaksın. Kurulumu kademeli vereceğim ve her adımı birlikte ilerleyebileceğiz. Hazırsan başlıyoruz.

---

## 🎯 Hedefler:
- 14 Windows 10 bilgisayarı birlikte çalıştırmak.
- Bazıları GPU'lu, bazıları değil.
- Birden fazla modeli paralel ve/veya ardışık olarak eğitmek.
- Eğitilen modelleri yerel sunucuda çalıştırmak (inference için).
- Tüm süreci uzaktan yönetmek.

---

## 🧱 MİMARİ YAPI PLANI

### 1. 📡 Ağ & Uzak Erişim
### 2. ⚙️ Ortam Kurulumu (Python + Kütüphaneler)
### 3. ☁️ Dağıtık Eğitim Framework’ü (Ray + PyTorch)
### 4. 🚀 Model Eğitimi Otomasyonu (Çoklu model + log + GPU dağılımı)
### 5. 🧠 Model Servisi (Yerel sunucuda inference çalıştırmak)
### 6. 🎛️ Yönetim Paneli veya Komut Scriptleri

---

## 1. 📡 AĞ & UZAK ERİŞİM

### 🔗 Tailscale Kurulumu (VPN ile tüm makineleri aynı ağda görmek)
#### Adımlar:
- [https://tailscale.com/download](https://tailscale.com/download) → Her Windows 10 bilgisayara indirip kur.
- Tek bir Google hesabıyla giriş yap (her cihazı listeleyecek).
- Kurulumdan sonra IP’ler şöyle görünecek:
  - PC1: `100.x.x.x`
  - PC2: `100.x.x.x` (gibi)

### 🧪 Test:
- PC1’den PC2’ye `ping` at → çalışıyor mu?
- `ssh username@100.x.x.x` bağlantısı yapılabiliyor mu?

📝 SSH bağlantısını Windows'a kurmak için OpenSSH Server ve istemcisi etkinleştirilmeli. Gerekirse PowerShell ile bunu da yapabiliriz.

---

## 2. ⚙️ ORTAM KURULUMU (Anaconda + Ray + PyTorch)

### 🐍 Python Ortam Kurulumu Script (Windows için `.bat`)
```bat
:: miniconda kurulu varsayalım
conda create -n ai_env python=3.10 -y
conda activate ai_env
pip install torch torchvision torchaudio --extra-index-url https://download.pytorch.org/whl/cu118
pip install ray[default] numpy pandas matplotlib
```

GPU varsa CUDA destekli PyTorch kurulur, yoksa CPU versiyonu kurulur.

### 🧪 Her makinede:
- `conda activate ai_env`
- `python -c "import torch; print(torch.cuda.is_available())"` → True/False çıkmalı

---

## 3. ⚡ RAY DAĞITIK FRAMEWORK KURULUMU

### 📍 Yapı
- 1 Head Node → kontrol merkezi
- 13 Worker Node → işçi makineler

### 🔌 Ray Başlatma Komutları

#### ➕ Head Node (örneğin PC1)
```bash
ray start --head --port=6379
```

#### ➕ Worker (örneğin PC2, PC3...)
```bash
ray start --address='HEAD_NODE_IP:6379'
```

Tüm makineler Ray cluster’a bağlanmış olur.

---

## 4. 🚀 ÇOKLU MODEL EĞİTİMİ (Paralel)

### 📁 Örnek klasör yapısı:
```
ai_cluster/
├── models/
│   ├── model1.py
│   ├── model2.py
├── train.py
├── config/
│   ├── model1.yaml
│   ├── model2.yaml
```

### 🧠 `train.py` örnek kod:
```python
import ray
import yaml
from model1 import train_model1
from model2 import train_model2

@ray.remote(num_gpus=1)
def train_with_gpu(func, config):
    return func(config)

@ray.remote
def train_with_cpu(func, config):
    return func(config)

def main():
    ray.init(address='auto')
    with open("config/model1.yaml") as f:
        cfg1 = yaml.safe_load(f)
    with open("config/model2.yaml") as f:
        cfg2 = yaml.safe_load(f)

    jobs = [
        train_with_gpu.remote(train_model1, cfg1),
        train_with_cpu.remote(train_model2, cfg2),
    ]

    results = ray.get(jobs)
    print(results)

if __name__ == "__main__":
    main()
```

---

## 5. 🧠 MODEL SERVİSİ (Yerel sunucuda inference çalıştırmak)

Eğitilen modelleri saklayıp, inference için sunucu kurabiliriz:

### 💡 FastAPI ile REST API sunucu
```bash
pip install fastapi uvicorn
```

#### `server.py`:
```python
from fastapi import FastAPI
import torch
from model1 import MyModel

app = FastAPI()
model = MyModel()
model.load_state_dict(torch.load("model1.pth"))
model.eval()

@app.get("/predict")
def predict(x: float):
    with torch.no_grad():
        result = model(torch.tensor([[x]]))
    return {"result": result.item()}
```

#### Başlatmak için:
```bash
uvicorn server:app --host 0.0.0.0 --port 8000
```

---

## 6. 🎛️ YÖNETİM PANELİ VE KOMUTLAR

Eğer GUI istiyorsan:
- Basit bir web arayüz (Flask + HTML)
- Scriptleri çalıştıran butonlar
- Her bilgisayardan log toplayan sistem

Veya CLI (komut satırı scriptleri):
- `start_cluster.bat`
- `stop_cluster.bat`
- `train_all_models.py`
- `upload_model_to_server.py`

---

## 🔄 Günlük Akış Örneği
1. Tailscale ile makineler açık ve bağlı.
2. Ana bilgisayarda `ray start --head` ile başlatılır.
3. Diğerleri `ray start --address=...` ile bağlanır.
4. `train.py` script’i çalıştırılır → modeller eğitilir.
5. Eğitilen modeller `.pth` olarak sunucuya aktarılır.
6. Sunucuda API açılır → sonuç alınır.

---

## 📥 SONRAKİ ADIM
Şimdi senden birkaç bilgi alırsam, sana **tam otomatik script seti** ve örnek model dosyaları hazırlayabilirim:

1. Hangi framework’ü kullanmak istiyorsun? (PyTorch / TensorFlow)
2. Elinde şu an hangi AI modelleri veya eğitim verisi var?
3. Model servisinde (inference) kullanacağın örnek senaryo nedir?
4. Grafik arayüz ister misin, yoksa komut satırı yeterli mi?

Bunlara göre sistemin ilk versiyonunu 100% sana özel kodlayacağım 💻💡
