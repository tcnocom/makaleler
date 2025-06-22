+++
title = 'Javascript İle Tc Kimlik No Olusturma'
date = 2024-04-02T10:00:05+03:00
draft = false
categories = ['Blog', 'Örnek Kodlar']
tags = ['javascript', 'js', 'tc no oluşturma', 'tc kimlik no oluşturma kodu', 'js ile tc oluşturma', 'javascript ile tc oluşturma']
+++

Bu Javascript kodu, Türkiye Cumhuriyeti Kimlik Numarası'nı (TC Kimlik No) oluşturmak için resmi [TC kimlik no üretme algoritmasını](https://tc-no.com/tc-kimlik-numarasi-algoritmasi/) kullanır.

TC Kimlik Numarası oluşturma gereksinimlerini karşılamak için güvenilir ve etkili bir çözüm sunar.

Bu kod sayesinde, web geliştiriciler TC Kimlik Numaralarını hızlı ve doğru bir şekilde üretebilir, veri doğrulama işlemlerinde, test verisi oluşturma gibi aşamalarda ve çeşitli uygulamalarda kullanabilirler.

```javascript {linenos=true}
function generateTCNumber() {
  var random_pool1 = Math.floor(Math.random() * (99999 - 10000 + 1)) + 10000;
  var random_pool2 = Math.floor(Math.random() * (9999 - 1000 + 1)) + 1000;

  var random_pool1_str = random_pool1.toString().split('');
  var random_pool2_str = random_pool2.toString().split('');

  var k1_sum = random_pool1_str.reduce((total, num) => total + parseInt(num), 0);
  var k2_sum = random_pool2_str.reduce((total, num) => total + parseInt(num), 0);

  var tckn = '';
  for (var i = 0; i < random_pool2_str.length; i++) {
      tckn += random_pool1_str[i] + random_pool2_str[i];
  }

  var digit_10 = (k1_sum * 7 - k2_sum) % 10;
  var digit_11 = (k1_sum + k2_sum + digit_10) % 10;

  return tckn + random_pool1_str[random_pool1_str.length - 1] + digit_10 + digit_11;
}

```

