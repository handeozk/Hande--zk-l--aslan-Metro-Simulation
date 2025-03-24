Proje Başlığı: Metro Simülasyon Projesi
Proje hakkında kısa açıklama: Bu projede şehir içi bir metro ağındaki istasyonlar içinde başlangıç ve hedef istasyonları belirlenerek, bu istasyonlar arasındaki en az aktarmalı ve en kısa süreli yolun nasıl gidileceği kullanıcıya sunulur.
Projede kullanılan teknolojiler ve kütüphaneler: Projede Python dili kullanılmıştır. Google collab üzerinden kodun çalışılabilirliği ve senaryolar test edilmiştir. Projede collections modülünden defaultdict ve deque işlemleri, heapq ve typing modülü kullanılmıştır. Collections modülünden deque işlemiyle oluşturulan verilerin iki ucuna da ekleme ve çıkarma işlemini hızlı bir şekilde yapılması sağlanmıştır. Defaultdict işlemiyleanlamsız veya var olmayan verileri anlamlı bir cevaba dönüştürülmesi hedeflenmiştir. Heapq modülüyle yığın içinde tanımlanan en küçük değere sahip verilerin öncelikli olarak seçilmesi hedeflenmiştir. Type modülü ile de kullanılan verilerdeki nesnelerin uygun parametrede olması sağlanmıştır.
Bu projede 2 farklı algoritme kullanılmıştır. Metro istasyonları arasındaki en az aktarmalı yolu bulabilmek için BFS algoritması kullanılırken, en kısa süreli yolu bulabilmek için A* algoritması kullanılmıştır.
BFS algoritması: Buradaki amaç geniş öncelikli arama yapmaktır. Geniş öncelikli arama yapmak için deque veri yapısı kullanılır. Buradaki neden FIFO mantığından yararlanmaktır. Bu algoritmayla başlangıç seçilen ilk istasyon veri yığınından ilk çıkarılan olacak ve başlangıç olarak seçilecektir. Başlangıç istasyonun komşu istasyonları ise ziyaret edilerek yığından çıkarılarak kuyruğa eklenmeye devam edecektir. Böylece hedef istasyona ulaşana kadar yığından çıkartılan istasyonlar bir kuyruk oluşturacaktır. Eğer istasyonlardan daha önce ziyaret edilen varsa bu istasyonlar tekrar kuyruğa alınmayacak ve o istasyonun komşu istasyonlarına gidilecektir, devamında komşu istasyonları da kuyruğa eklenecektir. Bu algoritma sayesinde en az aktarmalı yol bulunarak başlangıçtan hedef istasyona ulaşım sağlanacaktır. BFS algoritmasının burada kullanılan özelliği esas olarak bir düğümün komşularını keşfetmek ve en kısa yolu kullanarak hedef düğüme ulaşmaktır.
A* algoritması: Bu algoritmada hedefe ulaşmak için en kısa yol ile beraber maliyeti de hesaplayarak en verimli yolun da kullanılması amaçlanır ve bunu yaparken sezgisel yöntemler kullanılır. Bu algoritmanın daha verimli olmasının nedeni hedefe daha yakın olan düğümlere öncelik vermesidir. f= g+ h denklemi kullanılır. Burada g olarak ifade ettiğimiz fonksiyon başlangıçtan bizim bulundupğumuz pozisyona getiren maliyet iken h fonksiyonu biizm pozisyonumuzdan hedefe giden maliyet ve bunların toplamının f fonksiyonuna eşit olmasıdır. Burada manhattan ve öklid uzaklıkları kullanılarak maliyet hesaplaması yapıldığında f'in en küçük olduğu nodlar arası yol algoritma tarafından seçilir. Bu algoritmanın projede kullanılmasının nedeni metrodaki istasyonlar arası geçen sürenin maliyetinin en aza indirilmesi amaçlanan en kısa sürede başlangıç ve hedef arası yolun nasıl gidileceği sorusunun cevabının bulunmasıdır. 
Örnek kullanım ve test sonuçları: Oluşturulan kod ile birlikte bir metro istasyonları ve metro ağı örneklemi oluşturularak bu örneklem üzerinden 4 farklı senaryo oluşturulmuştur. 4 farklı senaryo kod ile çalıştırıldığı zaman BFS algoritması ile en az aktarmalı yol cevabını alırken, A* algoritması ile en kısa süreli yol cevabı alınmıştır. Bu örneklem ve senaryoların çalıştırması ile alınan cevaplar sayesinde kodun çalışılırlığı ve güvenilirliği test edilmiştir.
Örnek kullanım: 
if __name__ == "__main__":
    metro = MetroAgi()
    
    # İstasyonlar ekleme
    # Kırmızı Hat
    metro.istasyon_ekle("K1", "Kızılay", "Kırmızı Hat")
    metro.istasyon_ekle("K2", "Ulus", "Kırmızı Hat")
    metro.istasyon_ekle("K3", "Demetevler", "Kırmızı Hat")
    metro.istasyon_ekle("K4", "OSB", "Kırmızı Hat")
    
    # Mavi Hat
    metro.istasyon_ekle("M1", "AŞTİ", "Mavi Hat")
    metro.istasyon_ekle("M2", "Kızılay", "Mavi Hat")  # Aktarma noktası
    metro.istasyon_ekle("M3", "Sıhhiye", "Mavi Hat")
    metro.istasyon_ekle("M4", "Gar", "Mavi Hat")
    
    # Turuncu Hat
    metro.istasyon_ekle("T1", "Batıkent", "Turuncu Hat")
    metro.istasyon_ekle("T2", "Demetevler", "Turuncu Hat")  # Aktarma noktası
    metro.istasyon_ekle("T3", "Gar", "Turuncu Hat")  # Aktarma noktası
    metro.istasyon_ekle("T4", "Keçiören", "Turuncu Hat")
    
    # Bağlantılar ekleme
    # Kırmızı Hat bağlantıları
    metro.baglanti_ekle("K1", "K2", 4)  # Kızılay -> Ulus
    metro.baglanti_ekle("K2", "K3", 6)  # Ulus -> Demetevler
    metro.baglanti_ekle("K3", "K4", 8)  # Demetevler -> OSB
    
    # Mavi Hat bağlantıları
    metro.baglanti_ekle("M1", "M2", 5)  # AŞTİ -> Kızılay
    metro.baglanti_ekle("M2", "M3", 3)  # Kızılay -> Sıhhiye
    metro.baglanti_ekle("M3", "M4", 4)  # Sıhhiye -> Gar
    
    # Turuncu Hat bağlantıları
    metro.baglanti_ekle("T1", "T2", 7)  # Batıkent -> Demetevler
    metro.baglanti_ekle("T2", "T3", 9)  # Demetevler -> Gar
    metro.baglanti_ekle("T3", "T4", 5)  # Gar -> Keçiören
    
    # Hat aktarma bağlantıları (aynı istasyon farklı hatlar)
    metro.baglanti_ekle("K1", "M2", 2)  # Kızılay aktarma
    metro.baglanti_ekle("K3", "T2", 3)  # Demetevler aktarma
    metro.baglanti_ekle("M4", "T3", 2)  # Gar aktarma
    
    # Test senaryoları
    print("\n=== Test Senaryoları ===")
    
    # Senaryo 1: AŞTİ'den OSB'ye
    print("\n1. AŞTİ'den OSB'ye:")
    rota = metro.en_az_aktarma_bul("M1", "K4")
    if rota:
        print("En az aktarmalı rota:", " -> ".join(i.ad for i in rota))
    
    sonuc = metro.en_hizli_rota_bul("M1", "K4")
    if sonuc:
        rota, sure = sonuc
        print(f"En hızlı rota ({sure} dakika):", " -> ".join(i.ad for i in rota))
    
    # Senaryo 2: Batıkent'ten Keçiören'e
    print("\n2. Batıkent'ten Keçiören'e:")
    rota = metro.en_az_aktarma_bul("T1", "T4")
    if rota:
        print("En az aktarmalı rota:", " -> ".join(i.ad for i in rota))
    
    sonuc = metro.en_hizli_rota_bul("T1", "T4")
    if sonuc:
        rota, sure = sonuc
        print(f"En hızlı rota ({sure} dakika):", " -> ".join(i.ad for i in rota))
    
    # Senaryo 3: Keçiören'den AŞTİ'ye
    print("\n3. Keçiören'den AŞTİ'ye:")
    rota = metro.en_az_aktarma_bul("T4", "M1")
    if rota:
        print("En az aktarmalı rota:", " -> ".join(i.ad for i in rota))
    
    sonuc = metro.en_hizli_rota_bul("T4", "M1")
    if sonuc:
        rota, sure = sonuc
        print(f"En hızlı rota ({sure} dakika):", " -> ".join(i.ad for i in rota)) 
    
    # Senaryo 4: Ulus'tan Batıkent'e 
    print("\n4. Ulus'tan Batıkent'e:")
    rota = metro.en_az_aktarma_bul("K2", "T1")
    if rota:
        print("En az aktarmalı rota:", " -> ".join(i.ad for i in rota))
    
    sonuc = metro.en_hizli_rota_bul("K2", "T1")
    if sonuc:
        rota, sure = sonuc
        print(f"En hızlı rota ({sure} dakika):", " -> ".join(i.ad for i in rota)) 
=== Test Senaryoları ===

1. AŞTİ'den OSB'ye:
En az aktarmalı rota: AŞTİ -> Kızılay -> Kızılay -> Ulus -> Demetevler -> OSB
En hızlı rota (25 dakika): AŞTİ -> Kızılay -> Kızılay -> Ulus -> Demetevler -> OSB

2. Batıkent'ten Keçiören'e:
En az aktarmalı rota: Batıkent -> Demetevler -> Gar -> Keçiören
En hızlı rota (21 dakika): Batıkent -> Demetevler -> Gar -> Keçiören

3. Keçiören'den AŞTİ'ye:
En az aktarmalı rota: Keçiören -> Gar -> Gar -> Sıhhiye -> Kızılay -> AŞTİ
En hızlı rota (19 dakika): Keçiören -> Gar -> Gar -> Sıhhiye -> Kızılay -> AŞTİ

4. Ulus'tan Batıkent'e:
En az aktarmalı rota: Ulus -> Demetevler -> Demetevler -> Batıkent
En hızlı rota (16 dakika): Ulus -> Demetevler -> Demetevler -> Batıkent

Projeyi geliştirme fikirleri: Yapılan projede başlangıç ve hedef istasyonlar arasındaki en az aktarmalı ve en kısa süreli yol bulma başarılı bir şekilde sağlanmıştır. Bu projenin geliştirilmesinde başlangıç ve hedef istasyonlar arasında uğranması gerekli olan duraklar senaryoya eklenerek kod çalıştırıldığında araya eklenen bu duraklardan geçen bir en az aktarma ve en kısa süreli yol bulma işlemi yaptırılabilir. Projenin daha verilmli hale getirebilmesi için metro ağlarındaki tren geliş süreleri ve aktarmalar arası geçen süreler gibi kompleks veri girişleri ve bu girşler sonucu alınan farklı cevaplar kullanıcılara sunulabilir. Aynı zamanda metro ağ kullanım ücreti de yine A* algoritması kullanılarak en ekonomik yol tercihi, bu iki süre ve ücret algoritması birleştirilerek de en optimal yol bulunması işlemi de projeye eklenebilir.
