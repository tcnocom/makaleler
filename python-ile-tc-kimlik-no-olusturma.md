+++
title = 'Python İle Tc Kimlik No Olusturma'
date = 2024-04-02T10:08:13+03:00
draft = false
categories = ['Blog', 'Örnek Kodlar']
tags = ['python', 'tc no oluşturma', 'tc kimlik no oluşturma kodu', 'python ile tc oluşturma']
+++

Bu python kodu, Türkiye Cumhuriyeti Kimlik Numarası'nı (TC Kimlik No) oluşturmak için resmi [TC kimlik no üretme algoritmasını](https://tc-no.com/tc-kimlik-numarasi-algoritmasi/) kullanır.

TC Kimlik Numarası oluşturma gereksinimlerini karşılamak için güvenilir ve etkili bir çözüm sunar.

Bu kod sayesinde, web geliştiriciler TC Kimlik Numaralarını hızlı ve doğru bir şekilde üretebilir, veri doğrulama işlemlerinde, test verisi oluşturma gibi aşamalarda ve çeşitli uygulamalarda kullanabilirler.


```python {linenos=true}
import random

def generateTCNumber():
    random_pool1 = random.randint(10000, 99999)
    random_pool2 = random.randint(1000, 9999)

    random_pool1_str = str(random_pool1)
    random_pool2_str = str(random_pool2)

    k1_sum = sum(map(int, random_pool1_str))
    k2_sum = sum(map(int, random_pool2_str))

    tckn = ''
    for i in range(len(random_pool2_str)):
        tckn += random_pool1_str[i] + random_pool2_str[i]

    digit_10 = (k1_sum * 7 - k2_sum) % 10
    digit_11 = (k1_sum + k2_sum + digit_10) % 10

    return tckn + random_pool1_str[-1] + str(digit_10) + str(digit_11)

print(generateTCNumber())

```

