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




























































