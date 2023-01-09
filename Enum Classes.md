Necati Ergin'in notlarından alıntıdır. http://plepa.com/2016/11/18/numaralandirma-siniflari-enum-classes/

# Numaralandırma Sınıfları (Enum Classes)

- C++ 11 ile gelen araçlardan biri de numaralandırma sınıfları. Standartların kulnnaıdığı resmi terim "strongly typed enums". "Güçlü tür özelliği kazandırılmış numaralandırma türleri" olarak türkçeye çevirilebilir.

- Numaralandırma türlerinin dile eklenmesiyle birlikte artık C++ da iki ayrı numaralandırma aracı var. Numaralandırma türlerinin dile neden eklendiğini anlayabilmek için, eski numaralandırma türlerinin C++11 öncesinde yol açtığı tipik sorunları anlayabilmemiz gerekiyor:

## Numaralandırma sabitlerinin bilinirlik alanları

- Düz numaralandırma türlerinde, tanıtılan numaralandırma sabitlerinin bilinirlik alanı numaralandırma türünün bilinirlik alanıdır. Bu durum numaralandırma sabitleri olan isimlerin aynı bilinirlik alanında bulunan diğer isimlerle çakışma riskini arttırır. Çok sayıda kütüphane kullanılan projerlerde numaralandırma sabitleri olarak kullanılan isimlerin çakışması çok sık karşılaşılan bir durumdur.

```CPP
//traffic.h
enum TrafficLight {Yellow, Green, Red};

//screen.h
enum ScreenColor { White, Gray, Green, Red, Magenta, Brown, Black };

//simulation.cpp
//	#include "traffic.h"
//	#include "screen.h"
```
> Yukarıdaki kodda traffic.h başlık dosyasında tanıtılan enumTrafficLight isimli bir tür var. Bu başlık dosyası ile doğrudan bir ilişkisi olmayan screen.h isimli başlık dosyası ise enum ScrenColor isimli bir türü tanıtmış. Simulation.cpp isimli kod dosyası her iki modülün sağladığı hizmetlerden faydalanabilmek için iki başlık dosyasını da include ederek kendi kaynak dosyasına eklemiş.

> Bu durumu derleyici sentaks hatası olarak işaretleyecek. Green ve Red isimleri çakışıyor. Numaralandırma sınıflarının sağladığı faydalardan ilki burada. Numaralandırma sınıfg türlerinin kendi bilinirlik alanları var ve tanıtılan numaralandırma sabitleri, numaralandırma sınıfının kendi bilinirlik alanında yer alıyor.

- Yukarıdaki kodda şimdi numaralandırma sınıflarını kullanıyoruz:

```CPP
//traffic.h
enum class TrafficLight {Yellow, Green, Red};

//screen.h
enum class ScreenColor { White, Gray, Green, Red, Magenta, Brown, Black };

//simulation.cpp
//	#include "traffic.h"
//	#include "screen.h"

void func()
{
	auto traffic_light = TrafficLight::Green;
	auto screen_color= ScreenColor::Green;
}
```

> Numaralandırma sınıflarına ilişkin sabit isimleri numaralandırma sınıf ismiyle nitelenmek zorunda. Aşağıdaki kullanım geçerli değildir:

```CPP
ScreenColor scr_color = Magenta; //geçersiz
```

- Düz numaralandırma türleri ile tanıtılan numaralandırma sabitlerinin bir bilinirlik alanı olmamasına karşın C++11 artık onları da numaralandırma tür ismiyle niteleyerek kullanabiliyoruz:

```CPP
enum Suit {Club, diamond, Hearth, Spade};

Suit s = Suit::diamond;
```
> C++11 öncesi numaralandırma sabitlerinin isim çakışmalarından korunması için bir yapı ile sarmalanması sık başvurulan bir yöntemdi:

```CPP
struct SuitWrapper {
	enum Suit {Club, Diamond, Heart, Spade};
};

SuitWrapper::Suit s = SuitWrapper::Diamond;
```

> Böyle bir sarmalamanın görece bir avantajı, sarmalayan sınıftan türetme yapılabilmesi. Ancak numaralandırma sınıflarından türetme yapılması olanağı yok. İsim çakışmasından korunmak için kullanılan başka bir yöntem de numaralandırma türünün tanımını bir isim alanı içine almaktı.

```CPP
namespace Neco {
	enum suit { Club, Diamond, Heart, Spade };
}

Neco::suit s = Neco::Diamond;
```

## Düz Numaralandırma Türlerine İlişkin Sorunlu Tür dönüşümleri

- Düz numaralandırma türlerine yalnızca aynı türden değerler atanabilir, yani **diğer türlerden düz numaralandırma türlerine  otomatik (implicit) Tür dönüşümü yoktur**:

```CPP
enum Color {White, Yellow, Gray, Green, Brown, Black};
enum Font { Arial, Verdana, TimesNewRoman, Courier, Helvetica };

int main()
{
	Color c1 = Yellow;	// Geçerli
	Color c2 = 3;		// Geçersiz
	Font f1 = Verdana;	// Geçerli
	Font f2 = Black;	// Geçersiz
	c1 = f1;			// Geçersiz
}
```

> Numaralandırma türlerine diğer türlerden otomatik tür dönüşümü olmaması yanlış yazımlara karşı önemli bir koruma sağlar. Eğer, küçük bir olasılıkla da olsa, geçersiz olan ilk değer verme veya atama işlemleri istenerek yapılıyorsa **static_cast** tür dönüştürme işleci kullanılabilir:

```CPP
enum Color {White, Yellow, Gray, Green, Brown, Black};
enum Font { Arial, Verdana, TimesNewRoman, Courier, Helvetica };

int main()
{
	Color c1 = Yellow;	
	Color c2 = static_cast<Color>(3);
	Font f1 = Verdana;	
	Font f2 = static_cast<Font>(Black);
	c1 = static_cast<Color>(f1);		
}
```

- Ancak, düz sayı numaralandırma türlerinden tamsayı ve gerçek sayı türlerine implicit tür dönüşümü var. Aşağıdaki koda bakalım:

```CPP
enum Color {White, Yellow, Gray, Green, Brown, Black};

int main()
{
	Color c = Green;
	int cnt = 0;

	int ival = c;
}
```
> Burada **int** türden **ival** değişkenine **Color** türden **c** değişkeninin değeriyle ilk değer verilmiş. Dilin kurallarıona göre kod geçerli. Color türünden c derleyici tarafından int türden 3 değerine dönüştürülecek.

> Numaralandırma sınıflarında artık diğer türlere otomatik tür dönüşümü geçerli değil:

```CPP
enum class Color { White, Yellow, Gray, Green, Brown, Black };

int main()
{
	Color c = Color::Green;
	int cnt = 0;

	//int i = c; // geçersiz

	int j = static_cast<int>(c); // Geçerli
}
```
> Bu kodda i değişkenine verilen ilk değer geçerli değil. Çünkü color türünden int türüne otomatik tür dönüşümü yok. Ancak j değişkenine ilk değer verilirken Color türünden değer **static_cast** işleciyle int türüne dönüştürülüyor. Kod geçerli. 

## Numaralandırma Türlerinin Baz Türleri

- Hem C hem C++ dillerinden numaralandırma türleri için derleyici arka planda bir tamsayı türü kullanır. Bu tam sayı türüne **underlying type** deniyor. Biz bu anlamda **Baz Tür** terimini kullanacağız. C dilinde numaralandırma türlerinin baz türü her zaman int türüdür. Yani bir C kodunda **enum Data** bir tür olmak üzere,

```CPP
assert(sizeof(enum Data) == sizeof(int));
```

- ifadesi her zaman doğrulanır.

### C++11 standartları ile gelen diğer gelişmeler:

- **Hem düz numaralandırma türleri hem de numaralandırma sınıfları için bildirimde ya da tanımda baz tür belirlenebiliyor.**

**Örnek:**

```CPP
enum Suit : unsigned char {Club, Diamond, Heart, Spade};

enum class BufferSize : unsigned int {
	SmallSize	= 10000u,
	DefaultSize	= 100000u,
	LargeSize	= 1000000u
};

enum Color : unsigned char;

enum Font;	// Geçersiz

enum class ErrorCode;

enum class ImageWidth : unsigned long;
```

> Burada tanımlanan düz **enum Suit** türünün baz türü olarak **unsigned char** türü seçilmiş. Baz türün **enum** etiketi olarak seçilen isimden sonra gelen **:** atomunu izlediğini görüyorsunuz.

> Numaralandırma sınıfı olarak tanımlanan **BufferSize** türünde ise baz tür olarak unsigned int seçilmiş.

> Düz numaralandırma türü olan **Font** yalnızca bildirilmiş ancak tanımlanmamış. Bildirimde baz türü belirtilmediği için bildirim geçersiz.

> Numaralandırma sınıfı olarak bildirilen **ErrorCode** türünde baz türü belirtilmemiş. Baz tür varsayılan biçimde int türü olarak kabul edilecek.

> Numaralandırma sınıfı olarak bildirilen **ImageWidth** türünde baz tür unsigned long seçilmiş.

### Ön Bildirim Neden Önemli?

- User-defined türler söz konusu olduğunda derleyici bir türün tanımını görmese de o türün bildirimine dayanarak belirli bağlamlarda kullanımı geçerli kabul eder. Derleyicinin varlığından haberdar olduğu ancak henüz tanımını göremediği bir türe **tamamlanmamış tür (Incomplete Type)** denir. Tamamlanmamış türlerden gösterici değişkenler tanımlanabilir ya da tamamlanmamış türler işlev bildiriminde kullanılabilir.

- Tamamlanmamış türleri belirli bir bağlamlarda kullanabilmek için derleyici bu türlerin ön bildirimini görmelidir. Bir türü ön bildirimle kullanabildiğimiz durumlarda bu türün tanımını içeren başlık dosyasını kendi kodumuza dahil etmemiz gerekmez. Bu durumda başlık dosyalarının birbirine bağımlılığı ortadan kaldırıldığı gibi derleme süreleri kısalır.

- Ayrıca başlık dosyasından gelecek isimlerin çakışma riski ortadan kalkmış olur. Aslında tıpki gösterici değişkenlerde olduğu gibi numaralandırma türlerinden değişkenleri de numaralandırma türünün tanımını derleyiciye göstermeden tanımlayabiliriz. Ancak bunun için derleyicinin söz konusu numaralandırma türü için bellekte kaç byte yer ayrılacağını bilmesi gerekir. Aşağıdaki koda bakalım:

```CPP
//fileoperations.h

enum ErrorCode : unsigned int;

class File {
private:
	ErrorCode m_ec;
	///
};
```

> fileoperations.h isimli başlık dosyasında tanımlanan File isimli sınıfın private veri öğelerinden biri ErrorCode numaralandırma türünden. ErrorCode türünün ön bildirimi yapılmış ve bildirimde baz türün unsigned int türü olduğu belirtilmiş. C++11 öncesinde File sınıfının tanımının geçerli olabilmesi için derleyicinin ErrorCode türünün de tanımını görmesi gerekirdi. ErrorCode türünün error.h isimli bir başlık dosyasında tanımlandığını kabul edelim. Bu durumda fileoperations.h başlık dosyası error.h başlık dosyasını dahil edecekti:

```CPP
//fileoperations.h
 
#include "error.h"
 
class File {
private:
	ErrorCode m_ec;
	///
};
```
> Oysa C++11 kurallarına göre artık ErrorCode türünün ön bildirimi bu türden bir veri öğesini kullanabilmemiz için yeterli. Şimdi kazandığımız avantajlara bir bakalım:
fileoperations.h başlık dosyasını dahil eden müşteri kodları ErrorCode türünün tanımını içeren başlık dosyasını dahil etmeyecekler. Böylece:

1. Derleme süresi kısalacak.
2. error.h başlık dosyasında tanımlanan numaralandırma sabitleri olan isimler müşteri kodlar tarafından görülmeyeceği için isim çakışması riski söz konusu olmayacak: ErrorCode türünde onlarca numaralandırma sabiti tanımlanmış olabilir, değil mi?
3. error.h başlık dosyasındaki değişimler fileoperations.h dosyasını dahil eden kodların değiştirilmesini ya da bu kodların yeniden derlenmesini gerektirmeyecek.








































