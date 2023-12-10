Algoritma sifreleme ödevi:

*Bu program  sifreleme ve deşifreleme yöntemlerine dayanan  bir programdır.

*Bu programda harfler kullanıcının istediği miktarda kayar yani ötelenir.Eğer kullanıcı bir harfi ötelemek isterse 1. seçeneği seçer eger bir kelimenin içindeki bütün harfleri ötelemek isterse bu seferde 2. Seçeneği seçer.


*İki seçenekte de üç durum vardır:

1)Şifreleme

2)Deşifreleme



Programdaki harfler İngiliz alfabesine göre ayarlanmıştır.Türkçe harf girişinde program hata verebilir.Türkce harf girmeye özen gösterin.
Harf dışında sayı girildiğinde program hata verip başa döndürecektir.

Mevcut Dosya Üzerinden İşlem seçeneği seçildiği surette "input.txt" adlı dosya baz alınacak ve işlemler bu dosya üzerinden yürütülecektir.
Yeni Dosya Oluşturma seçeneği seçildiği surette program size özel bir "input.txt" dosyası oluşturacaktır.
Bunun haricinde kullanıcı, takviye olarak yeni bir dosya oluşturmak isterse "exe." dosyasının klasörüne yeni bir "txt." dosyası oluşturabilir ve kod içine yeni oluşturulan dosyanın adını entegre edebilir.
 
 
 
 
 PROGRAMIN MANTIĞI:


Eger 1. seçeneği seçerseniz bir harf ve kaydırma miktarı girmeniz istenilecektir.Örneğin harf olarak a sayısını kaydırma miktarı olarakta 3 sayiısını seçtiniz bu harfin kaydırılmış hali d olur.Bu sifreleme metodudur.Eğer bu harfi eski haline döndürmek isterseniz deşifreleme metodunu kullanmanız gereklidir.Deşifreleme yöntemi ise seçtiğiniz harfi kaydırma miktarı ile harfi geri eski haline çeviriyor.Program size iki seçenek sunacak eğer isterseniz deşifreleme yöntemini seçerek harfi eski haline çevirebilirsiniz.Eger istemezseniz program sonlanacaktır.


Eger 2. Seçeneği seçerseniz sizden bir kelime ve kaydırma miktarı isteyecek.Aldığı kelimeyi kaydırma miktarı kadar olacak şekilde içindeki tüm harfleri ayrı ayrı kaydıracak.örnegin elma kelimesi 3 birim kaydırılmak istenirse yeni kelimemiz hopd kelimesidir.Eğer bu kelimeyi eski haline döndürmek istersek deşifreleme yöntemini seçmeliyiz.Program size iki seçenek sunacak eğer isterseniz deşifreleme  yöntemini seçerek kelimeyi eski haline çevirebilirsiniz.Eger istemezseniz program sonlanacaktır.





C dilinde kodun bağlantısı:https://1drv.ms/u/s!AktJHM3hppwRhhl_S9FVs1uqPJZX?e=W8A0o5
  


**KOD**
#include <stdio.h>

#include <string.h>

#include <ctype.h>

char sifrele(char harf, int kaydirma);          // Harfi şifreleyen fonksiyon

void kaydir(char *kelime, int kaydirma_miktari);// Kelimeyi şifreleyen fonksiyon

char desifrele(char harf, int kaydirma);       // Harfi deşifreleyen fonksiyon

char sifrele(char harf, int kaydirma) {        // Belirli bir kaydırma miktarıyla harfi şifreleyen fonksiyon
   
    if (islower(harf)) {                       // Eğer Harf küçükse
        harf = harf + kaydirma;                // Kaydırma miktarı uygulanır
       
        if (harf > 'z') {                      // Eğer 'z' değerini aşarsa
            harf = harf - 'z' + 'a' - 1;       // 'a'ya geri döner
        }
        return harf;                           // Şifrelenmiş harfi döndürür
    }
    return harf;                               // Harf büyükse aynı harfi döndürür
}

void kaydir(char *kelime, int kaydirma_miktari) {// Belirli bir kaydırma miktarıyla kelimeyi şifreleyen fonksiyon
    
    
int uzunluk = strlen(kelime);               // Kelimenin uzunluğunu alır
    
    int i;
    
    for (i = 0; i < uzunluk; i++) {            // Tüm karakterler için
        if (isalpha(kelime[i])) {               // Eğer karakter harfse
            if (islower(kelime[i])) {           // Eğer küçük harfse
                kelime[i] = 'a' + ((kelime[i] - 'a' + kaydirma_miktari) % 26); // Kaydırma işlemi
            } else if (isupper(kelime[i])) {    // Eğer büyük harfse
                kelime[i] = 'A' + ((kelime[i] - 'A' + kaydirma_miktari) % 26); // Kaydırma işlemi
            }
        }
    }
}

char desifrele(char harf, int kaydirma) {       // Belirli bir kaydırma miktarıyla harfi deşifreleyen fonksiyon
    
    if (islower(harf)) {                        // Eğer Harf küçükse
       
        harf = harf - kaydirma;                 // Kaydırma miktarı uygulanır
       
        if (harf < 'a') {                       // Eğer 'a' değerini aşarsa
            
            harf = harf + 'z' - 'a' + 1;        // 'z'ye geri döner
        }
        return harf;                            // Deşifrelenmiş harfi döndürür
    }
    return harf;                                // Harf büyükse aynı harfi döndürür
}

void sifreleHarf() {                            // Harf sıralamasını şifrelemek için kullanıcıdan girdi alıp işleyen fonksiyon
   
    char harf;                                  // Kullanıcının girdiği harf
    
    int kaydirma;                               // Kullanıcının girdiği kaydırma miktarı

    printf("Lutfen sifrelemek istediginiz harfi girin: "); // Kullanıcıdan harf girdisi iste
    scanf(" %c", &harf);                        // Kullanıcının girdiği harfi al

    if (isalpha(harf)) {                        // Eğer girilen değer harfse
       
        printf("Lutfen kaydirma miktarini girin: "); // Kaydırma miktarı girdisi iste
       
        scanf("%d", &kaydirma);                 // Kullanıcının girdiği kaydırma miktarını al

        printf("Sifrelenmis hali: %c\n", sifrele(harf, kaydirma)); // Şifrelenmiş harfi yazdır

        printf("\nIngilizce alfabedeki tum harfler:\n"); // Alfabeyi yazdır
       
        char karakter;
       
        for (karakter = 'a'; karakter <= 'z'; karakter++) { // Harfleri yazdır
            printf("%c ", karakter);
        }

        printf("\nHarflerin kaydirilmis hali:\n"); // Kaydırılmış harfleri yazdır
       
        for (karakter = 'a'; karakter <= 'z'; karakter++) {
            printf("%c ", sifrele(karakter, kaydirma)); // Harfleri kaydır ve yazdır
        }
        printf("\n");

        printf("\nDesifrelemek istiyor musunuz? (1: Evet / 0: Hayir): "); // Kullanıcıya deşifreleme isteyip istemediğini sor
      
        int desifreSecim;
       
        scanf("%d", &desifreSecim);
       
        if (desifreSecim == 1) { // Eğer kullanıcı deşifreleme istiyorsa
            printf("Desifrelenmis hali: %c\n", desifrele(sifrele(harf, kaydirma), kaydirma)); // Şifrelenmiş harfi deşifrele ve yazdır
        }
    } else {
        printf("Lutfen bir harf girin.\n");       // Harf dışında bir karakter girildiyse uyarı ver
    }
}

void sifreleKelime() {                           // Kelime sıralamasını şifrelemek için kullanıcıdan girdi alıp işleyen fonksiyon
    
    char kelime[100];                            // Kullanıcının girdiği kelime
    
    int kaydirma;                                // Kullanıcının girdiği kaydırma miktarı

    printf("Kelimeyi giriniz: ");
    
    scanf("%s", kelime);                         // Kullanıcıdan kelime girmesini istiyoruz

    printf("Kaydirma miktarini giriniz: ");
    scanf("%d", &kaydirma);                      // Kullanıcıdan kelime girmesini istiyoruz

    kaydir(kelime, kaydirma);                    // Kelimeyi kaydır
    
    printf("Kaydirilmis hali: %s\n", kelime);    // Kaydırılmış kelimeyi yaz
   
    printf("Orijinal hali: %s\n", kelime);       // Orijinal kelimeyi yazdır

    
    printf("\nDesifrelemek istiyor musunuz? (1: Evet / 0: Hayir): "); // Kullanıcıya deşifreleme isteyip istemediğini sor
    
    int desifreSecim;
    
    scanf("%d", &desifreSecim);
   
    if (desifreSecim == 1) { // Eğer kullanıcı deşifreleme istiyorsa
        kaydir(kelime, -kaydirma);                   // Deşifreleme için kelimeyi ters yönde kaydır
        printf("Desifrelenmis hali: %s\n", kelime);  // Deşifrelenmiş kelimeyi yazdır
    }
}

int main() {
    int secim;                                   // Kullanıcının seçimi

    printf("Seciminizi yapin:\n");                // Kullanıcıya seçenekleri gösteriyoruz
    printf("1. Harf siralamasi\n");
    printf("2. Kelime siralamasi\n");
    scanf("%d", &secim);                         //  burada kullanıcının seçimini almak istiyoruz

    if (secim == 1) {                            // Eğer kullanıcı 1 i secerse
        sifreleHarf();                           // Harf sıralamasını şifrele
    } else if (secim == 2) {                     // Eğer kullanıcı 2 yi secerse
        sifreleKelime();                         // Kelime sıralamasını şifrele
    } else {
        printf("Gecersiz secim!\n");             // Geçersiz bir seçim yapıldıysa uyarı ver
    }

    return 0;                                    // Programı bitir
}



**KODUN CIKTILARI**

![WhatsApp Görsel 2023-12-08 saat 15 23 25_6bea65e5](https://github.com/betulyldrmm/betulyldrmm/assets/153064674/9bde2062-8ed2-4b24-bbe3-e8cb343cbcd0)



![WhatsApp Görsel 2023-12-08 saat 15 23 42_6c94895e](https://github.com/betulyldrmm/betulyldrmm/assets/153064674/8216380f-10a5-4f82-bfdf-efa9066c883d)


