# Inline Namespace

- Inline isim alanları (Inline namespace) C++11 standartları ile dile eklenmiş bir özellik. Bir isim alanı inline anahtar sözcüğü ile bildirildiğinde bu isim alanı içindeki isimler onu içine alan isim alanı içinde doğrudna görülür hale geliyor.

```CPP
inline namespace Neco {
	int x = 10;
}
```

- Bunun gibi bir isim alanı kullanımının:

```CPP
namespace Neco {
    int x = 10;
    //...
}
using namespace Neco;
```
- Bunun gibi bir koda karşılık geldiğini düşünebiliriz. Şimdi de aşağıdaki koda bakalım.

