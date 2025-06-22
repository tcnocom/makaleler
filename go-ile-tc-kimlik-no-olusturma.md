# Go İle Tc Kimlik No Olusturma

Bu go (golang) kodu, Türkiye Cumhuriyeti Kimlik Numarası'nı (TC Kimlik No) oluşturmak için resmi [TC kimlik no üretme algoritmasını](https://tc-no.com/tc-kimlik-numarasi-algoritmasi/) kullanır.

TC Kimlik Numarası oluşturma gereksinimlerini karşılamak için güvenilir ve etkili bir çözüm sunar.

Bu kod sayesinde, web geliştiriciler TC Kimlik Numaralarını hızlı ve doğru bir şekilde üretebilir, veri doğrulama işlemlerinde, test verisi oluşturma gibi aşamalarda ve çeşitli uygulamalarda kullanabilirler.


```go {linenos=true}
package main

import (
	"fmt"
	"math/rand"
	"time"
)

func generateTCNumber() string {
	rand.Seed(time.Now().UnixNano())

	random_pool1 := rand.Intn(99999-10000+1) + 10000
	random_pool2 := rand.Intn(9999-1000+1) + 1000

	random_pool1_str := []rune(fmt.Sprintf("%d", random_pool1))
	random_pool2_str := []rune(fmt.Sprintf("%d", random_pool2))

	k1_sum := 0
	for _, digit := range random_pool1_str {
		k1_sum += int(digit - '0')
	}

	k2_sum := 0
	for _, digit := range random_pool2_str {
		k2_sum += int(digit - '0')
	}

	tckn := ""
	for i := 0; i < len(random_pool2_str); i++ {
		tckn += string(random_pool1_str[i]) + string(random_pool2_str[i])
	}

	digit_10 := (k1_sum*7 - k2_sum) % 10
	digit_11 := (k1_sum + k2_sum + digit_10) % 10

	return tckn + string(random_pool1_str[len(random_pool1_str)-1]) + fmt.Sprintf("%d", digit_10) + fmt.Sprintf("%d", digit_11)
}

func main() {
	fmt.Println(generateTCNumber())
}


```

Bu Go kodu, math/rand ve time paketlerini kullanarak rastgele sayılar oluşturur. Ayrıca, string dönüşümleri için fmt.Sprintf ve döngüler kullanır.
