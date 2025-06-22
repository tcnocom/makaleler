# Java İle Tc Kimlik No Olusturma

Bu JAVA kodu, Türkiye Cumhuriyeti Kimlik Numarası'nı (TC Kimlik No) oluşturmak için resmi [TC kimlik no üretme algoritmasını](https://tc-no.com/tc-kimlik-numarasi-algoritmasi/) kullanır.

TC Kimlik Numarası oluşturma gereksinimlerini karşılamak için güvenilir ve etkili bir çözüm sunar.

Bu kod sayesinde, web geliştiriciler TC Kimlik Numaralarını hızlı ve doğru bir şekilde üretebilir, veri doğrulama işlemlerinde, test verisi oluşturma gibi aşamalarda ve çeşitli uygulamalarda kullanabilirler.

```java {linenos=true}
import java.util.Random;

public class Main {

    public static String generateTCNumber() {
        Random rand = new Random();

        int random_pool1 = rand.nextInt(99999 - 10000 + 1) + 10000;
        int random_pool2 = rand.nextInt(9999 - 1000 + 1) + 1000;

        String random_pool1_str = String.valueOf(random_pool1);
        String random_pool2_str = String.valueOf(random_pool2);

        int k1_sum = 0;
        for (char c : random_pool1_str.toCharArray()) {
            k1_sum += Character.getNumericValue(c);
        }

        int k2_sum = 0;
        for (char c : random_pool2_str.toCharArray()) {
            k2_sum += Character.getNumericValue(c);
        }

        StringBuilder tckn = new StringBuilder();
        for (int i = 0; i < random_pool2_str.length(); i++) {
            tckn.append(random_pool1_str.charAt(i)).append(random_pool2_str.charAt(i));
        }

        int digit_10 = (k1_sum * 7 - k2_sum) % 10;
        int digit_11 = (k1_sum + k2_sum + digit_10) % 10;

        return tckn.toString() + random_pool1_str.charAt(random_pool1_str.length() - 1) + digit_10 + digit_11;
    }

    public static void main(String[] args) {
        System.out.println(generateTCNumber());
    }
}


```

Bu Java kodu, *java.util.Random* sınıfını kullanarak rastgele sayılar oluşturur. Döngüler ve dizi işlemleriyle string işlemleri gerçekleştirir.
