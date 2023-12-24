#include <stdio.h>
#include <string.h>

// Teklif struct'ı tanımlama
struct Teklif {
    float miktar;
};

int main() {
    int teklifSayisi,i;

    printf("Kac kisi teklif verecek: ");
    scanf("%d", &teklifSayisi);

    if (teklifSayisi <= 0) {
        printf("Gecersiz girdi. En az 1 teklif veren olmalidir.\n");
        return 1; // Hata durumu
    }

    // Teklif bilgilerini tutacak olan struct dizisi
    struct Teklif teklifler[teklifSayisi];

    // Teklifleri alma
    for (i = 0; i < teklifSayisi; i++) {
        printf("%d. kisinin teklifi:\n", i + 1);
        printf("Teklif Miktari: ");
        scanf("%f", &teklifler[i].miktar);
    }

    // En yüksek teklifi
    float maxTeklif = 0;

    for (i = 0; i < teklifSayisi; i++) {
        if (teklifler[i].miktar > maxTeklif) {
            maxTeklif = teklifler[i].miktar;
            
        }
    }

    // Kazananı yazdırma
    printf("En yuksek teklif: %.2f TL\n", maxTeklif);
    

    return 0;
}
