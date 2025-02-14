import java.util.Arrays;
import java.util.Scanner;

public class TransportRoutePlanner {
    public static void main(String[] args) {
        // Kullanıcıdan kriter ağırlıklarını al
        Scanner input = new Scanner(System.in);
        double[] weights = new double[5];
        String[] criteriaNames = {"Nüfus Yoğunluğu", "Ulaşım Altyapısı", "Maliyet", "Çevresel Etki", "Sosyal Fayda"};
        String[] neighborhoodNames = {"Cumhuriyet Mahallesi", "Kofçaz Mahallesi", "İstasyon Mahallesi"};  // Mahalle isimlerini güncelledik

        System.out.println("Kriter ağırlıklarını giriniz (Toplamı 100 olmalı):");
        for (int i = 0; i < weights.length; i++) {
            System.out.print(criteriaNames[i] + ": ");
            weights[i] = input.nextDouble();
        }

        // Ağırlıkları normalize et (toplamı 100 olacak şekilde her ağırlığı 100'e böl)
        double totalWeight = Arrays.stream(weights).sum();
        if (Math.abs(totalWeight - 100.0) > 1e-6) {
            System.out.println("Hata: Kriter ağırlıklarının toplamı 100 olmalıdır!");
            return;
        }

        // Ağırlıkları 100'e bölüp normalize et
        for (int i = 0; i < weights.length; i++) {
            weights[i] /= 100.0;
        }

        // 3 mahalle için sentetik veriler (nüfus yoğunluğu, ulaşım altyapısı, maliyet, çevresel etki, sosyal fayda)
        double[][] criteria = {
                {15, 7, 50, 8, 9},   // Cumhuriyet
                {12, 5, 40, 7, 8.5}, // Kofçaz
                {18, 9, 60, 6, 9.5}  // İstasyon
        };

        // Her mahalle için skorları hesapla
        double[] scores = new double[criteria.length];
        for (int i = 0; i < criteria.length; i++) {
            scores[i] = 0;
            for (int j = 0; j < criteria[i].length; j++) {
                scores[i] += criteria[i][j] * weights[j];
            }
        }

        // Softmax ile ağırlıkları hesapla
        double[] probabilities = softmax(scores);

        // En uygun mahalleyi seçme
        int bestNeighborhood = getBestRoute(probabilities);

        // Sonuçları yazdırma
        System.out.print("Kriter ağırlıkları: ");
        for (int i = 0; i < probabilities.length; i++) {
            System.out.printf("%s: %.4f ", neighborhoodNames[i], probabilities[i]);
        }
        System.out.println();
        System.out.println("En uygun güzergah " + neighborhoodNames[bestNeighborhood]);
    }

    // Softmax fonksiyonu
    public static double[] softmax(double[] scores) {
        double sumExp = 0.0;
        double[] probabilities = new double[scores.length];

        // Skorları normalize et (Numerik kararlılık için en büyük skoru çıkar)
        double maxScore = Arrays.stream(scores).max().getAsDouble();
        for (int i = 0; i < scores.length; i++) {
            scores[i] -= maxScore;
        }

        // Softmax paydası için exp değerlerini hesapla
        for (double score : scores) {
            sumExp += Math.exp(score);
        }

        // Softmax sonucu
        for (int i = 0; i < scores.length; i++) {
            probabilities[i] = (Math.exp(scores[i]) / sumExp) + 1e-10;
        }

        // Normalize et (toplamı 1 yap)
        double total = Arrays.stream(probabilities).sum();
        for (int i = 0; i < probabilities.length; i++) {
            probabilities[i] /= total;
        }

        return probabilities;
    }

    // En yüksek ağırlığa sahip güzergahı seçme
    public static int getBestRoute(double[] weights) {
        int bestIndex = 0;
        double maxWeight = weights[0];

        for (int i = 1; i < weights.length; i++) {
            if (weights[i] > maxWeight) {
                maxWeight = weights[i];
                bestIndex = i;
            }
        }
        return bestIndex;
    }
}
