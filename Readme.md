---
marp: true
theme: default
paginate: true
---

# WEB Tabanlı Programlama Dersi Proje Sunumu
## Space Blaster Oyunu

**Hazırlayanlar:**
- Alperen Namlı (Öğrenci No: 23360859074)
- Halil Hüseyin Çalışkan (Öğrenci No: 23360859001)
- Muhammed Emin Uysal (Öğrenci No: 23360859045)
- Nurullah Harun Köse (Öğrenci No: 24360859003)
- Recep Doruk (Öğrenci No: 23360859077)

---

## 1. Hedeflenen Oyun Projesi ve Temel Mekanikler

**Oyunun Adı: Space Blaster
**Oyun Bağlantısı :
**Oyunun Amacı ve Konsepti: Space Blaster, HTML, CSS ve JavaScript kullanılarak geliştirilmiş, oyuncunun bir uzay gemisini kontrol ederek uzay boşluğunda ilerlediği web tabanlı interaktif bir oyundur. 

**Temel Oyun Mekanikleri ve Teknik Detaylar:**

- **Gelişmiş Hareket Sistemi:** 
  - Oyuncu, uzay gemisini yön tuşları veya "W, A, S, D" tuşlarını kullanarak yatay ve dikey eksende özgürce hareket ettirebilir.
  - Hareket hesaplamaları, farklı ekran boyutlarında (responsive) sorunsuz çalışabilmesi için piksel yerine yüzdelik değerler (`%`) üzerinden yapılmaktadır.
  - CSS özelliği sayesinde uzay gemisinin hareketleri keskin atlamalar yerine yumuşak ve akıcı bir şekilde gerçekleşir.

- **Dinamik ve Döngüsel Arka Plan Animasyonu:** 
  - Uzay hissiyatını gerçekçi kılmak için 10 farklı uzay görselinden oluşan bir animasyon kurgulanmıştır.
  - CSS kullanılarak 80 saniyelik sonsuz bir döngü (infinite) oluşturulmuş ve görsellerin yumuşak bir şekilde birbiri ardına gelmesi sağlanmıştır.
  - Z-index katmanlandırması kullanılarak arka plan en alt katmanda, uzay gemisi ise üst katmanda tutulmuştur.

- **Kullanıcı Etkileşimi ve Oyun Durumu (State) Yönetimi:** 
  - Oyun, ekrandaki "Oyuna Başla" butonuna tıklanmasıyla başlar. Başlangıçta inaktif olan klavye kontrolleri, bu butona basıldığında `oyun_basladi = true` değişkeni ile aktif hale gelir.
  - Klavye dinleyicisi (event listener), `keydown` olaylarını anlık olarak yakalar. Kullanıcının "Caps Lock" açık unutma ihtimaline karşı basılan tuşlar otomatik olarak küçük harfe (`toLowerCase()`) çevrilerek kontrol hatalarının önüne geçilir.
  - Tıklanan "Oyuna Başla" butonu, akıcılığı bozmamak için oyun başladığında gizlenir .

---

## 2. Grup Üyelerinin Sorumlulukları

- **Alperen Namlı:** Market sistemi entegrasyonu, oyun içi ekonomi (altın toplama mekaniği), ses efektlerinin (müzik, çarpışma, lazer) projeye dahil edilmesi ve gemi geliştirmeleri (mühendis, tahsildar yetenekleri).
- **Recep Doruk:** Oyun içi özel güçlerin (power-up: üçlü mermi, zaman yavaşlatma, ateş hızı artışı) kodlanması, kedi toplama görevleri ve seviye atlama (hedef gezegen) mekaniklerinin tasarımı.
- **Muhammed Emin Uysal:** Uzay gemisinin hareket dinamikleri (ivme ve sürtünme hesaplamaları), kullanıcı arayüzü (UI) tasarımı, can barı ve bilgi panellerinin ekrana dinamik olarak yansıtılması.
- **Halil Hüseyin Çalışkan:** Oyun döngüsü (game loop) yönetimi, nesneler arası çarpışma algılama (collision detection) algoritmaları ve meteor/partikül efekt sisteminin entegrasyonu.
- **Nurullah Harun Köse:** Projenin temel HTML/CSS mimarisinin oluşturulması, proje sunum/raporunun hazırlanması.

---

## 3. Proje Bağlantıları

- **Canlıya Alınmış Proje Bağlantısı :

- **GitHub Repo Bağlantısı: https://github.com/HalilHuseyinCaliskan/WEB_Projesi

---

## Teşekkürler

Sorularınız?
