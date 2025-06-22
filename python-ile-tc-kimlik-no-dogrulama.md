+++
title = 'Python İle Tc Kimlik No Doğrulama'
date = 2025-01-24T10:08:13+03:00
draft = false
categories = ['Blog', 'Örnek Kodlar']
tags = ['python', 'tc no doğrulama', 'tc kimlik no doğrulama kodu', 'python ile tc doğrulama']
+++

Bu python kodu, Türkiye Cumhuriyeti Kimlik Numarası'nı (TC Kimlik No) doğrulamak için resmi [TC kimlik no algoritmasını](https://tc-no.com/tc-kimlik-numarasi-algoritmasi/) kullanır.

TC Kimlik Numarası doğrulama gereksinimlerini karşılamak için güvenilir ve etkili bir çözüm sunar.

Bu kod sayesinde, web geliştiriciler TC Kimlik Numaralarının geçerliliğini hızlı ve doğru bir şekilde kontrol edebilir, veri doğrulama işlemlerinde ve çeşitli uygulamalarda kullanabilirler.

```python {linenos=true}
def validateTCNumber(tckn):
    # TC Kimlik numarası 11 haneli olmalıdır
    if not len(tckn) == 11:
        return False
    
    # TC Kimlik numarası sadece rakamlardan oluşmalıdır
    if not tckn.isdigit():
        return False
    
    # İlk hane 0 olamaz
    if tckn[0] == '0':
        return False
    
    digits = [int(d) for d in tckn]
    
    # 10. hane kontrolü
    digit10 = ((sum(digits[0:9:2]) * 7) - sum(digits[1:8:2])) % 10
    if digit10 != digits[9]:
        return False
    
    # 11. hane kontrolü
    digit11 = (sum(digits[:10])) % 10
    if digit11 != digits[10]:
        return False
    
    return True

# Test örnekleri
test_numbers = [
    "10000000146",  # Geçerli
    "12345678901",  # Geçersiz
    "1234",         # Geçersiz (11 haneli değil)
    "0234567890A"   # Geçersiz (rakam değil)
]

for tckn in test_numbers:
    result = validateTCNumber(tckn)
    print(f"{tckn}: {'Geçerli' if result else 'Geçersiz'}")
```

Bu Python fonksiyonu aşağıdaki kontrolleri yapar:

1. TC Kimlik numarasının 11 haneli olup olmadığını kontrol eder
2. Tüm karakterlerin rakam olup olmadığını kontrol eder
3. İlk hanenin 0 olmadığını kontrol eder
4. 10. ve 11. hanelerin doğrulama algoritmasına uygunluğunu kontrol eder

Fonksiyon, verilen TC Kimlik numarası geçerliyse `True`, değilse `False` döndürür. 