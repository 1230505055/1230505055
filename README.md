#include <stdio.h>

// Fonksiyon prototipleri
void sifrele(char *dosyaAdi, char *sifre);
void coz(char *dosyaAdi, char *sifre);

int main() {
    char dosyaAdi[] = "input 1.txt";
    char sifre[] = "sifre123";

    // Dosyayı şifrele
    sifrele(dosyaAdi, sifre);

    // Şifreli dosyayı çöz
    coz(dosyaAdi, sifre);

    return 0;
}

// Dosyayı şifreleme fonksiyonu
void sifrele(char *dosyaAdi, char *sifre) {
    FILE *dosya = fopen(dosyaAdi, "r");
    FILE *sifreliDosya = fopen("sifreliDosya.txt", "w");

    if (dosya == NULL || sifreliDosya == NULL) {
        printf("Dosya acilamadi!");
        return;
    }

    int karakter;
    int sifreUzunluk = strlen(sifre);
    int i = 0;

    while ((karakter = fgetc(dosya)) != EOF) {
        fputc(karakter ^ sifre[i % sifreUzunluk], sifreliDosya);
        i++;
    }

    fclose(dosya);
    fclose(sifreliDosya);

    printf("Dosya sifrelenmis ve 'sifreliDosya.txt' olarak kaydedilmistir.\n");
}

 // Şifreli dosyayı çözme fonksiyonu
void coz(char *dosyaAdi, char *sifre) {
    FILE *sifreliDosya = fopen("sifreliDosya.txt", "r");
    FILE *cozulmusDosya = fopen("cozulmusDosya.txt", "w");

    if (sifreliDosya == NULL || cozulmusDosya == NULL) {
        printf("Dosya acilamadi!");
        return;
    }

    int karakter;
    int sifreUzunluk = strlen(sifre);
    int i = 0;

    while ((karakter = fgetc(sifreliDosya)) != EOF) {
        fputc(karakter ^ sifre[i % sifreUzunluk], cozulmusDosya);
        i++;
    }

    fclose(sifreliDosya);
    fclose(cozulmusDosya);

    printf("Sifreli dosya cozulmus ve 'cozulmusDosya.txt' olarak kaydedilmistir.\n");
}
