https://gemini.google.com/share/ee0ccc975c53


prompt:

<!DOCTYPE html>



<html lang="tr">



<!-- Türkçe karakter kullanımında sıkıntıları engellemek için lang="tr" olarak ayarlandı. -->



<head>



    <meta charset="UTF-8">

    <meta name="description" content="Bu proje WEB Tabanlı Programlama Dersi kapsamında yapılmıştır.">

    <meta name="author" content="Alperen Namlı, Halil Hüseyin Çalışkan, Muhammed Emin Uysal, Nurullah Harun Köse, Recep Doruk">

    <meta name="keys" content="HTML,CSS,Javascript,Oyun">



    <!-- UTF-8 ayarı yapılıp karakter yazımından kaynaklaı hatalar engellendi.

    Proje de kimlerin görev aldığı ve projenin ne hakkında olduğu meta etiketi içerisinde belirtildi.

    -->



    <style>





        body{

            margin: 0px;

            padding: 0px;

        }

        /*Genellikle web sitelerinde kullanıldığı için ve hizalamayı  sıfırdan aldığı için tercih edildi.*/

        .resimler{

            display: none;

        }

        /* Resimleri tutan div'in gözükmemesi için yapıldı.*/



        .arka_plan_animasyon{



            width: 100%;

            height: 100vh;

            background-size: cover;

            position: absolute;

            top:0;

            left:0;

            animation: animasyon_yap 80s infinite;



        }

        /* Öyle bir div tanımlandı ki bu div'in bouyutu tüm sayfayı kaplıyor ve (position:absolute) diyerek manuel ayarlamalar yapabiliyoruz.*/

        /* Arka planın belirli bir sıraya göre toplam süresi 80 saniye olacak şekilde sürekli değişmesi için animasyon tanımlandı.*/



        @keyframes animasyon_yap{



            0%, 8% {

                background-image: url(images/uzay1.png);

            }

            10%, 18% {

                background-image: url(images/uzay2.png);

            }

            20%, 28% {

                background-image: url(images/uzay3.png);

            }

            30%, 38% {

                background-image: url(images/uzay4.png);

            }

            40%, 48% {

                background-image: url(images/uzay5.png);

            }

            50%, 58% {

                background-image: url(images/uzay6.png);

            }

            60%, 68% {

                background-image: url(images/uzay7.png);

            }

            70%, 78% {

                background-image: url(images/uzay8.png);

            }

            80%, 88% {

                background-image: url(images/uzay9.png);

            }

            90%, 94% {

                background-image: url(images/uzay10.png);

            }

            96%, 100% {

                background-image: url(images/uzay1.png);

            }

        }

        /*Animasyonun temel görevi toplamda 10 farklı uzay resmini belirli bir süre arka planda tutarak yer değiştirmesidir bunun için zaman aralıkları belirlenir.*/



        .buton1{

            position: absolute;

            width: 10%;

            height: 10vh;

            top: 50%;

            left: 50%;

            transform: translate(-50%,-50%);

            border-radius: 15px;

            background-color: #7CAAE6;

            font-weight: bold;

            font-family: 'Times New Roman', Times, serif;

            font-size: large;

            transition: all 0.4s;

        }

        /*Buton manuel olarak hizalanır ve konumu sayfanın tam ortasına getirilir. Standart CSS özellikler eklenir(köşe yumuşatma,renk ayarlama vb..)*/



        .buton1:hover{

            cursor: pointer;

            background-color: #3B8EFF;

            transform: translate(-50%,-50%) scale(1.2);



        }

        /*Butonun üzerine gelince butonda değişimler olur (renk ve boyut) bu değişimlerin süresi ise transition özelliği ile sağlanır.*/



   



    </style>

   

    <script>

// 1. Değişkenleri Tanımlayalım

let canvas, ctx;

let oyunDevamEdiyor = false;



// Oyuncu (roket) Objesi

let roket = {

            x: 100,

            y: 100,

            vx: 0, // Yatay hız

            vy: 0, // Dikey hız

            ivme: 0.4, // Hızlanma gücü

            surtunme: 0.96, // Yavaşlama oranı

            boyut: 80,

            can: 100,

            maksCan: 100

        };

let toplananKediler = 0;

let hedefKediSayisi = 30;

let seviye = 1;

let kediler = [];

const kediGorseli = new Image();

        kediGorseli.src = 'images/kedi.png';

const roketGorseli = new Image();

        roketGorseli.src = 'images/roket.png'; // Yüklediğin dosya adı

        roket.resim = roketGorseli;

// Hedef (Gezegen) Objesi

const gezegenGorseli = new Image();

gezegenGorseli.src = 'images/gezegen.png'; // images klasörüne bir gezegen resmi eklemelisin



let hedef = {

    y: -450, // Başlangıçta ekranın dışında

    boyut: 400,

    mesafe: 3000, // Hedefe ulaşmak için katedilmesi gereken yol

    gorunurMu: false

};

// Basılan tuşları takip etmek için bir liste

let tuslar = {};

let meteorlar = [];

let meteorHizi = 0.5;

let partikuller = []; // Partikül sistemi dizisi

let yildizlar = [];    // Dinamik yıldızlar dizisi

let sarsintiSuresi = 0; // Ekran sallanması için sayaç

const meteorGorseli = new Image();

meteorGorseli.src = 'images/meteor.png';



// 2. Butona tıklandığında çalışacak fonksiyon

function buton_giris() {

    // Menü butonunu gizle

    var buton = document.getElementById("buton_id_1");

    buton.style.display = "none";



    // Canvas (Oyun alanı) oluştur ve ekrana ekle

    canvas = document.createElement("canvas");

    ctx = canvas.getContext("2d");

   

    // Canvas'ı tüm ekranı kaplayacak şekilde ayarla

    canvas.width = window.innerWidth;

    canvas.height = window.innerHeight;

    canvas.style.position = "absolute";

    canvas.style.top = "0";

    canvas.style.left = "0";

    canvas.style.zIndex = "10"; // Arka plan animasyonunun üstünde durması için

   

    document.body.appendChild(canvas);

    // EKRAN BOYUTU DEĞİŞİNCE CANVAS'I GÜNCELLE

for(let i=0; i<100; i++) {

                yildizlar.push({

                    x: Math.random() * canvas.width,

                    y: Math.random() * canvas.height,

                    hiz: Math.random() * 3 + 1,

                    boyut: Math.random() * 2

                });

            }



    window.addEventListener('resize', function() {

        canvas.width = window.innerWidth;

        canvas.height = window.innerHeight;

    });

   

    // 3. Roketin başlangıç pozisyonunu ekranın ortası yap

            roket.x = canvas.width / 2 - roket.boyut / 2;

            roket.y = canvas.height / 2 - roket.boyut / 2;



    // Klavye dinleyicilerini başlat

    window.addEventListener("keydown", (e) => { tuslar[e.key] = true; });

    window.addEventListener("keyup", (e) => { tuslar[e.key] = false; });



    // Oyun döngüsünü başlat

    oyunDevamEdiyor = true;

    oyun_dongusu();

}

// Partikül Oluşturma Fonksiyonu

        function partikulOlustur(x, y, renk, adet) {

            for (let i = 0; i < adet; i++) {

                partikuller.push({

                    x: x,

                    y: y,

                    vx: Math.random() * 6 - 3,

                    vy: Math.random() * 6 - 3,

                    omur: 1.0,

                    renk: renk

                });

            }

        }

       

function kediOlustur() {

     let boyut = 50;

     let x = Math.random() * (canvas.width - boyut);

      kediler.push({

         x: x, y: -boyut,

          boyut: boyut,

            hiz: Math.random() * 1 + 2

            });

        }

function meteorOlustur() {

    let boyut = Math.random() * (80 - 40) + 40; // 40px ile 80px arası rastgele boyut

    let x = Math.random() * (canvas.width - boyut);

   

    meteorlar.push({

        x: x,

        y: -boyut, // Ekranın hemen dışından başlasın

        boyut: boyut,

        hiz: Math.random() * 3 + meteorHizi // Her meteorun hızı biraz farklı olsun

    });

}



// 3. Ana Oyun Döngüsü (Her saniye 60 kez çalışır)

function oyun_dongusu() {

    if (!oyunDevamEdiyor) return;



    guncelle();

    ciz();



    requestAnimationFrame(oyun_dongusu);

}



function guncelle() {

            // Momentum Hareketi

            if (tuslar["ArrowUp"] || tuslar["w"]) roket.vy -= roket.ivme;

            if (tuslar["ArrowDown"] || tuslar["s"]) roket.vy += roket.ivme;

            if (tuslar["ArrowLeft"] || tuslar["a"]) roket.vx -= roket.ivme;

            if (tuslar["ArrowRight"] || tuslar["d"]) roket.vx += roket.ivme;



            roket.vx *= roket.surtunme;

            roket.vy *= roket.surtunme;

            roket.x += roket.vx;

            roket.y += roket.vy;



            // Egzoz Partikülleri

            if (Math.abs(roket.vx) > 0.5 || Math.abs(roket.vy) > 0.5) {

                partikulOlustur(roket.x + roket.boyut / 2, roket.y + roket.boyut - 10, "orange", 1);

            }



            // Ekran Sınırları

            if (roket.x < 0) { roket.x = 0; roket.vx *= -0.5; }

            if (roket.y < 0) { roket.y = 0; roket.vy *= -0.5; }

            if (roket.x + roket.boyut > canvas.width) { roket.x = canvas.width - roket.boyut; roket.vx *= -0.5; }

            if (roket.y + roket.boyut > canvas.height) { roket.y = canvas.height - roket.boyut; roket.vy *= -0.5; }



            // Yıldızlar

            yildizlar.forEach(y => {

                y.y += y.hiz;

                if (y.y > canvas.height) y.y = 0;

            });



            // Kedi Toplama ve Hedef Kontrolü

            if (toplananKediler < hedefKediSayisi && Math.random() < 0.015) {

                kediOlustur();

            } else if (toplananKediler >= hedefKediSayisi) {

                hedef.gorunurMu = true;

            }



            // Gezegen Hareketi

            if (hedef.gorunurMu) {

                hedef.y += 1.2;

                // Gezegene ulaşma kontrolü

                if (roket.y < hedef.y + hedef.boyut / 2 && Math.abs(roket.x - (canvas.width/2 - roket.boyut/2)) < 200) {

                    seviyeAtla();

                }

                if (hedef.y > canvas.height) { // Gezegen kaçırılırsa tekrar belirsin

                    hedef.y = -450;

                }

            }



            // Meteorlar

            if (Math.random() < 0.02) { meteorOlustur(); }



            // Meteor Çarpışma

            for (let i = 0; i < meteorlar.length; i++) {

                let m = meteorlar[i];

                m.y += m.hiz;

                if (roket.x < m.x + m.boyut && roket.x + roket.boyut > m.x &&

                    roket.y < m.y + m.boyut && roket.y + roket.boyut > m.y) {

                    roket.can -= 20;

                    sarsintiSuresi = 10;

                    partikulOlustur(m.x + m.boyut / 2, m.y + m.boyut / 2, "gray", 15);

                    meteorlar.splice(i, 1); i--;

                    if (roket.can <= 0) { oyunBitti(); return; }

                    continue;

                }

                if (m.y > canvas.height) { meteorlar.splice(i, 1); i--; }

            }



            // Kedi Toplama Çarpışma

            for (let i = 0; i < kediler.length; i++) {

                let k = kediler[i];

                k.y += k.hiz;

                if (roket.x < k.x + k.boyut && roket.x + roket.boyut > k.x &&

                    roket.y < k.y + k.boyut && roket.y + roket.boyut > k.y) {

                    toplananKediler++;

                    partikulOlustur(k.x + k.boyut / 2, k.y + k.boyut / 2, "#f39c12", 10);

                    kediler.splice(i, 1); i--;

                    continue;

                }

                if (k.y > canvas.height) { kediler.splice(i, 1); i--; }

            }



            // Partikül Güncelleme

            for (let i = 0; i < partikuller.length; i++) {

                let p = partikuller[i];

                p.x += p.vx; p.y += p.vy; p.omur -= 0.02;

                if (p.omur <= 0) { partikuller.splice(i, 1); i--; }

            }



            if (sarsintiSuresi > 0) sarsintiSuresi--;

        }

function seviyeAtla() {

meteorlar = []; // Eski meteorları sil

    kediler = [];   // Eski kedileri sil

            seviye++;

            toplananKediler = 0;

            hedef.gorunurMu = false;

            hedef.y = -450;

            meteorHizi += 0.8; // Meteorlar hızlanır

            roket.can = Math.min(roket.can + 30, 100); // Ödül olarak can verir

            partikulOlustur(canvas.width / 2, canvas.height / 2, "white", 50);

            alert("Kediler Güvende! Seviye " + seviye + " başlıyor. Meteorlar daha hızlı!");

        }

// 5. Çizim Kısmı (Her şey ekrana burada basılır)

function ciz() {

            ctx.clearRect(0, 0, canvas.width, canvas.height);



            ctx.save();

            if (sarsintiSuresi > 0) {

                ctx.translate(Math.random() * 10 - 5, Math.random() * 10 - 5);

            }



            // Yıldızlar

            ctx.fillStyle = "white";

            yildizlar.forEach(y => { ctx.fillRect(y.x, y.y, y.boyut, y.boyut); });



            // Gezegen

            if (hedef.gorunurMu && gezegenGorseli.complete) {

                ctx.drawImage(gezegenGorseli, (canvas.width / 2) - (hedef.boyut / 2), hedef.y, hedef.boyut, hedef.boyut);

            }



            // Kediler

            kediler.forEach(k => {

                if (kediGorseli.complete) ctx.drawImage(kediGorseli, k.x, k.y, k.boyut, k.boyut);

            });



            // Partiküller

            partikuller.forEach(p => {

                ctx.globalAlpha = p.omur;

                ctx.fillStyle = p.renk;

                ctx.fillRect(p.x, p.y, 3, 3);

            });

            ctx.globalAlpha = 1.0;



            // Roket

            if (roket.resim.complete) {

                ctx.drawImage(roket.resim, roket.x, roket.y, roket.boyut, roket.boyut);

            }



            // Meteorlar

            meteorlar.forEach(meteor => {

                if (meteorGorseli.complete) {

                    ctx.drawImage(meteorGorseli, meteor.x, meteor.y, meteor.boyut, meteor.boyut);

                }

            });



            ctx.restore();



            // --- UI Elemanları ---

            // Can Barı

            ctx.fillStyle = "#333";

            ctx.fillRect(20, 20, 200, 20);

            let canOrani = (roket.can / roket.maksCan);

            ctx.fillStyle = canOrani > 0.4 ? "#2ecc71" : "#e74c3c";

            ctx.fillRect(20, 20, 200 * canOrani, 20);

            ctx.strokeStyle = "white";

            ctx.strokeRect(20, 20, 200, 20);



            // Kedi Sayacı ve Seviye

            ctx.fillStyle = "white";

            ctx.font = "bold 20px 'Times New Roman'";

            ctx.fillText("Toplanan Kediler: " + toplananKediler + " / " + hedefKediSayisi, 20, 65);

            ctx.fillText("Seviye: " + seviye, 20, 90);

           

            if (hedef.gorunurMu) {

                ctx.fillStyle = "#f1c40f";

                ctx.fillText("GEZEGEN GÖRÜNDÜ! KEDİLERİ ULAŞTIR!", canvas.width / 2 - 150, 100);

            }

        }

       

       

       

        function oyunBitti() {

    oyunDevamEdiyor = false;

    alert("Meteor çarptı! Görev başarısız.");

    location.reload();

}





    </script>





</head>



<body>



    <div class="resimler">

        <img src="images/uzay1.png">

        <img src="images/uzay2.png">

        <img src="images/uzay3.png">

        <img src="images/uzay4.png">

        <img src="images/uzay5.png">

        <img src="images/uzay6.png">

        <img src="images/uzay7.png">

        <img src="images/uzay8.png">

        <img src="images/uzay9.png">

        <img src="images/uzay10.png">

        <img src="images/roket.png" id="roket_pre">

        <img src="images/meteor.png" id="meteor_pre">

        <img src="images/gezegen.png" id="gezegen_pre">

    </div>

    <!-- resimlerin animasyon sırasında yüklenmesinden kaynaklanan problemlerin önüne geçek için class'ı resimler olan bir div oluşturuldu.

    Bu div'in amacı style etiketinde belirtildiği gibi resimleri önceden yüklemektir.-->



    <div class="arka_plan_animasyon"></div>

    <!-- Sayfanın arka planında sürekli animasyon yapılması için boş bir div oluşturulur.-->



    <button class="buton1" onclick="buton_giris()"  id="buton_id_1">Oyuna Başla</button>

    <!-- Oyuna giriş butona tıklayınca olacak şeyler için Javascript ile bir fonksiyon oluşturulur.-->





</body>



</html>



tamam şimdi bu koda şu değişiklikleri eklemeni istiyorum:

-önce roketi uzay_gemisi olan resimle değiştir .

-sonra uzayı uzay9 ile değiştir.

-meteorların düşme hızı oyun başında yavaş olsun ve oyun süresi uzadıkça düşme hızları aynı oranda artsın.

- uzay gemisinin , meteorların ve düşerken topladığımız kedilerin boyutunu biraz daha küçült.

- roketle ateş etme aksiyonları olsun ve bu sayede karşımıza çıkan meteorları yok edebilelim.

- belirli zamanlarda yukarıdan düşen yuvarlak şekilli özel yetenekler olsun. Örneğin bir tanesinde kum saati işareti olsun ve onu alırsak tüm meteorların düşme hızı 7 saniyeliğine yarıya düşsün. Diğer özel güçte mermi simgesi olsun ve onu alırsak mermi hızı 10 saniyeliğine 2 katına çıksın.

-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

Ai cevabı:



Harika bir güncelleme planı! İstediğin tüm özellikleri (uzay gemisi görseli değişimi, sabit uzay9 arka planı, artan meteor hızı, boyutların küçültülmesi, ateş etme mekaniği ve özel yetenekler) koduna entegre ettim.

Aşağıdaki kodu kopyalayıp web_proje.html dosyanın içine tamamen yapıştırabilirsin.

Yaptığım temel değişiklikler şunlar:



Arka plan animasyonu kaldırılarak sabit images/uzay9.png yapıldı.

Roket görselinin ismi images/uzay_gemisi.png olarak güncellendi.

Cisimlerin boyutları küçültüldü (Roket: 50, Kedi: 30, Meteor: 25-50 arası).

Boşluk (Space) tuşuna ateş etme özelliği eklendi. Mermiler meteorları yok ediyor.

Oyun süresi ilerledikçe meteorHizi değişkeni saniyede bir ufak ufak artacak şekilde ayarlandı.

Yukarıdan rastgele düşen zaman (Kum saati ⏳) ve mermi (Mermi 🔫) isimli özel güçler eklendi. Çarpışma kontrollerine bu güçlerin saniye sayaçları dahil edildi.

İşte güncellenmiş kodun:

HTML



<!DOCTYPE html><html lang="tr"><head>

<meta charset="UTF-8">

<meta name="description" content="Bu proje WEB Tabanlı Programlama Dersi kapsamında yapılmıştır.">

<meta name="author" content="Alperen Namlı, Halil Hüseyin Çalışkan, Muhammed Emin Uysal, Nurullah Harun Köse, Recep Doruk">

<meta name="keys" content="HTML,CSS,Javascript,Oyun">



<style>

body{

margin: 0px;

padding: 0px;

overflow: hidden; /* Sayfanın kaymasını engeller */

}

.resimler{

display: none;

}



.arka_plan_animasyon{

width: 100%;

height: 100vh;

background-size: cover;

background-image: url(images/uzay9.png); /* Sabit uzay9 arka planı */

position: absolute;

top:0;

left:0;

}



.buton1{

position: absolute;

width: 10%;

height: 10vh;

top: 50%;

left: 50%;

transform: translate(-50%,-50%);

border-radius: 15px;

background-color: #7CAAE6;

font-weight: bold;

font-family: 'Times New Roman', Times, serif;

font-size: large;

transition: all 0.4s;

}



.buton1:hover{

cursor: pointer;

background-color: #3B8EFF;

transform: translate(-50%,-50%) scale(1.2);

}

</style>


<script>// 1. Değişkenleri Tanımlayalımlet canvas, ctx;let oyunDevamEdiyor = false;let oyunSuresiFrames = 0; // Süreye bağlı hız artışı için sayaç// Oyuncu (roket) Objesi (Boyutu 50'ye düşürüldü)let roket = {

x: 100,

y: 100,

vx: 0,

vy: 0,

ivme: 0.4,

surtunme: 0.96,

boyut: 50,

can: 100,

maksCan: 100

};// Mermi Değişkenlerilet mermiler = [];let sonAtesZamani = 0;let atesGecikmesi = 15; // Mermiler arası bekleme süresi (Frame)// Özel Güç Değişkenlerilet gucSimgeleri = [];let meteorHizCarpani = 1;let meteorYavaslaticiSayac = 0;let mermiHizCarpani = 1;let mermiBuffSayac = 0;let toplananKediler = 0;let hedefKediSayisi = 30;let seviye = 1;let kediler = [];const kediGorseli = new Image();

kediGorseli.src = 'images/kedi.png';const roketGorseli = new Image();

roketGorseli.src = 'images/uzay_gemisi.png'; // Roket görseli uzay_gemisi olarak değiştirildi

roket.resim = roketGorseli;// Hedef (Gezegen) Objesiconst gezegenGorseli = new Image();

gezegenGorseli.src = 'images/gezegen.png'; let hedef = {

y: -450,

boyut: 400,

mesafe: 3000,

gorunurMu: false

};let tuslar = {};let meteorlar = [];let meteorHizi = 0.5; // Başlangıç hızılet partikuller = []; let yildizlar = []; let sarsintiSuresi = 0; const meteorGorseli = new Image();

meteorGorseli.src = 'images/meteor.png'; // 2. Butona tıklandığında çalışacak fonksiyonfunction buton_giris() {

var buton = document.getElementById("buton_id_1");

buton.style.display = "none";



canvas = document.createElement("canvas");

ctx = canvas.getContext("2d");


canvas.width = window.innerWidth;

canvas.height = window.innerHeight;

canvas.style.position = "absolute";

canvas.style.top = "0";

canvas.style.left = "0";

canvas.style.zIndex = "10";


document.body.appendChild(canvas);



for(let i=0; i<100; i++) {

yildizlar.push({

x: Math.random() * canvas.width,

y: Math.random() * canvas.height,

hiz: Math.random() * 3 + 1,

boyut: Math.random() * 2

});

}



window.addEventListener('resize', function() {

canvas.width = window.innerWidth;

canvas.height = window.innerHeight;

});


roket.x = canvas.width / 2 - roket.boyut / 2;

roket.y = canvas.height / 2 - roket.boyut / 2;



window.addEventListener("keydown", (e) => {

tuslar[e.key] = true;

if (e.key === " ") e.preventDefault(); // Boşluk tuşunun sayfayı kaydırmasını engeller

});

window.addEventListener("keyup", (e) => { tuslar[e.key] = false; });



oyunDevamEdiyor = true;

oyun_dongusu();

}function partikulOlustur(x, y, renk, adet) {

for (let i = 0; i < adet; i++) {

partikuller.push({

x: x,

y: y,

vx: Math.random() * 6 - 3,

vy: Math.random() * 6 - 3,

omur: 1.0,

renk: renk

});

}

}

function kediOlustur() {

let boyut = 30; // Kediler küçültüldü

let x = Math.random() * (canvas.width - boyut);

kediler.push({

x: x, y: -boyut,

boyut: boyut,

hiz: Math.random() * 1 + 2

});

}function meteorOlustur() {

let boyut = Math.random() * (50 - 25) + 25; // Meteorlar küçültüldü

let x = Math.random() * (canvas.width - boyut);


meteorlar.push({

x: x,

y: -boyut,

boyut: boyut,

hiz: Math.random() * 2 + meteorHizi

});

}function gucOlustur() {

let boyut = 30;

let x = Math.random() * (canvas.width - boyut);

let tip = Math.random() < 0.5 ? 'zaman' : 'mermi';


gucSimgeleri.push({

x: x,

y: -boyut,

boyut: boyut,

hiz: 2,

tip: tip

});

}// 3. Ana Oyun Döngüsüfunction oyun_dongusu() {

if (!oyunDevamEdiyor) return;



guncelle();

ciz();



requestAnimationFrame(oyun_dongusu);

}function guncelle() {

oyunSuresiFrames++;


// Oyun süresi uzadıkça meteor düşme hızı artsın (Her saniye hafif bir artış)

if (oyunSuresiFrames % 60 === 0) {

meteorHizi += 0.02;

}



// Özel Güç Sayaçlarını Güncelle

if (meteorYavaslaticiSayac > 0) {

meteorYavaslaticiSayac--;

if (meteorYavaslaticiSayac === 0) meteorHizCarpani = 1;

}

if (mermiBuffSayac > 0) {

mermiBuffSayac--;

if (mermiBuffSayac === 0) mermiHizCarpani = 1;

}



// Momentum Hareketi

if (tuslar["ArrowUp"] || tuslar["w"]) roket.vy -= roket.ivme;

if (tuslar["ArrowDown"] || tuslar["s"]) roket.vy += roket.ivme;

if (tuslar["ArrowLeft"] || tuslar["a"]) roket.vx -= roket.ivme;

if (tuslar["ArrowRight"] || tuslar["d"]) roket.vx += roket.ivme;



// Ateş Etme

if (tuslar[" "] && sonAtesZamani <= 0) {

mermiler.push({

x: roket.x + roket.boyut / 2 - 2,

y: roket.y,

boyutX: 4,

boyutY: 15,

hiz: 10 * mermiHizCarpani // Mermi buff alındıysa hız x2 olur

});

sonAtesZamani = atesGecikmesi;

}

if (sonAtesZamani > 0) sonAtesZamani--;



roket.vx *= roket.surtunme;

roket.vy *= roket.surtunme;

roket.x += roket.vx;

roket.y += roket.vy;



// Egzoz Partikülleri

if (Math.abs(roket.vx) > 0.5 || Math.abs(roket.vy) > 0.5) {

partikulOlustur(roket.x + roket.boyut / 2, roket.y + roket.boyut - 5, "orange", 1);

}



// Ekran Sınırları

if (roket.x < 0) { roket.x = 0; roket.vx *= -0.5; }

if (roket.y < 0) { roket.y = 0; roket.vy *= -0.5; }

if (roket.x + roket.boyut > canvas.width) { roket.x = canvas.width - roket.boyut; roket.vx *= -0.5; }

if (roket.y + roket.boyut > canvas.height) { roket.y = canvas.height - roket.boyut; roket.vy *= -0.5; }



// Yıldızlar

yildizlar.forEach(y => {

y.y += y.hiz;

if (y.y > canvas.height) y.y = 0;

});



// Mermiler ve Meteorları Vurma

for (let i = 0; i < mermiler.length; i++) {

let m = mermiler[i];

m.y -= m.hiz;

let vuruldu = false;



for (let j = 0; j < meteorlar.length; j++) {

let met = meteorlar[j];

if (m.x < met.x + met.boyut && m.x + m.boyutX > met.x &&

m.y < met.y + met.boyut && m.y + m.boyutY > met.y) {


partikulOlustur(met.x + met.boyut / 2, met.y + met.boyut / 2, "gray", 15);

meteorlar.splice(j, 1);

vuruldu = true;

break;

}

}



if (vuruldu) {

mermiler.splice(i, 1); i--; continue;

}

if (m.y < 0) { mermiler.splice(i, 1); i--; }

}



// Özel Güç Çıkma İhtimali

if (Math.random() < 0.002) { gucOlustur(); }



// Özel Güçlerin Düşmesi ve Toplanması

for (let i = 0; i < gucSimgeleri.length; i++) {

let g = gucSimgeleri[i];

g.y += g.hiz;



// Roket ile özel güç çarpışması

if (roket.x < g.x + g.boyut && roket.x + roket.boyut > g.x &&

roket.y < g.y + g.boyut && roket.y + roket.boyut > g.y) {


if (g.tip === 'zaman') {

meteorHizCarpani = 0.5; // Meteorları yarı hızına düşür

meteorYavaslaticiSayac = 7 * 60; // 7 saniye (60 fps)

partikulOlustur(roket.x + roket.boyut / 2, roket.y, "#00c8ff", 20);

} else if (g.tip === 'mermi') {

mermiHizCarpani = 2; // Mermi hızını iki katına çıkar

mermiBuffSayac = 10 * 60; // 10 saniye (60 fps)

partikulOlustur(roket.x + roket.boyut / 2, roket.y, "#ff3232", 20);

}


gucSimgeleri.splice(i, 1); i--;

continue;

}



if (g.y > canvas.height) { gucSimgeleri.splice(i, 1); i--; }

}



// Kedi Toplama ve Hedef Kontrolü

if (toplananKediler < hedefKediSayisi && Math.random() < 0.015) {

kediOlustur();

} else if (toplananKediler >= hedefKediSayisi) {

hedef.gorunurMu = true;

}



// Gezegen Hareketi

if (hedef.gorunurMu) {

hedef.y += 1.2;

if (roket.y < hedef.y + hedef.boyut / 2 && Math.abs(roket.x - (canvas.width/2 - roket.boyut/2)) < 200) {

seviyeAtla();

}

if (hedef.y > canvas.height) {

hedef.y = -450;

}

}



// Meteorlar

if (Math.random() < 0.02) { meteorOlustur(); }



// Meteor Çarpışma

for (let i = 0; i < meteorlar.length; i++) {

let m = meteorlar[i];

m.y += m.hiz * meteorHizCarpani; // Kum saati alındıysa yavaş düşer



if (roket.x < m.x + m.boyut && roket.x + roket.boyut > m.x &&

roket.y < m.y + m.boyut && roket.y + roket.boyut > m.y) {

roket.can -= 20;

sarsintiSuresi = 10;

partikulOlustur(m.x + m.boyut / 2, m.y + m.boyut / 2, "gray", 15);

meteorlar.splice(i, 1); i--;

if (roket.can <= 0) { oyunBitti(); return; }

continue;

}

if (m.y > canvas.height) { meteorlar.splice(i, 1); i--; }

}



// Kedi Toplama Çarpışma

for (let i = 0; i < kediler.length; i++) {

let k = kediler[i];

k.y += k.hiz;

if (roket.x < k.x + k.boyut && roket.x + roket.boyut > k.x &&

roket.y < k.y + k.boyut && roket.y + roket.boyut > k.y) {

toplananKediler++;

partikulOlustur(k.x + k.boyut / 2, k.y + k.boyut / 2, "#f39c12", 10);

kediler.splice(i, 1); i--;

continue;

}

if (k.y > canvas.height) { kediler.splice(i, 1); i--; }

}



// Partikül Güncelleme

for (let i = 0; i < partikuller.length; i++) {

let p = partikuller[i];

p.x += p.vx; p.y += p.vy; p.omur -= 0.02;

if (p.omur <= 0) { partikuller.splice(i, 1); i--; }

}



if (sarsintiSuresi > 0) sarsintiSuresi--;

}function seviyeAtla() {

meteorlar = [];

kediler = [];

mermiler = [];

gucSimgeleri = [];

seviye++;

toplananKediler = 0;

hedef.gorunurMu = false;

hedef.y = -450;

meteorHizi += 0.5; // Yeni seviyede meteor temel hızı iyice artar

roket.can = Math.min(roket.can + 30, 100);

partikulOlustur(canvas.width / 2, canvas.height / 2, "white", 50);

alert("Kediler Güvende! Seviye " + seviye + " başlıyor. Meteorlar artık daha hızlı düşecek!");

}// 5. Çizim Kısmı function ciz() {

ctx.clearRect(0, 0, canvas.width, canvas.height);



ctx.save();

if (sarsintiSuresi > 0) {

ctx.translate(Math.random() * 10 - 5, Math.random() * 10 - 5);

}



// Yıldızlar

ctx.fillStyle = "white";

yildizlar.forEach(y => { ctx.fillRect(y.x, y.y, y.boyut, y.boyut); });



// Gezegen

if (hedef.gorunurMu && gezegenGorseli.complete) {

ctx.drawImage(gezegenGorseli, (canvas.width / 2) - (hedef.boyut / 2), hedef.y, hedef.boyut, hedef.boyut);

}



// Kediler

kediler.forEach(k => {

if (kediGorseli.complete) ctx.drawImage(kediGorseli, k.x, k.y, k.boyut, k.boyut);

});



// Özel Güç Simgelerini Çiz

gucSimgeleri.forEach(g => {

ctx.beginPath();

ctx.arc(g.x + g.boyut / 2, g.y + g.boyut / 2, g.boyut / 2, 0, Math.PI * 2);

ctx.fillStyle = g.tip === 'zaman' ? "rgba(0, 200, 255, 0.8)" : "rgba(255, 50, 50, 0.8)";

ctx.fill();

ctx.strokeStyle = "white";

ctx.lineWidth = 2;

ctx.stroke();


ctx.fillStyle = "white";

ctx.font = "20px Arial";

ctx.textAlign = "center";

ctx.textBaseline = "middle";

ctx.fillText(g.tip === 'zaman' ? "⏳" : "🔫", g.x + g.boyut / 2, g.y + g.boyut / 2);

});



// Partiküller

partikuller.forEach(p => {

ctx.globalAlpha = p.omur;

ctx.fillStyle = p.renk;

ctx.fillRect(p.x, p.y, 3, 3);

});

ctx.globalAlpha = 1.0;



// Mermileri Çiz

ctx.fillStyle = "yellow";

mermiler.forEach(m => {

ctx.fillRect(m.x, m.y, m.boyutX, m.boyutY);

});



// Roket

if (roket.resim.complete) {

ctx.drawImage(roket.resim, roket.x, roket.y, roket.boyut, roket.boyut);

}



// Meteorlar

meteorlar.forEach(meteor => {

if (meteorGorseli.complete) {

ctx.drawImage(meteorGorseli, meteor.x, meteor.y, meteor.boyut, meteor.boyut);

}

});



ctx.restore();



// --- UI Elemanları ---

// Can Barı

ctx.fillStyle = "#333";

ctx.fillRect(20, 20, 200, 20);

let canOrani = (roket.can / roket.maksCan);

ctx.fillStyle = canOrani > 0.4 ? "#2ecc71" : "#e74c3c";

ctx.fillRect(20, 20, 200 * canOrani, 20);

ctx.strokeStyle = "white";

ctx.strokeRect(20, 20, 200, 20);



// Kedi Sayacı ve Seviye

ctx.fillStyle = "white";

ctx.font = "bold 20px 'Times New Roman'";

ctx.textAlign = "left";

ctx.fillText("Toplanan Kediler: " + toplananKediler + " / " + hedefKediSayisi, 20, 65);

ctx.fillText("Seviye: " + seviye, 20, 90);


// Aktif Güç Göstergeleri

if (meteorYavaslaticiSayac > 0) {

ctx.fillStyle = "#00c8ff";

ctx.fillText("Zaman Yavaşlatıldı: " + Math.ceil(meteorYavaslaticiSayac / 60) + "s", 20, 120);

}

if (mermiBuffSayac > 0) {

ctx.fillStyle = "#ff3232";

ctx.fillText("Hızlı Mermi: " + Math.ceil(mermiBuffSayac / 60) + "s", 20, 145);

}


if (hedef.gorunurMu) {

ctx.fillStyle = "#f1c40f";

ctx.textAlign = "center";

ctx.fillText("GEZEGEN GÖRÜNDÜ! KEDİLERİ ULAŞTIR!", canvas.width / 2, 100);

}

}

function oyunBitti() {

oyunDevamEdiyor = false;

alert("Meteor çarptı! Görev başarısız.");

location.reload();

}



</script></head><body>



<div class="resimler">

<img src="images/uzay9.png">

<img src="images/uzay_gemisi.png" id="roket_pre">

<img src="images/meteor.png" id="meteor_pre">

<img src="images/gezegen.png" id="gezegen_pre">

</div>



<div class="arka_plan_animasyon"></div>



<button class="buton1" onclick="buton_giris()" id="buton_id_1">Oyuna Başla</button></body></html>

-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

prompt: oyunu başlat dedikten 1 saniye sonra oyun kendi kendine duruyor.

-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------


Ai cevabı:



Recep, oyunun 1 saniye sonra aniden donup kalması (kendi kendine durması) aslında arkada çok spesifik bir Javascript çökmesi (hata) olduğunu gösteriyor. Bu çok yaygın karşılaşılan ve mantığı çok ilginç olan bir hatadır, hemen nedenini açıklayayım.



Neden Tam Olarak 1 Saniye Sonra Çöküyor?

Tarayıcılar bir resim dosyasını (uzay_gemisi.png, meteor.png vb.) ararken bulamazsa, hemen pes etmezler. Yaklaşık 1 saniye kadar dosyayı yüklemeyi denerler. Bu 1 saniyelik süreçte kodumuzdaki resim.complete (resim yüklendi mi?) kontrolü "hayır, henüz yüklenmedi" der ve oyun çalışmaya devam eder.

Ancak 1 saniye geçip tarayıcı dosyayı bulamayınca pes eder ve resim.complete değerini "Evet, işlem bitti (ama hatalı bitti)" diyerek True'ya çeker. Bizim kodumuz da "Aha resim yüklenmiş, hadi ekrana çizelim!" diyerek kırık bir resmi canvas'a çizmeye çalışır. Kırık resmi çizmeye çalışmak Javascript'in anında çökmesine ve oyun döngüsünün tamamen durmasına yol açar.

Yani dosyalar klasörde olsa bile; bir dosyanın isminde veya uzantısında hala ufak bir hata var. (Örneğin senin indirdiğin resim uzay_gemisi.jpg olabilir ama kodda .png yazıyor olabilir).



Kesin Çözüm: Kodumuzu Çökmelere Karşı Korumalı Hale Getirelim

Eksik bir resim olsa bile oyunun çökmesini engellemek için kodumuzdaki çizim (ciz) fonksiyonuna küçük bir güvenlik önlemi eklemeliyiz. Mevcut ciz() fonksiyonunu silip yerine aşağıdakini yapıştır:

JavaScript



// 5. Çizim Kısmı (Güvenli Çizim Modu)function ciz() {

ctx.clearRect(0, 0, canvas.width, canvas.height);



ctx.save();

if (sarsintiSuresi > 0) {

ctx.translate(Math.random() * 10 - 5, Math.random() * 10 - 5);

}



// Yıldızlar

ctx.fillStyle = "white";

yildizlar.forEach(y => { ctx.fillRect(y.x, y.y, y.boyut, y.boyut); });



// Gezegen (Güvenli Çizim)

if (hedef.gorunurMu && gezegenGorseli.complete && gezegenGorseli.naturalWidth !== 0) {

ctx.drawImage(gezegenGorseli, (canvas.width / 2) - (hedef.boyut / 2), hedef.y, hedef.boyut, hedef.boyut);

}



// Kediler (Güvenli Çizim)

kediler.forEach(k => {

if (kediGorseli.complete && kediGorseli.naturalWidth !== 0) {

ctx.drawImage(kediGorseli, k.x, k.y, k.boyut, k.boyut);

}

});



// Özel Güç Simgelerini Çiz

gucSimgeleri.forEach(g => {

ctx.beginPath();

ctx.arc(g.x + g.boyut / 2, g.y + g.boyut / 2, g.boyut / 2, 0, Math.PI * 2);

ctx.fillStyle = g.tip === 'zaman' ? "rgba(0, 200, 255, 0.8)" : "rgba(255, 50, 50, 0.8)";

ctx.fill();

ctx.strokeStyle = "white";

ctx.lineWidth = 2;

ctx.stroke();


ctx.fillStyle = "white";

ctx.font = "20px Arial";

ctx.textAlign = "center";

ctx.textBaseline = "middle";

ctx.fillText(g.tip === 'zaman' ? "⏳" : "🔫", g.x + g.boyut / 2, g.y + g.boyut / 2);

});



// Partiküller

partikuller.forEach(p => {

ctx.globalAlpha = p.omur;

ctx.fillStyle = p.renk;

ctx.fillRect(p.x, p.y, 3, 3);

});

ctx.globalAlpha = 1.0;



// Mermileri Çiz

ctx.fillStyle = "yellow";

mermiler.forEach(m => {

ctx.fillRect(m.x, m.y, m.boyutX, m.boyutY);

});



// Roket (Güvenli Çizim)

if (roket.resim.complete && roket.resim.naturalWidth !== 0) {

ctx.drawImage(roket.resim, roket.x, roket.y, roket.boyut, roket.boyut);

}



// Meteorlar (Güvenli Çizim)

meteorlar.forEach(meteor => {

if (meteorGorseli.complete && meteorGorseli.naturalWidth !== 0) {

ctx.drawImage(meteorGorseli, meteor.x, meteor.y, meteor.boyut, meteor.boyut);

}

});



ctx.restore();



// --- UI Elemanları ---

// Can Barı

ctx.fillStyle = "#333";

ctx.fillRect(20, 20, 200, 20);

let canOrani = (roket.can / roket.maksCan);

ctx.fillStyle = canOrani > 0.4 ? "#2ecc71" : "#e74c3c";

ctx.fillRect(20, 20, 200 * canOrani, 20);

ctx.strokeStyle = "white";

ctx.strokeRect(20, 20, 200, 20);



// Kedi Sayacı ve Seviye

ctx.fillStyle = "white";

ctx.font = "bold 20px 'Times New Roman'";

ctx.textAlign = "left";

ctx.fillText("Toplanan Kediler: " + toplananKediler + " / " + hedefKediSayisi, 20, 65);

ctx.fillText("Seviye: " + seviye, 20, 90);


// Aktif Güç Göstergeleri

if (meteorYavaslaticiSayac > 0) {

ctx.fillStyle = "#00c8ff";

ctx.fillText("Zaman Yavaşlatıldı: " + Math.ceil(meteorYavaslaticiSayac / 60) + "s", 20, 120);

}

if (mermiBuffSayac > 0) {

ctx.fillStyle = "#ff3232";

ctx.fillText("Hızlı Mermi: " + Math.ceil(mermiBuffSayac / 60) + "s", 20, 145);

}


if (hedef.gorunurMu) {

ctx.fillStyle = "#f1c40f";

ctx.textAlign = "center";

ctx.fillText("GEZEGEN GÖRÜNDÜ! KEDİLERİ ULAŞTIR!", canvas.width / 2, 100);

}

}

-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------


prompt:



tamam şimdi aynı kodda roketin hızını ve meteorların düşme hızını yarı yarıya düşürür müsün?

-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------


Ai cevabı:



Tamamdır, oyunun zorluğunu biraz daha dengeli bir hale getirelim. Roketin ivmesini ve meteorların hem başlangıç hızlarını hem de zamanla/seviyeyle artan hızlarını tam yarı yarıya düşürdüm.

Sadece <script> ve </script> etiketleri arasındaki kısmı aşağıdaki kodla değiştirmen yeterli olacaktır:



// 1. Değişkenleri Tanımlayalım

let canvas, ctx;

let oyunDevamEdiyor = false;

let oyunSuresiFrames = 0; // Süreye bağlı hız artışı için sayaç



// Oyuncu (roket) Objesi 

let roket = {

    x: 100,

    y: 100,

    vx: 0, 

    vy: 0, 

    ivme: 0.2, // YARIYA DÜŞÜRÜLDÜ (Önceki: 0.4)

    surtunme: 0.96, 

    boyut: 50, 

    can: 100,

    maksCan: 100

};



// Mermi Değişkenleri

let mermiler = [];

let sonAtesZamani = 0;

let atesGecikmesi = 15; // Mermiler arası bekleme süresi (Frame)



// Özel Güç Değişkenleri

let gucSimgeleri = [];

let meteorHizCarpani = 1;

let meteorYavaslaticiSayac = 0;

let mermiHizCarpani = 1;

let mermiBuffSayac = 0;



let toplananKediler = 0;

let hedefKediSayisi = 30;

let seviye = 1;



let kediler = [];

const kediGorseli = new Image();

kediGorseli.src = 'images/kedi.png';



const roketGorseli = new Image();

roketGorseli.src = 'images/uzay_gemisi.png'; 

roket.resim = roketGorseli;



// Hedef (Gezegen) Objesi

const gezegenGorseli = new Image();

gezegenGorseli.src = 'images/gezegen.png'; 



let hedef = {

    y: -450, 

    boyut: 400,

    mesafe: 3000, 

    gorunurMu: false

};



let tuslar = {};

let meteorlar = [];

let meteorHizi = 0.25; // BAŞLANGIÇ HIZI YARIYA DÜŞÜRÜLDÜ (Önceki: 0.5)

let partikuller = []; 

let yildizlar = [];    

let sarsintiSuresi = 0; 

const meteorGorseli = new Image();

meteorGorseli.src = 'images/meteor.png'; 



// 2. Butona tıklandığında çalışacak fonksiyon

function buton_giris() {

    var buton = document.getElementById("buton_id_1");

    buton.style.display = "none";



    canvas = document.createElement("canvas");

    ctx = canvas.getContext("2d");

    

    canvas.width = window.innerWidth;

    canvas.height = window.innerHeight;

    canvas.style.position = "absolute";

    canvas.style.top = "0";

    canvas.style.left = "0";

    canvas.style.zIndex = "10"; 

    

    document.body.appendChild(canvas);



    for(let i=0; i<100; i++) {

        yildizlar.push({

            x: Math.random() * canvas.width,

            y: Math.random() * canvas.height,

            hiz: Math.random() * 3 + 1,

            boyut: Math.random() * 2

        });

    }



    window.addEventListener('resize', function() {

        canvas.width = window.innerWidth;

        canvas.height = window.innerHeight;

    });

    

    roket.x = canvas.width / 2 - roket.boyut / 2;

    roket.y = canvas.height / 2 - roket.boyut / 2;



    window.addEventListener("keydown", (e) => { 

        tuslar[e.key] = true; 

        if (e.key === " ") e.preventDefault(); 

    });

    window.addEventListener("keyup", (e) => { tuslar[e.key] = false; });



    oyunDevamEdiyor = true;

    oyun_dongusu();

}



function partikulOlustur(x, y, renk, adet) {

    for (let i = 0; i < adet; i++) {

        partikuller.push({

            x: x,

            y: y,

            vx: Math.random() * 6 - 3,

            vy: Math.random() * 6 - 3,

            omur: 1.0,

            renk: renk

        });

    }

}

        

function kediOlustur() {

    let boyut = 30; 

    let x = Math.random() * (canvas.width - boyut);

    kediler.push({

        x: x, y: -boyut,

        boyut: boyut,

        hiz: Math.random() * 1 + 2

    });

}



function meteorOlustur() {

    let boyut = Math.random() * (50 - 25) + 25; 

    let x = Math.random() * (canvas.width - boyut);

    

    meteorlar.push({

        x: x,

        y: -boyut,

        boyut: boyut,

        // RASTGELE HIZ EKLENTİSİ DE YARIYA DÜŞÜRÜLDÜ (Önceki: Math.random() * 2)

        hiz: Math.random() * 1 + meteorHizi 

    });

}



function gucOlustur() {

    let boyut = 30;

    let x = Math.random() * (canvas.width - boyut);

    let tip = Math.random() < 0.5 ? 'zaman' : 'mermi';

    

    gucSimgeleri.push({

        x: x,

        y: -boyut,

        boyut: boyut,

        hiz: 2,

        tip: tip

    });

}



// 3. Ana Oyun Döngüsü

function oyun_dongusu() {

    if (!oyunDevamEdiyor) return;



    guncelle();

    ciz();



    requestAnimationFrame(oyun_dongusu);

}



function guncelle() {

    oyunSuresiFrames++;

    

    // ZAMANLA ARTAN HIZ YARIYA DÜŞÜRÜLDÜ (Önceki: 0.02)

    if (oyunSuresiFrames % 60 === 0) {

        meteorHizi += 0.01;

    }



    // Özel Güç Sayaçlarını Güncelle

    if (meteorYavaslaticiSayac > 0) {

        meteorYavaslaticiSayac--;

        if (meteorYavaslaticiSayac === 0) meteorHizCarpani = 1;

    }

    if (mermiBuffSayac > 0) {

        mermiBuffSayac--;

        if (mermiBuffSayac === 0) mermiHizCarpani = 1;

    }



    // Momentum Hareketi

    if (tuslar["ArrowUp"] || tuslar["w"]) roket.vy -= roket.ivme;

    if (tuslar["ArrowDown"] || tuslar["s"]) roket.vy += roket.ivme;

    if (tuslar["ArrowLeft"] || tuslar["a"]) roket.vx -= roket.ivme;

    if (tuslar["ArrowRight"] || tuslar["d"]) roket.vx += roket.ivme;



    // Ateş Etme

    if (tuslar[" "] && sonAtesZamani <= 0) {

        mermiler.push({

            x: roket.x + roket.boyut / 2 - 2, 

            y: roket.y, 

            boyutX: 4, 

            boyutY: 15, 

            hiz: 10 * mermiHizCarpani 

        });

        sonAtesZamani = atesGecikmesi;

    }

    if (sonAtesZamani > 0) sonAtesZamani--;



    roket.vx *= roket.surtunme;

    roket.vy *= roket.surtunme;

    roket.x += roket.vx;

    roket.y += roket.vy;



    // Egzoz Partikülleri

    if (Math.abs(roket.vx) > 0.5 || Math.abs(roket.vy) > 0.5) {

        partikulOlustur(roket.x + roket.boyut / 2, roket.y + roket.boyut - 5, "orange", 1);

    }



    // Ekran Sınırları

    if (roket.x < 0) { roket.x = 0; roket.vx *= -0.5; }

    if (roket.y < 0) { roket.y = 0; roket.vy *= -0.5; }

    if (roket.x + roket.boyut > canvas.width) { roket.x = canvas.width - roket.boyut; roket.vx *= -0.5; }

    if (roket.y + roket.boyut > canvas.height) { roket.y = canvas.height - roket.boyut; roket.vy *= -0.5; }



    // Yıldızlar

    yildizlar.forEach(y => {

        y.y += y.hiz;

        if (y.y > canvas.height) y.y = 0;

    });



    // Mermiler ve Meteorları Vurma

    for (let i = 0; i < mermiler.length; i++) {

        let m = mermiler[i];

        m.y -= m.hiz;

        let vuruldu = false;



        for (let j = 0; j < meteorlar.length; j++) {

            let met = meteorlar[j];

            if (m.x < met.x + met.boyut && m.x + m.boyutX > met.x &&

                m.y < met.y + met.boyut && m.y + m.boyutY > met.y) {

                

                partikulOlustur(met.x + met.boyut / 2, met.y + met.boyut / 2, "gray", 15);

                meteorlar.splice(j, 1);

                vuruldu = true;

                break;

            }

        }



        if (vuruldu) {

            mermiler.splice(i, 1); i--; continue;

        }

        if (m.y < 0) { mermiler.splice(i, 1); i--; }

    }



    // Özel Güç Çıkma İhtimali

    if (Math.random() < 0.002) { gucOlustur(); }



    // Özel Güçlerin Düşmesi ve Toplanması

    for (let i = 0; i < gucSimgeleri.length; i++) {

        let g = gucSimgeleri[i];

        g.y += g.hiz;



        // Roket ile özel güç çarpışması

        if (roket.x < g.x + g.boyut && roket.x + roket.boyut > g.x &&

            roket.y < g.y + g.boyut && roket.y + roket.boyut > g.y) {

            

            if (g.tip === 'zaman') {

                meteorHizCarpani = 0.5; 

                meteorYavaslaticiSayac = 7 * 60; 

                partikulOlustur(roket.x + roket.boyut / 2, roket.y, "#00c8ff", 20);

            } else if (g.tip === 'mermi') {

                mermiHizCarpani = 2; 

                mermiBuffSayac = 10 * 60; 

                partikulOlustur(roket.x + roket.boyut / 2, roket.y, "#ff3232", 20);

            }

            

            gucSimgeleri.splice(i, 1); i--;

            continue;

        }



        if (g.y > canvas.height) { gucSimgeleri.splice(i, 1); i--; }

    }



    // Kedi Toplama ve Hedef Kontrolü

    if (toplananKediler < hedefKediSayisi && Math.random() < 0.015) { 

        kediOlustur(); 

    } else if (toplananKediler >= hedefKediSayisi) {

        hedef.gorunurMu = true;

    }



    // Gezegen Hareketi

    if (hedef.gorunurMu) {

        hedef.y += 1.2;

        if (roket.y < hedef.y + hedef.boyut / 2 && Math.abs(roket.x - (canvas.width/2 - roket.boyut/2)) < 200) {

            seviyeAtla();

        }

        if (hedef.y > canvas.height) { 

            hedef.y = -450;

        }

    }



    // Meteorlar

    if (Math.random() < 0.02) { meteorOlustur(); }



    // Meteor Çarpışma

    for (let i = 0; i < meteorlar.length; i++) {

        let m = meteorlar[i];

        m.y += m.hiz * meteorHizCarpani; 



        if (roket.x < m.x + m.boyut && roket.x + roket.boyut > m.x &&

            roket.y < m.y + m.boyut && roket.y + roket.boyut > m.y) {

            roket.can -= 20;

            sarsintiSuresi = 10;

            partikulOlustur(m.x + m.boyut / 2, m.y + m.boyut / 2, "gray", 15);

            meteorlar.splice(i, 1); i--;

            if (roket.can <= 0) { oyunBitti(); return; }

            continue;

        }

        if (m.y > canvas.height) { meteorlar.splice(i, 1); i--; }

    }



    // Kedi Toplama Çarpışma

    for (let i = 0; i < kediler.length; i++) {

        let k = kediler[i];

        k.y += k.hiz;

        if (roket.x < k.x + k.boyut && roket.x + roket.boyut > k.x &&

            roket.y < k.y + k.boyut && roket.y + roket.boyut > k.y) {

            toplananKediler++;

            partikulOlustur(k.x + k.boyut / 2, k.y + k.boyut / 2, "#f39c12", 10);

            kediler.splice(i, 1); i--;

            continue;

        }

        if (k.y > canvas.height) { kediler.splice(i, 1); i--; }

    }



    // Partikül Güncelleme

    for (let i = 0; i < partikuller.length; i++) {

        let p = partikuller[i];

        p.x += p.vx; p.y += p.vy; p.omur -= 0.02;

        if (p.omur <= 0) { partikuller.splice(i, 1); i--; }

    }



    if (sarsintiSuresi > 0) sarsintiSuresi--;

}



function seviyeAtla() {

    meteorlar = []; 

    kediler = []; 

    mermiler = [];

    gucSimgeleri = [];

    seviye++;

    toplananKediler = 0;

    hedef.gorunurMu = false;

    hedef.y = -450;

    // SEVİYE ATLAYINCA ARTAN HIZ YARIYA DÜŞÜRÜLDÜ (Önceki: 0.5)

    meteorHizi += 0.25; 

    roket.can = Math.min(roket.can + 30, 100); 

    partikulOlustur(canvas.width / 2, canvas.height / 2, "white", 50);

    alert("Kediler Güvende! Seviye " + seviye + " başlıyor. Meteorlar artık daha hızlı düşecek!");

}



// 5. Çizim Kısmı (Güvenli Çizim Modu)

function ciz() {

    ctx.clearRect(0, 0, canvas.width, canvas.height);



    ctx.save();

    if (sarsintiSuresi > 0) {

        ctx.translate(Math.random() * 10 - 5, Math.random() * 10 - 5);

    }



    // Yıldızlar

    ctx.fillStyle = "white";

    yildizlar.forEach(y => { ctx.fillRect(y.x, y.y, y.boyut, y.boyut); });



    // Gezegen (Güvenli Çizim)

    if (hedef.gorunurMu && gezegenGorseli.complete && gezegenGorseli.naturalWidth !== 0) {

        ctx.drawImage(gezegenGorseli, (canvas.width / 2) - (hedef.boyut / 2), hedef.y, hedef.boyut, hedef.boyut);

    }



    // Kediler (Güvenli Çizim)

    kediler.forEach(k => {

        if (kediGorseli.complete && kediGorseli.naturalWidth !== 0) {

            ctx.drawImage(kediGorseli, k.x, k.y, k.boyut, k.boyut);

        }

    });



    // Özel Güç Simgelerini Çiz

    gucSimgeleri.forEach(g => {

        ctx.beginPath();

        ctx.arc(g.x + g.boyut / 2, g.y + g.boyut / 2, g.boyut / 2, 0, Math.PI * 2);

        ctx.fillStyle = g.tip === 'zaman' ? "rgba(0, 200, 255, 0.8)" : "rgba(255, 50, 50, 0.8)";

        ctx.fill();

        ctx.strokeStyle = "white";

        ctx.lineWidth = 2;

        ctx.stroke();

        

        ctx.fillStyle = "white";

        ctx.font = "20px Arial";

        ctx.textAlign = "center";

        ctx.textBaseline = "middle";

        ctx.fillText(g.tip === 'zaman' ? "⏳" : "🔫", g.x + g.boyut / 2, g.y + g.boyut / 2);

    });



    // Partiküller

    partikuller.forEach(p => {

        ctx.globalAlpha = p.omur;

        ctx.fillStyle = p.renk;

        ctx.fillRect(p.x, p.y, 3, 3);

    });

    ctx.globalAlpha = 1.0;



    // Mermileri Çiz

    ctx.fillStyle = "yellow";

    mermiler.forEach(m => {

        ctx.fillRect(m.x, m.y, m.boyutX, m.boyutY);

    });



    // Roket (Güvenli Çizim)

    if (roket.resim.complete && roket.resim.naturalWidth !== 0) {

        ctx.drawImage(roket.resim, roket.x, roket.y, roket.boyut, roket.boyut);

    }



    // Meteorlar (Güvenli Çizim)

    meteorlar.forEach(meteor => {

        if (meteorGorseli.complete && meteorGorseli.naturalWidth !== 0) {

            ctx.drawImage(meteorGorseli, meteor.x, meteor.y, meteor.boyut, meteor.boyut);

        }

    });



    ctx.restore();



    // --- UI Elemanları ---

    // Can Barı

    ctx.fillStyle = "#333";

    ctx.fillRect(20, 20, 200, 20);

    let canOrani = (roket.can / roket.maksCan);

    ctx.fillStyle = canOrani > 0.4 ? "#2ecc71" : "#e74c3c";

    ctx.fillRect(20, 20, 200 * canOrani, 20);

    ctx.strokeStyle = "white";

    ctx.strokeRect(20, 20, 200, 20);



    // Kedi Sayacı ve Seviye

    ctx.fillStyle = "white";

    ctx.font = "bold 20px 'Times New Roman'";

    ctx.textAlign = "left";

    ctx.fillText("Toplanan Kediler: " + toplananKediler + " / " + hedefKediSayisi, 20, 65);

    ctx.fillText("Seviye: " + seviye, 20, 90);

    

    // Aktif Güç Göstergeleri

    if (meteorYavaslaticiSayac > 0) {

        ctx.fillStyle = "#00c8ff";

        ctx.fillText("Zaman Yavaşlatıldı: " + Math.ceil(meteorYavaslaticiSayac / 60) + "s", 20, 120);

    }

    if (mermiBuffSayac > 0) {

        ctx.fillStyle = "#ff3232";

        ctx.fillText("Hızlı Mermi: " + Math.ceil(mermiBuffSayac / 60) + "s", 20, 145);

    }

    

    if (hedef.gorunurMu) {

        ctx.fillStyle = "#f1c40f";

        ctx.textAlign = "center";

        ctx.fillText("GEZEGEN GÖRÜNDÜ! KEDİLERİ ULAŞTIR!", canvas.width / 2, 100);

    }

}

        

function oyunBitti() {

    oyunDevamEdiyor = false;

    alert("Meteor çarptı! Görev başarısız.");

    location.reload(); 

}

-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------


prompt:

şimdi aynı oyuna şunları ekler misin:

- bazı meteorların üzerinde sayılar yazsın . üzerine o sayı kadar mermi gelmeden yok olmasın .

- bir özel güç daha ekleyelim bu özel gücün simgesi üç tane mermi olsun ve eğer onu alırsak roket 10 saniye boyunca üçerli mermi atmaya başlasın.

-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------


Ai cevabı:



Harika fikirler! Oyunun mekaniğini çok daha zevkli ve stratejik bir hale getirecek bu güncellemeler.

İstediğin gibi:



Meteorlara Can (Health) Eklendi: Meteorların %30'u "dayanıklı" olarak doğacak ve üzerinde 2, 3 veya 4 gibi sayılar yazacak. Mermi isabet ettikçe bu sayı düşecek ve 0 olunca patlayacaklar. Normal meteorlar (1 canlı) üzerinde sayı yazmadan tek atışta yok olmaya devam edecek.

3x Mermi Gücü: Ekrana "3x" simgesiyle (mor renkli) düşen yeni bir özel güç eklendi. Bunu aldığında 10 saniye boyunca roketin sağından, solundan ve ortasından 3 adet mermi çıkacak.



// 1. Değişkenleri Tanımlayalım

let canvas, ctx;

let oyunDevamEdiyor = false;

let oyunSuresiFrames = 0; // Süreye bağlı hız artışı için sayaç



// Oyuncu (roket) Objesi 

let roket = {

    x: 100,

    y: 100,

    vx: 0, 

    vy: 0, 

    ivme: 0.2, 

    surtunme: 0.96, 

    boyut: 50, 

    can: 100,

    maksCan: 100

};



// Mermi Değişkenleri

let mermiler = [];

let sonAtesZamani = 0;

let atesGecikmesi = 15; // Mermiler arası bekleme süresi (Frame)



// Özel Güç Değişkenleri

let gucSimgeleri = [];

let meteorHizCarpani = 1;

let meteorYavaslaticiSayac = 0;

let mermiHizCarpani = 1;

let mermiBuffSayac = 0;

let ucluMermiSayac = 0; // 3x Mermi için sayaç



let toplananKediler = 0;

let hedefKediSayisi = 30;

let seviye = 1;



let kediler = [];

const kediGorseli = new Image();

kediGorseli.src = 'images/kedi.png';



const roketGorseli = new Image();

roketGorseli.src = 'images/uzay_gemisi.png'; 

roket.resim = roketGorseli;



// Hedef (Gezegen) Objesi

const gezegenGorseli = new Image();

gezegenGorseli.src = 'images/gezegen.png'; 



let hedef = {

    y: -450, 

    boyut: 400,

    mesafe: 3000, 

    gorunurMu: false

};



let tuslar = {};

let meteorlar = [];

let meteorHizi = 0.25; 

let partikuller = []; 

let yildizlar = [];    

let sarsintiSuresi = 0; 

const meteorGorseli = new Image();

meteorGorseli.src = 'images/meteor.png'; 



// 2. Butona tıklandığında çalışacak fonksiyon

function buton_giris() {

    var buton = document.getElementById("buton_id_1");

    buton.style.display = "none";



    canvas = document.createElement("canvas");

    ctx = canvas.getContext("2d");

    

    canvas.width = window.innerWidth;

    canvas.height = window.innerHeight;

    canvas.style.position = "absolute";

    canvas.style.top = "0";

    canvas.style.left = "0";

    canvas.style.zIndex = "10"; 

    

    document.body.appendChild(canvas);



    for(let i=0; i<100; i++) {

        yildizlar.push({

            x: Math.random() * canvas.width,

            y: Math.random() * canvas.height,

            hiz: Math.random() * 3 + 1,

            boyut: Math.random() * 2

        });

    }



    window.addEventListener('resize', function() {

        canvas.width = window.innerWidth;

        canvas.height = window.innerHeight;

    });

    

    roket.x = canvas.width / 2 - roket.boyut / 2;

    roket.y = canvas.height / 2 - roket.boyut / 2;



    window.addEventListener("keydown", (e) => { 

        tuslar[e.key] = true; 

        if (e.key === " ") e.preventDefault(); 

    });

    window.addEventListener("keyup", (e) => { tuslar[e.key] = false; });



    oyunDevamEdiyor = true;

    oyun_dongusu();

}



function partikulOlustur(x, y, renk, adet) {

    for (let i = 0; i < adet; i++) {

        partikuller.push({

            x: x,

            y: y,

            vx: Math.random() * 6 - 3,

            vy: Math.random() * 6 - 3,

            omur: 1.0,

            renk: renk

        });

    }

}

        

function kediOlustur() {

    let boyut = 30; 

    let x = Math.random() * (canvas.width - boyut);

    kediler.push({

        x: x, y: -boyut,

        boyut: boyut,

        hiz: Math.random() * 1 + 2

    });

}



function meteorOlustur() {

    let boyut = Math.random() * (50 - 25) + 25; 

    let x = Math.random() * (canvas.width - boyut);

    

    // Meteorların %30'u zorlu olsun (2 ile 4 arası canı olsun), kalanı 1 canlı olsun.

    let meteorCani = 1;

    if (Math.random() < 0.3) {

        meteorCani = Math.floor(Math.random() * 3) + 2; // 2, 3 veya 4

    }

    

    meteorlar.push({

        x: x,

        y: -boyut,

        boyut: boyut,

        hiz: Math.random() * 1 + meteorHizi,

        can: meteorCani

    });

}



function gucOlustur() {

    let boyut = 30;

    let x = Math.random() * (canvas.width - boyut);

    

    // Güç türünü rastgele seç (3 türden biri)

    let tipRastgele = Math.random();

    let tip = '';

    if (tipRastgele < 0.33) {

        tip = 'zaman';

    } else if (tipRastgele < 0.66) {

        tip = 'mermi';

    } else {

        tip = 'uclu_mermi';

    }

    

    gucSimgeleri.push({

        x: x,

        y: -boyut,

        boyut: boyut,

        hiz: 2,

        tip: tip

    });

}



// 3. Ana Oyun Döngüsü

function oyun_dongusu() {

    if (!oyunDevamEdiyor) return;



    guncelle();

    ciz();



    requestAnimationFrame(oyun_dongusu);

}



function guncelle() {

    oyunSuresiFrames++;

    

    if (oyunSuresiFrames % 60 === 0) {

        meteorHizi += 0.01;

    }



    // Özel Güç Sayaçlarını Güncelle

    if (meteorYavaslaticiSayac > 0) {

        meteorYavaslaticiSayac--;

        if (meteorYavaslaticiSayac === 0) meteorHizCarpani = 1;

    }

    if (mermiBuffSayac > 0) {

        mermiBuffSayac--;

        if (mermiBuffSayac === 0) mermiHizCarpani = 1;

    }

    if (ucluMermiSayac > 0) {

        ucluMermiSayac--;

    }



    // Momentum Hareketi

    if (tuslar["ArrowUp"] || tuslar["w"]) roket.vy -= roket.ivme;

    if (tuslar["ArrowDown"] || tuslar["s"]) roket.vy += roket.ivme;

    if (tuslar["ArrowLeft"] || tuslar["a"]) roket.vx -= roket.ivme;

    if (tuslar["ArrowRight"] || tuslar["d"]) roket.vx += roket.ivme;



    // Ateş Etme

    if (tuslar[" "] && sonAtesZamani <= 0) {

        let hizY = 10 * mermiHizCarpani;

        

        if (ucluMermiSayac > 0) {

            // 3 mermi at

            mermiler.push({ x: roket.x + roket.boyut / 2 - 2, y: roket.y, boyutX: 4, boyutY: 15, hiz: hizY }); // Orta

            mermiler.push({ x: roket.x + roket.boyut / 2 - 15, y: roket.y + 10, boyutX: 4, boyutY: 15, hiz: hizY }); // Sol

            mermiler.push({ x: roket.x + roket.boyut / 2 + 11, y: roket.y + 10, boyutX: 4, boyutY: 15, hiz: hizY }); // Sağ

        } else {

            // Tek mermi at

            mermiler.push({ x: roket.x + roket.boyut / 2 - 2, y: roket.y, boyutX: 4, boyutY: 15, hiz: hizY });

        }

        sonAtesZamani = atesGecikmesi;

    }

    if (sonAtesZamani > 0) sonAtesZamani--;



    roket.vx *= roket.surtunme;

    roket.vy *= roket.surtunme;

    roket.x += roket.vx;

    roket.y += roket.vy;



    // Egzoz Partikülleri

    if (Math.abs(roket.vx) > 0.5 || Math.abs(roket.vy) > 0.5) {

        partikulOlustur(roket.x + roket.boyut / 2, roket.y + roket.boyut - 5, "orange", 1);

    }



    // Ekran Sınırları

    if (roket.x < 0) { roket.x = 0; roket.vx *= -0.5; }

    if (roket.y < 0) { roket.y = 0; roket.vy *= -0.5; }

    if (roket.x + roket.boyut > canvas.width) { roket.x = canvas.width - roket.boyut; roket.vx *= -0.5; }

    if (roket.y + roket.boyut > canvas.height) { roket.y = canvas.height - roket.boyut; roket.vy *= -0.5; }



    // Yıldızlar

    yildizlar.forEach(y => {

        y.y += y.hiz;

        if (y.y > canvas.height) y.y = 0;

    });



    // Mermiler ve Meteorları Vurma

    for (let i = 0; i < mermiler.length; i++) {

        let m = mermiler[i];

        m.y -= m.hiz;

        let vuruldu = false;



        for (let j = 0; j < meteorlar.length; j++) {

            let met = meteorlar[j];

            if (m.x < met.x + met.boyut && m.x + m.boyutX > met.x &&

                m.y < met.y + met.boyut && m.y + m.boyutY > met.y) {

                

                // Mermi meteor'a çarptığında ufak bir sarı partikül çıksın

                partikulOlustur(m.x, m.y, "yellow", 5);

                

                met.can--; // Meteorun canını düşür

                if (met.can <= 0) {

                    partikulOlustur(met.x + met.boyut / 2, met.y + met.boyut / 2, "gray", 15);

                    meteorlar.splice(j, 1);

                }

                

                vuruldu = true;

                break;

            }

        }



        if (vuruldu) {

            mermiler.splice(i, 1); i--; continue;

        }

        if (m.y < 0) { mermiler.splice(i, 1); i--; }

    }



    // Özel Güç Çıkma İhtimali

    if (Math.random() < 0.002) { gucOlustur(); }



    // Özel Güçlerin Düşmesi ve Toplanması

    for (let i = 0; i < gucSimgeleri.length; i++) {

        let g = gucSimgeleri[i];

        g.y += g.hiz;



        // Roket ile özel güç çarpışması

        if (roket.x < g.x + g.boyut && roket.x + roket.boyut > g.x &&

            roket.y < g.y + g.boyut && roket.y + roket.boyut > g.y) {

            

            if (g.tip === 'zaman') {

                meteorHizCarpani = 0.5; 

                meteorYavaslaticiSayac = 7 * 60; 

                partikulOlustur(roket.x + roket.boyut / 2, roket.y, "#00c8ff", 20);

            } else if (g.tip === 'mermi') {

                mermiHizCarpani = 2; 

                mermiBuffSayac = 10 * 60; 

                partikulOlustur(roket.x + roket.boyut / 2, roket.y, "#ff3232", 20);

            } else if (g.tip === 'uclu_mermi') {

                ucluMermiSayac = 10 * 60; 

                partikulOlustur(roket.x + roket.boyut / 2, roket.y, "#9b59b6", 20);

            }

            

            gucSimgeleri.splice(i, 1); i--;

            continue;

        }



        if (g.y > canvas.height) { gucSimgeleri.splice(i, 1); i--; }

    }



    // Kedi Toplama ve Hedef Kontrolü

    if (toplananKediler < hedefKediSayisi && Math.random() < 0.015) { 

        kediOlustur(); 

    } else if (toplananKediler >= hedefKediSayisi) {

        hedef.gorunurMu = true;

    }



    // Gezegen Hareketi

    if (hedef.gorunurMu) {

        hedef.y += 1.2;

        if (roket.y < hedef.y + hedef.boyut / 2 && Math.abs(roket.x - (canvas.width/2 - roket.boyut/2)) < 200) {

            seviyeAtla();

        }

        if (hedef.y > canvas.height) { 

            hedef.y = -450;

        }

    }



    // Meteorlar

    if (Math.random() < 0.02) { meteorOlustur(); }



    // Meteor Çarpışma

    for (let i = 0; i < meteorlar.length; i++) {

        let m = meteorlar[i];

        m.y += m.hiz * meteorHizCarpani; 



        if (roket.x < m.x + m.boyut && roket.x + roket.boyut > m.x &&

            roket.y < m.y + m.boyut && roket.y + roket.boyut > m.y) {

            roket.can -= 20;

            sarsintiSuresi = 10;

            partikulOlustur(m.x + m.boyut / 2, m.y + m.boyut / 2, "gray", 15);

            meteorlar.splice(i, 1); i--;

            if (roket.can <= 0) { oyunBitti(); return; }

            continue;

        }

        if (m.y > canvas.height) { meteorlar.splice(i, 1); i--; }

    }



    // Kedi Toplama Çarpışma

    for (let i = 0; i < kediler.length; i++) {

        let k = kediler[i];

        k.y += k.hiz;

        if (roket.x < k.x + k.boyut && roket.x + roket.boyut > k.x &&

            roket.y < k.y + k.boyut && roket.y + roket.boyut > k.y) {

            toplananKediler++;

            partikulOlustur(k.x + k.boyut / 2, k.y + k.boyut / 2, "#f39c12", 10);

            kediler.splice(i, 1); i--;

            continue;

        }

        if (k.y > canvas.height) { kediler.splice(i, 1); i--; }

    }



    // Partikül Güncelleme

    for (let i = 0; i < partikuller.length; i++) {

        let p = partikuller[i];

        p.x += p.vx; p.y += p.vy; p.omur -= 0.02;

        if (p.omur <= 0) { partikuller.splice(i, 1); i--; }

    }



    if (sarsintiSuresi > 0) sarsintiSuresi--;

}



function seviyeAtla() {

    meteorlar = []; 

    kediler = []; 

    mermiler = [];

    gucSimgeleri = [];

    seviye++;

    toplananKediler = 0;

    hedef.gorunurMu = false;

    hedef.y = -450;

    meteorHizi += 0.25; 

    roket.can = Math.min(roket.can + 30, 100); 

    partikulOlustur(canvas.width / 2, canvas.height / 2, "white", 50);

    alert("Kediler Güvende! Seviye " + seviye + " başlıyor. Meteorlar artık daha hızlı düşecek!");

}



// 5. Çizim Kısmı (Güvenli Çizim Modu)

function ciz() {

    ctx.clearRect(0, 0, canvas.width, canvas.height);



    ctx.save();

    if (sarsintiSuresi > 0) {

        ctx.translate(Math.random() * 10 - 5, Math.random() * 10 - 5);

    }



    // Yıldızlar

    ctx.fillStyle = "white";

    yildizlar.forEach(y => { ctx.fillRect(y.x, y.y, y.boyut, y.boyut); });



    // Gezegen

    if (hedef.gorunurMu && gezegenGorseli.complete && gezegenGorseli.naturalWidth !== 0) {

        ctx.drawImage(gezegenGorseli, (canvas.width / 2) - (hedef.boyut / 2), hedef.y, hedef.boyut, hedef.boyut);

    }



    // Kediler 

    kediler.forEach(k => {

        if (kediGorseli.complete && kediGorseli.naturalWidth !== 0) {

            ctx.drawImage(kediGorseli, k.x, k.y, k.boyut, k.boyut);

        }

    });



    // Özel Güç Simgelerini Çiz

    gucSimgeleri.forEach(g => {

        ctx.beginPath();

        ctx.arc(g.x + g.boyut / 2, g.y + g.boyut / 2, g.boyut / 2, 0, Math.PI * 2);

        

        let renk = "";

        let sembol = "";

        if (g.tip === 'zaman') { renk = "rgba(0, 200, 255, 0.8)"; sembol = "⏳"; }

        else if (g.tip === 'mermi') { renk = "rgba(255, 50, 50, 0.8)"; sembol = "🔫"; }

        else if (g.tip === 'uclu_mermi') { renk = "rgba(155, 89, 182, 0.8)"; sembol = "3x"; }



        ctx.fillStyle = renk;

        ctx.fill();

        ctx.strokeStyle = "white";

        ctx.lineWidth = 2;

        ctx.stroke();

        

        ctx.fillStyle = "white";

        ctx.font = "bold 14px Arial";

        ctx.textAlign = "center";

        ctx.textBaseline = "middle";

        ctx.fillText(sembol, g.x + g.boyut / 2, g.y + g.boyut / 2);

    });



    // Partiküller

    partikuller.forEach(p => {

        ctx.globalAlpha = p.omur;

        ctx.fillStyle = p.renk;

        ctx.fillRect(p.x, p.y, 3, 3);

    });

    ctx.globalAlpha = 1.0;



    // Mermileri Çiz

    ctx.fillStyle = "yellow";

    mermiler.forEach(m => {

        ctx.fillRect(m.x, m.y, m.boyutX, m.boyutY);

    });



    // Roket 

    if (roket.resim.complete && roket.resim.naturalWidth !== 0) {

        ctx.drawImage(roket.resim, roket.x, roket.y, roket.boyut, roket.boyut);

    }



    // Meteorlar 

    meteorlar.forEach(meteor => {

        if (meteorGorseli.complete && meteorGorseli.naturalWidth !== 0) {

            ctx.drawImage(meteorGorseli, meteor.x, meteor.y, meteor.boyut, meteor.boyut);

            

            // Eğer meteorun canı 1'den fazlaysa üzerine canını yazdır

            if (meteor.can > 1) {

                ctx.fillStyle = "white";

                ctx.font = "bold 16px Arial";

                ctx.textAlign = "center";

                ctx.textBaseline = "middle";

                ctx.fillText(meteor.can, meteor.x + meteor.boyut / 2, meteor.y + meteor.boyut / 2);

            }

        }

    });



    ctx.restore();



    // --- UI Elemanları ---

    // Can Barı

    ctx.fillStyle = "#333";

    ctx.fillRect(20, 20, 200, 20);

    let canOrani = (roket.can / roket.maksCan);

    ctx.fillStyle = canOrani > 0.4 ? "#2ecc71" : "#e74c3c";

    ctx.fillRect(20, 20, 200 * canOrani, 20);

    ctx.strokeStyle = "white";

    ctx.strokeRect(20, 20, 200, 20);



    // Kedi Sayacı ve Seviye

    ctx.fillStyle = "white";

    ctx.font = "bold 20px 'Times New Roman'";

    ctx.textAlign = "left";

    ctx.fillText("Toplanan Kediler: " + toplananKediler + " / " + hedefKediSayisi, 20, 65);

    ctx.fillText("Seviye: " + seviye, 20, 90);

    

    // Aktif Güç Göstergeleri

    let uiY = 120; // Güç göstergelerinin alt alta düzgün dizilmesi için

    if (meteorYavaslaticiSayac > 0) {

        ctx.fillStyle = "#00c8ff";

        ctx.fillText("Zaman Yavaşlatıldı: " + Math.ceil(meteorYavaslaticiSayac / 60) + "s", 20, uiY);

        uiY += 25;

    }

    if (mermiBuffSayac > 0) {

        ctx.fillStyle = "#ff3232";

        ctx.fillText("Hızlı Mermi: " + Math.ceil(mermiBuffSayac / 60) + "s", 20, uiY);

        uiY += 25;

    }

    if (ucluMermiSayac > 0) {

        ctx.fillStyle = "#9b59b6";

        ctx.fillText("Üçlü Mermi: " + Math.ceil(ucluMermiSayac / 60) + "s", 20, uiY);

    }

    

    if (hedef.gorunurMu) {

        ctx.fillStyle = "#f1c40f";

        ctx.textAlign = "center";

        ctx.fillText("GEZEGEN GÖRÜNDÜ! KEDİLERİ ULAŞTIR!", canvas.width / 2, 100);

    }

}

        

function oyunBitti() {

    oyunDevamEdiyor = false;

    alert("Meteor çarptı! Görev başarısız.");

    location.reload(); 

}
-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
