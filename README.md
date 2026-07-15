# Mevsimsel Talep Belirsizliği Altında Akıllı Depo Yönetimi 📊🚀
### Klasik ve Derin Pekiştirmeli Öğrenme Yöntemlerinin Karşılaştırmalı Performans Analizi

Bu proje, sınırlı kapasiteli bir depoda mevsimsel talep belirsizliği altında günlük sipariş miktarı belirleme (envanter optimizasyonu) problemini ele almaktadır. Proje kapsamında aynı ortam üzerinde üç farklı senaryo eğitilmiş ve karşılaştırılmıştır:
1. **Tablo Q (Mevsimden Habersiz)** — *Ablasyon Koşulu* (Durum: Stok seviyesi)
2. **Tablo Q (Mevsim-Farkında)** — *Klasik RL* (Durum: Stok, Mevsim)
3. **DQN (Mevsim-Farkında)** — *Derin RL* (Durum: Standartlaştırılmış stok ve döngüsel sin/cos zaman kodlaması)

---

## 📌 Proje Özeti & Öne Çıkanlar

* **Gerçek Veriyle Kalibrasyon:** Ortamdaki mevsimsel talep parametreleri varsayımsal değildir. **UCI Online Retail** veri setindeki (Chen vd., 2012; 531.285 işlem) gerçek satış oranları korunarak genel ortalama $\lambda = 3.0$ olacak şekilde Poisson dağılımına kalibre edilmiştir.
* **Yumuşak Zaman Temsili (DQN):** DQN ajanına mevsim geçişlerini yumuşak ve sürekli bir biçimde aktarabilmek adına zaman bilgisi $\sin(2\pi \cdot \text{gün}/365)$ ve $\cos(2\pi \cdot \text{gün}/365)$ sinyalleriyle sürekli durum vektörü olarak beslenmiştir.
* **Yorumlanabilir Politika:** DQN ajanı, gerçek verilerdeki yılbaşı alışverişi zirvesini (4. çeyrek, $\lambda = 4.24$) kendiliğinden analiz ederek, son çeyreğe stok biriktirerek girme biçiminde anlamlı bir "hedef stok" (base-stock) politikası geliştirmiştir.

---

## 📈 Karşılaştırmalı Performans Sonuçları (30 Bağımsız Test Yılı)

Ajanlar eğitildikten sonra, keşif tamamen kapatılarak ($\epsilon = 0$, greedy politika) 30 bağımsız simülasyon yılında test edilmiştir:

| Koşul | Ortalama Yıllık Ödül | Standart Sapma (Std) | Minimum Ödül | Maksimum Ödül |
| :--- | :---: | :---: | :---: | :---: |
| **Tablo Q (Mevsimsiz)** | 4125.1 | 230.0 | 3622 | 4537 |
| **Tablo Q (Mevsim-Fark.)** | 4697.1 | 243.4 | 4157 | 5163 |
| **DQN (Mevsim-Fark.)** | **4816.2** | 243.6 | 4375 | 5733 |

### Performans Kazanım Analizi:
* **Temsil Etkisi (%13.9 Artış):** Mevsim bilgisinin durum uzayına eklenmesi, ajanın Markov özelliğini korumasını sağlayarak ortalama ödülü 4125'ten 4697'ye çıkarmıştır.
* **Yöntem Etkisi (%2.5 Artış):** Aynı bilgiye sahipken klasik tablodan derin fonksiyon yaklaştırımına (DQN) geçmek performansı 4816'ya yükseltmiştir.
* **Toplam İyileşme:** Başlangıç (ablasyon) noktasına göre **%16.8 net kazanç** elde edilmiştir.

---

## 🛠️ Kullanılan Teknolojiler

* **Programlama Dili:** Python 3
* **Derin Öğrenme Kütüphanesi:** PyTorch (DQN mimarisi ve optimizasyonu için)
* **Veri Analizi & Simülasyon:** NumPy, Pandas, Matplotlib, PIL

---

## 📁 Dosya Yapısı

* `AkilliDepo_Final_QL_vs_DQN_v2.ipynb`: Ortam tanımlamalarını, Q-Learning & DQN ajanlarını, eğitim döngülerini ve görselleştirme araçlarını içeren ana Jupyter Notebook dosyası.
* `learning_curves.png`: Ajanların eğitim süreçlerindeki ödül gelişim grafiklerini gösteren görsel.
* `comparison_bar.png`: Test sonuçlarının standart sapmalarıyla birlikte karşılaştırma grafiği.
* `policy_heatmap.png`: DQN ajanının farklı mevsim ve stok seviyelerinde öğrendiği sipariş politikasının ısı haritası.
* `dqn_simulasyon.gif`: Eğitilen DQN ajanının 1 yıllık akıllı depo yönetim simülasyonunun animasyonu.

---

## 🚀 Kurulum ve Çalıştırma

### 1. Depoyu Klonlayın
```bash
git clone [https://github.com/nvncvsogl/akilliDepolamaQLvsDQL.git](https://github.com/nvncvsogl/akilliDepolamaQLvsDQL.git)
cd akilliDepolamaQLvsDQL
