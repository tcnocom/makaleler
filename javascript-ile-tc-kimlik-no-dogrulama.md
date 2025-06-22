# Javascript İle Tc Kimlik No Doğrulama

Bu JavaScript kodu, Türkiye Cumhuriyeti Kimlik Numarası'nı (TC Kimlik No) doğrulamak için resmi [TC kimlik no algoritmasını](https://tc-no.com/tc-kimlik-numarasi-algoritmasi/) kullanır.

TC Kimlik Numarası doğrulama gereksinimlerini karşılamak için güvenilir ve etkili bir çözüm sunar.

Bu kod sayesinde, web geliştiriciler TC Kimlik Numaralarının geçerliliğini hızlı ve doğru bir şekilde kontrol edebilir, veri doğrulama işlemlerinde ve çeşitli uygulamalarda kullanabilirler.

```javascript {linenos=true}
function validateTCNumber(tckn) {
    // TC Kimlik numarası 11 haneli olmalıdır
    if (tckn.length !== 11) {
        return false;
    }
    
    // TC Kimlik numarası sadece rakamlardan oluşmalıdır
    if (!/^[0-9]+$/.test(tckn)) {
        return false;
    }
    
    // İlk hane 0 olamaz
    if (tckn[0] === '0') {
        return false;
    }
    
    const digits = Array.from(tckn).map(Number);
    
    // 10. hane kontrolü
    const digit10 = ((digits.slice(0, 9).filter((_, i) => i % 2 === 0).reduce((a, b) => a + b, 0) * 7) - 
                     digits.slice(0, 8).filter((_, i) => i % 2 === 1).reduce((a, b) => a + b, 0)) % 10;
    if (digit10 !== digits[9]) {
        return false;
    }
    
    // 11. hane kontrolü
    const digit11 = digits.slice(0, 10).reduce((a, b) => a + b, 0) % 10;
    if (digit11 !== digits[10]) {
        return false;
    }
    
    return true;
}

// Test örnekleri
const testNumbers = [
    "10000000146",  // Geçerli
    "12345678901",  // Geçersiz
    "1234",         // Geçersiz (11 haneli değil)
    "0234567890A"   // Geçersiz (rakam değil)
];

testNumbers.forEach(tckn => {
    const result = validateTCNumber(tckn);
    console.log(`${tckn}: ${result ? "Geçerli" : "Geçersiz"}`);
});
```

Bu JavaScript fonksiyonu aşağıdaki kontrolleri yapar:

1. TC Kimlik numarasının 11 haneli olup olmadığını kontrol eder
2. Tüm karakterlerin rakam olup olmadığını kontrol eder
3. İlk hanenin 0 olmadığını kontrol eder
4. 10. ve 11. hanelerin doğrulama algoritmasına uygunluğunu kontrol eder

Fonksiyon, verilen TC Kimlik numarası geçerliyse `true`, değilse `false`