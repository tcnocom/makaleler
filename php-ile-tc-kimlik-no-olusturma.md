# Php İle Tc Kimlik No Olusturma

Bu PHP kodu, Türkiye Cumhuriyeti Kimlik Numarası'nı (TC Kimlik No) oluşturmak için resmi [TC kimlik no üretme algoritmasını](https://tc-no.com/tc-kimlik-numarasi-algoritmasi/) kullanır.

TC Kimlik Numarası oluşturma gereksinimlerini karşılamak için güvenilir ve etkili bir çözüm sunar.

Bu kod sayesinde, web geliştiriciler TC Kimlik Numaralarını hızlı ve doğru bir şekilde üretebilir, veri doğrulama işlemlerinde, test verisi oluşturma gibi aşamalarda ve çeşitli uygulamalarda kullanabilirler.

```php {linenos=true}
function generateTCNumber() {
    $random_pool1 = mt_rand(10000, 99999);
    $random_pool2 = mt_rand(1000, 9999);

    $random_pool1_str = str_split(strval($random_pool1));
    $random_pool2_str = str_split(strval($random_pool2));

    $k1_sum = array_sum($random_pool1_str);
    $k2_sum = array_sum($random_pool2_str);

    $tckn = '';

    for ($i = 0; $i < count($random_pool2_str); $i++) {
        $tckn .= $random_pool1_str[$i] . $random_pool2_str[$i];
    }

    $digit_10 = ($k1_sum * 7 - $k2_sum) % 10;
    $digit_11 = ($k1_sum + $k2_sum + $digit_10) % 10;

    return $tckn . $random_pool1_str[count($random_pool1_str) - 1] . $digit_10 . $digit_11;
}


```

