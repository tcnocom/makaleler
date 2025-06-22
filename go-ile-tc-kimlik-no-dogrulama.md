# Go İle Tc Kimlik No Doğrulama

Bu Go kodu, Türkiye Cumhuriyeti Kimlik Numarası'nı (TC Kimlik No) doğrulamak için resmi [TC kimlik no algoritmasını](https://tc-no.com/tc-kimlik-numarasi-algoritmasi/) kullanır.

TC Kimlik Numarası doğrulama gereksinimlerini karşılamak için güvenilir ve etkili bir çözüm sunar.

Bu kod sayesinde, Go geliştiricileri TC Kimlik Numaralarının geçerliliğini hızlı ve doğru bir şekilde kontrol edebilir, veri doğrulama işlemlerinde ve çeşitli uygulamalarda kullanabilirler.

```go {linenos=true}
package main

import (
    "fmt"
    "regexp"
    "strconv"
)

func validateTCNumber(tckn string) bool {
    // TC Kimlik numarası 11 haneli olmalıdır
    if len(tckn) != 11 {
        return false
    }
    
    // TC Kimlik numarası sadece rakamlardan oluşmalıdır
    matched, _ := regexp.MatchString("^[0-9]+$", tckn)
    if !matched {
        return false
    }
    
    // İlk hane 0 olamaz
    if tckn[0] == '0' {
        return false
    }
    
    digits := make([]int, 11)
    for i := 0; i < 11; i++ {
        digits[i], _ = strconv.Atoi(string(tckn[i]))
    }
    
    // 10. hane kontrolü
    sumEven := 0
    sumOdd := 0
    
    for i := 0; i < 9; i++ {
        if i%2 == 0 {
            sumEven += digits[i]
        } else {
            sumOdd += digits[i]
        }
    }
    
    digit10 := ((sumEven * 7) - sumOdd) % 10
    if digit10 != digits[9] {
        return false
    }
    
    // 11. hane kontrolü
    sum := 0
    for i := 0; i < 10; i++ {
        sum += digits[i]
    }
    
    digit11 := sum % 10
    if digit11 != digits[10] {
        return false
    }
    
    return true
}

func main() {
    // Test örnekleri
    testNumbers := []string{
        "10000000146",  // Geçerli
        "12345678901",  // Geçersiz
        "1234",         // Geçersiz (11 haneli değil)
        "0234567890A",  // Geçersiz (rakam değil)
    }

    for _, tckn := range testNumbers {
        result := validateTCNumber(tckn)
        if result {
            fmt.Printf("%s: Geçerli\n", tckn)
        } else {
            fmt.Printf("%s: Geçersiz\n", tckn)
        }
    }
}
```

Bu Go fonksiyonu aşağıdaki kontrolleri yapar:

1. TC Kimlik numarasının 11 haneli olup olmadığını kontrol eder
2. Tüm karakterlerin rakam olup olmadığını kontrol eder
3. İlk hanenin 0 olmadığını kontrol eder
4. 10. ve 11. hanelerin doğrulama algoritmasına uygunluğunu kontrol eder

Fonksiyon, verilen TC Kimlik numarası geçerliyse `true`, değilse `false` döndürür. 