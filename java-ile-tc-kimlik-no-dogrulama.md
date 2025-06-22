# Java İle Tc Kimlik No Doğrulama

Bu Java kodu, Türkiye Cumhuriyeti Kimlik Numarası'nı (TC Kimlik No) doğrulamak için resmi [TC kimlik no algoritmasını](https://tc-no.com/tc-kimlik-numarasi-algoritmasi/) kullanır.

TC Kimlik Numarası doğrulama gereksinimlerini karşılamak için güvenilir ve etkili bir çözüm sunar.

Bu kod sayesinde, Java geliştiricileri TC Kimlik Numaralarının geçerliliğini hızlı ve doğru bir şekilde kontrol edebilir, veri doğrulama işlemlerinde ve çeşitli uygulamalarda kullanabilirler.

```java {linenos=true}
public class TCKimlikNoValidator {
    public static boolean validateTCNumber(String tckn) {
        // TC Kimlik numarası 11 haneli olmalıdır
        if (tckn.length() != 11) {
            return false;
        }
        
        // TC Kimlik numarası sadece rakamlardan oluşmalıdır
        if (!tckn.matches("^[0-9]+$")) {
            return false;
        }
        
        // İlk hane 0 olamaz
        if (tckn.charAt(0) == '0') {
            return false;
        }
        
        int[] digits = new int[11];
        for (int i = 0; i < 11; i++) {
            digits[i] = Character.getNumericValue(tckn.charAt(i));
        }
        
        // 10. hane kontrolü
        int sumEven = 0;
        int sumOdd = 0;
        
        for (int i = 0; i < 9; i++) {
            if (i % 2 == 0) {
                sumEven += digits[i];
            } else {
                sumOdd += digits[i];
            }
        }
        
        int digit10 = ((sumEven * 7) - sumOdd) % 10;
        if (digit10 != digits[9]) {
            return false;
        }
        
        // 11. hane kontrolü
        int sum = 0;
        for (int i = 0; i < 10; i++) {
            sum += digits[i];
        }
        
        int digit11 = sum % 10;
        if (digit11 != digits[10]) {
            return false;
        }
        
        return true;
    }

    public static void main(String[] args) {
        // Test örnekleri
        String[] testNumbers = {
            "10000000146",  // Geçerli
            "12345678901",  // Geçersiz
            "1234",         // Geçerli (11 haneli değil)
            "0234567890A"   // Geçersiz (rakam değil)
        };

        for (String tckn : testNumbers) {
            boolean result = validateTCNumber(tckn);
            System.out.println(tckn + ": " + (result ? "Geçerli" : "Geçersiz"));
        }
    }
}
```

Bu Java sınıfı aşağıdaki kontrolleri yapar:

1. TC Kimlik numarasının 11 haneli olup olmadığını kontrol eder
2. Tüm karakterlerin rakam olup olmadığını kontrol eder
3. İlk hanenin 0 olmadığını kontrol eder
4. 10. ve 11. hanelerin doğrulama algoritmasına uygunluğunu kontrol eder

Fonksiyon, verilen TC Kimlik numarası geçerliyse `true`, değilse `false` döndürür. 