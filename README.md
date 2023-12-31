---ALGORİTMA ÖDEVİ:AÇIK ARTIRMA UYGULAMASI ---
Bu program bir açık artırma uygulamasıdır.

Bu program katılımcılardan teklif girmesini isteycektir.Programın amacı girilen değerler arasında en yüksek olanı seçmektir.

C programlama dilinde, struct (yapı), bir bellek bloğunda tek bir ad altında fiziksel olarak gruplandırılmış değişkenler listesini tanımlayan ve farklı değişkenlere tek bir işaretçi (pointer) aracılığıyla erişilmesine izin veren bileşik bir veri türüdür. 
Struct veri tipi, başka veri türlerini içerebilir.
Typedef ise ifadesini kullanarak, standart veri türlerinini (int, char, float, vs.) veya kullanıcı tanımlı yapıları farklı isimlerle tanımlayabiliriz.

Mevcut Dosya Üzerinden İşlem seçeneği seçildiği surette "input.txt" adlı dosya baz alınacak ve işlemler bu dosya üzerinden yürütülecektir. Yeni Dosya Oluşturma seçeneği seçildiği surette program size özel bir "input.txt" dosyası oluşturacaktır. 
Bunun haricinde kullanıcı, takviye olarak yeni bir dosya oluşturmak isterse "exe." dosyasının klasörüne yeni bir "txt." dosyası oluşturabilir ve kod içine yeni oluşturulan dosyanın adını entegre edebilir.



****PROGRAMIN MANTIĞI***
Program ilk önce kaç tane katılımcı oldugunun belirlenmesini isteyecektir.Örneğin katılımcı 5 ise hepsi bir teklif verecektir.Program hangisinin teklifi en yüksekse onu seçecekktir ve kazananı belirleyecektir.
Programda sonsuz bi döngü olacak şekilde etaplar vardır.İlk etap böylece bitecektir ardından eger katılımcılardan bazıları ya da hepsi daha yüksek bir teklif vermek isterlerse ikinci etaba gecilebilir.
Bir etaptan diğerine gecmek için "e" harfine basarsanız diğer etaba gecebilirsiniz eger "h" ye basarsanız program duracaktır.




******PROGRAMIN KODU*******

#include <stdio.h>

#define MAX_KATILIMCI 100

// Açık artırma için bir yapı (struct) tanımlanıyor
typedef struct AcikArtirma {
    double odeme;               // Toplam ödeme miktarı
   
    int kazanan_no;             // Kazanan katılımcının numarası
   
    double en_yuksek_teklif;    // En yüksek teklif miktarı
    int katilimci_sayisi;       // Katılan katılımcı sayısı
    double teklifler[MAX_KATILIMCI];  // Katılımcıların teklifleri
} AçıkArtırma;  // typedef ile yapıyı AçıkArtırma adı altında tanımlıyoruz

// Kazananın bilgilerini ekrana yazdırmak için bir fonksiyon tanımlanıyor

void goster_kazanan(int kazanan_no, double teklif) {
    printf("Kazanan katilimci: %d, Teklif: %.2f\n", kazanan_no + 1, teklif);
}

// Şu an kullanılmayan ödeme hesaplama fonksiyonu

double hesapla_odeme(AcikArtirma *a, int kazanan_no) {
    return a->odeme;  // Açık artırma yapısı içindeki ödeme miktarını geri döndürür
}

// Toplam ödeme miktarını ekrana yazdırmak için bir fonksiyon tanımlanıyor
void goster_odeme(double odeme) {
    printf("Toplam odeme: %.2f\n", odeme);
}

int main() {
   
    // Açık artırma yapısı oluşturuluyor ve başlangıç değerleri atanıyor
   
    struct AcikArtirma a = {0.0, -1, -1.0, 0, {0}};
    
    int kisi_sayisi;  // Kullanıcıdan alınacak katılımcı sayısını tutacak değişken
    
    char devam;  // Kullanıcının devam etmek isteyip istemediğini tutacak değişken

    while (1) { // Sonsuz bir döngü başlatılıyor
        printf("Kac kisi katilacak: ");
        scanf("%d", &kisi_sayisi); // Kullanıcıdan katılımcı sayısını alıyor

        printf("Katilimcilarin tekliflerini girin:\n");
        int i;
        for (i = 0; i < kisi_sayisi; ++i) {
            printf("Katilimci %d'in teklifi: ", i + 1);
            scanf("%lf", &a.teklifler[i]); // Her bir katılımcının teklifini alıyor

            if (a.teklifler[i] > a.en_yuksek_teklif) {
                a.en_yuksek_teklif = a.teklifler[i]; // En yüksek teklifi güncelliyor
                a.kazanan_no = i; // Kazanan katılımcı numarasını güncelliyor
            }
        }

        a.katilimci_sayisi = kisi_sayisi; // Katılımcı sayısını güncelliyor

        goster_kazanan(a.kazanan_no, a.teklifler[a.kazanan_no]); // Kazananı ve teklifi ekrana yazdırıyor

        printf("Devam etmek istiyor musunuz? (e/h): ");
        scanf(" %c", &devam); // Kullanıcıdan devam etmek isteyip istemediğini alıyor

        if (devam == 'h' || devam == 'H') { // Eğer devam etmek istemiyorsa döngüden çıkıyor
            break;
        }
    }

    return 0; // Programın başarıyla sonlandığını belirtiyor
}
