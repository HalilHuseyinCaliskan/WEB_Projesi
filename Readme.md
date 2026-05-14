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

**Oyunun Adı:** Space Blaster

**Oyun Bağlantısı:** 

**Oyunun Amacı ve Konsepti:** Space Blaster, HTML, CSS ve JavaScript kullanılarak geliştirilmiş, oyuncunun bir uzay gemisini kontrol ederek uzay boşluğunda ilerlediği web tabanlı interaktif bir oyundur. 

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

## 3. Oyun İçi Ekran Görüntüleri
<img width="1917" height="923" alt="Ekran görüntüsü 2026-05-13 123329" src="https://github.com/user-attachments/assets/517bf5e8-000a-4301-abee-a82f52829769" />
<img width="1912" height="896" alt="Ekran görüntüsü 2026-05-13 123355" src="https://github.com/user-attachments/assets/946fac8f-f8ce-4ba4-88a6-ae463cac8763" />
<img width="1917" height="930" alt="Ekran görüntüsü 2026-05-13 123403" src="https://github.com/user-attachments/assets/40e77d0e-44ec-4f4c-9927-9ab7d5be7d37" />
<img width="1916" height="923" alt="Ekran görüntüsü 2026-05-13 123416" src="https://github.com/user-attachments/assets/4efaa489-de38-42be-9d94-ce860b418420" />
<img width="1919" height="920" alt="Ekran görüntüsü 2026-05-13 123442" src="https://github.com/user-attachments/assets/46bf87f4-3179-40bb-9aa3-76e75a5edbc2" />

## 4. Assetler
https://kenney.nl/assets/space-shooter-extension

## 5. Proje Bağlantıları

- **Canlıya Alınmış Proje Bağlantısı:**

- **Oyun Bağlantısı:** [https://github.com/HalilHuseyinCaliskan/WEB_Projesi](https://halilhuseyincaliskan.github.io/WEB_Projesi/)

---

## Teşekkürler

Sorularınız?
