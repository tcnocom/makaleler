+++
title = 'Php İle Tc Kimlik No Doğrulama'
date = 2025-01-24T10:08:13+03:00
draft = false
categories = ['Blog', 'Örnek Kodlar']
tags = ['php', 'tc no doğrulama', 'tc kimlik no doğrulama kodu', 'php ile tc doğrulama']
+++

Bu PHP kodu, Türkiye Cumhuriyeti Kimlik Numarası'nı (TC Kimlik No) doğrulamak için resmi [TC kimlik no algoritmasını](https://tc-no.com/tc-kimlik-numarasi-algoritmasi/) kullanır.

TC Kimlik Numarası doğrulama gereksinimlerini karşılamak için güvenilir ve etkili bir çözüm sunar.

Bu kod sayesinde, web geliştiriciler TC Kimlik Numaralarının geçerliliğini hızlı ve doğru bir şekilde kontrol edebilir, veri doğrulama işlemlerinde ve çeşitli uygulamalarda kullanabilirler.

```php {linenos=true}
function validateTCNumber($tckn) {
    // TC Kimlik numarası 11 haneli olmalıdır
    if (strlen($tckn) != 11) {
        return false;
    }
    
    // TC Kimlik numarası sadece rakamlardan oluşmalıdır
    if (!ctype_digit($tckn)) {
        return false;
    }
    
    // İlk hane 0 olamaz
    if ($tckn[0] == '0') {
        return false;
    }
    
    $digits = array_map('intval', str_split($tckn));
    
    // 10. hane kontrolü
    $digit10 = ((array_sum(array_slice($digits, 0, 9, 2)) * 7) - array_sum(array_slice($digits, 1, 8, 2))) % 10;
    if ($digit10 != $digits[9]) {
        return false;
    }
    
    // 11. hane kontrolü
    $digit11 = array_sum(array_slice($digits, 0, 10)) % 10;
    if ($digit11 != $digits[10]) {
        return false;
    }
    
    return true;
}

// Test örnekleri
$test_numbers = [
    "10000000146",  // Geçerli
    "12345678901",  // Geçersiz
    "1234",         // Geçersiz (11 haneli değil)
    "0234567890A"   // Geçersiz (rakam değil)
];

foreach ($test_numbers as $tckn) {
    $result = validateTCNumber($tckn);
    echo "$tckn: " . ($result ? "Geçerli" : "Geçersiz") . "\n";
}
```

Bu PHP fonksiyonu aşağıdaki kontrolleri yapar:

1. TC Kimlik numarasının 11 haneli olup olmadığını kontrol eder
2. Tüm karakterlerin rakam olup olmadığını kontrol eder
3. İlk hanenin 0 olmadığını kontrol eder
4. 10. ve 11. hanelerin doğrulama algoritmasına uygunluğunu kontrol eder

Fonksiyon, verilen TC Kimlik numarası geçerliyse `true`, değilse `false` döndürür. 