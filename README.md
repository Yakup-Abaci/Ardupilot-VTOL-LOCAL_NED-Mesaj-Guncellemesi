# VTOL Drone için Hız Kontrollü LOCAL_NED Tabanlı Uçuş (ArduPilot Modifikasyonu)
Bu repo, **ArduPilot açık kaynak uçuş kontrol yazılımı** üzerinde yapılan geliştirmeleri içermektedir.
Çalışma kapsamında, **VTOL (Vertical Take-Off and Landing)** yapısına sahip bir hava aracının **drone (multirotor) modunda**, yalnızca konum hedefi yerine **hız tabanlı** olarak kontrollü şekilde hareket etmesi sağlanmıştır.

Geliştirilen yapı sayesinde araç:

- Maksimum hız yerine **sabit hızla** ilerleyebilmekte
- **Düşük hızlarda kararlı uçuş** gerçekleştirebilmekte
- **Ani frenleme** yapabilmekte
- **Takip (tracking) ve hedef izleme** senaryoları için uygun hale gelmiştir

## VTOL Nedir?

VTOL (Vertical Take-Off and Landing), hava araçlarının **dikey kalkış ve iniş** yapabilmesini sağlayan bir konsepttir.
VTOL araçlar genellikle iki farklı uçuş moduna sahiptir:
- **Multirotor (Drone) Modu**:
	Düşük hız, hassas manevra ve stabil kontrol sağlar.

- **Fixed-Wing (Uçak) Modu**:
	Uzun menzil ve yüksek hız için kullanılır.

Bu çalışma, özellikle **VTOL araçların multirotor modundaki kontrol kabiliyetini** geliştirmeye odaklanmıştır.

## Problemin Tanımı

ArduPilot’un standart kullanımında:
- Hareket komutları çoğunlukla **konum (position) hedefli** çalışır
- Araç, hedefe giderken **maksimum ivme ve hız sınırlarına** göre hareket eder
- Düşük hızda kararlı uçuş, hız sabitleme veya ani durma gibi senaryolar **sınırlı** kalır

Bu durum özellikle:
- Hedef takibi
- Görüntü tabanlı izleme
- Hassas yaklaşma manevraları
için yeterli değildir.

## Geliştirilen Çözüm

Bu repo kapsamında ArduPilot içerisinde **LOCAL_NED mesaj yapısı** üzerinde değişiklikler yapılmıştır.

**Yapılan Ana Değişiklikler**:
- **LOCAL_NED mesajı**, konum yerine **hız (velocity)** bilgisini referans alacak şekilde güncellendi
- X (North), Y (East) ve Z (Down) eksenlerinde verilen hız değerleri:
  - Araç tarafından **doğrudan hız hedefi** olarak algılanır
  - VTOL araç **4 motorunu aktif kullanarak** bu hızda hareket eder
- Hız değeri sıfırlandığında araç **aktif frenleme** yaparak durur.

## Kazanımlar

Bu modifikasyon ile aşağıdaki kabiliyetler elde edilmiştir:

- **Hız Sabitleme (Cruise Control benzeri yapı)**
- **Ani Frenleme (Active Braking)**
- **Düşük Hızlarda Kararlı Uçuş**
- **Takip ve İzleme Senaryolarına Uygunluk**
- **Maksimum hız bağımlılığının kaldırılması**

Bu sayede VTOL araç, özellikle:

- Görüntü işleme destekli hedef takibi
- Sabit hızda ilerleyen nesneleri izleme
- Hassas yaklaşma ve konumlama

senaryolarında **operasyonel olarak kullanılabilir** hale gelmiştir.

## Uçuş Mantığı (Özet)

1. Araç **VTOL – Multirotor (Drone) modunda** çalışır

2. Yer istasyonundan veya harici bir yazılımdan:
 - LOCAL_NED üzerinden **X, Y, Z hız değerleri** gönderilir

3. Uçuş kontrolcüsü:
 - Konum hedefi yerine **hız hedefini** takip eder

4. Araç:
 - Verilen hızda ilerler
 - Hız sıfırlandığında kontrollü şekilde durur

## Kullanım Alanları

Bu çalışma özellikle aşağıdaki alanlar için uygundur:

- 🎯 Hedef takip sistemleri
- 🎥 Görüntü tabanlı izleme (vision-based tracking)
- 🚁 VTOL platformlar
- 🧪 Otonom uçuş ve kontrol algoritmaları
- 🛡️ Savunma & havacılık Ar-Ge çalışmaları

## Demo Video


https://github.com/user-attachments/assets/a8210773-415b-45ec-aae2-210911a9bfd8



## Teknik Notlar

- Bu repo, **ArduPilot ana dalının birebir kopyası değildir**
- Açık kaynak ArduPilot üzerinde **deneysel ve araştırma amaçlı** değişiklikler içermektedir
- Gerçek uçuşlarda kullanmadan önce **simülasyon (SITL)** testleri önerilir.

## Gelecek Geliştirmeler

- PID bazlı hız kontrol optimizasyonu
- İvme sınırlama (acceleration limiting)
- Görüntü işleme sistemleriyle entegrasyon
- Fixed-wing moda geçiş sırasında hız sürekliliği
