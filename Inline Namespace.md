Necati Ergin Notlarından Alıntıdır:
https://necatiergin2019.medium.com/inline-isim-alanlar%C4%B1-inline-namespace-8143ef0d0ef2

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

```CPP
namespace A {
	inline namespace B {
		int x = 10;
	}
}

int main()
{
	A::B::x = 20;
	A::x = 20;
}

```

> x isimli değişkenin A isim alanı içinde yer alan B isim alanı içinde tanımlandığını görüyorusnuz. B isim alanı inline olarak tanımlandığından main işlevi içinde x ismini:

```CPP
A::B::x
```

> biçiminde kullanabileceğimizi gibi doğrudan:

```CPP
A::x
```
> biçiminde de kullanabiliyoruz. Birden fazla isim alanını da inline olarak tanımlamak mümkün:

```CPP
namespace A {
	inline namespace B {
		inline namespace C {
			int x = 10;
		}
	}
	inline namespace D {
		int y = 20;
	}
}

int main()
{
	A::x = 1;
	A::B::x = 2;
	A::B::C::x = 3;

	A::y = 4;
	A::D::y = 5;
}
```

> Yukarıdaki kodda B,C ve D isim alanları inline olarak tanımlandığından main işlevği içinde x ve y isimlerinin doğrudan A ismiyle nitelenerek kullanılması mümkünm oluyor.

- İyi de, ne işe yarıyor inline isim alanları? Inline isim alanlarının sağladığı en önemli avantajlarından biri sürüm (version) kontrolü. Aşağıdaki koda bakalım:

```CPP
namespace Networking {
	class TCPSocket {
		//
	};
	class UDPSocket {
		//
	};
}
```

> Networking isim alanı içinde TCPSoket ve UDPSocket sınıfları tanımlanmış.Bu isim alanları içinde tanımlanan bu sınıflar birçok kaynak dosya tarafından kullanılıtyor olsun. Şimdi TCPSocket sınıfında yaptığımız bazı geliştirmeler sonucunda yeni bir sınıf oluşturduğumuzu düşünelim. Yani TCPSocket sınıfının ikinci bir sürümünü oluşturduk. Müşteri kodların eski TCPSocket sınıfı yerine yeni TCPSocket sınıfını kullanmalarını istiyoruz. Bunun için birçok seçenek olabilir ancak en etkin çözümlerden biri bu sınıfları ayrı birer isim alanı içine koymak.

```CPP
namespace Networking {
	namespace Version1 {
		class TCPSocket {
			//...
		};
	}
	namespace Version2 {
		class TCPSocket {
			///...
		};
	}

	class UDPSocket {
		//...
	};
}
```

> Ama müşteri kodlar TCPSocket sınıfını

```CPP
Networking::TCPSocket
```
> biçiminde derleyetek kullanıyorlardı değil mi? Müşteri kodları hiç değiştirmeden  sürüm geçişini sağlayabilir miyiz? Evet, inline isim alanı burada devreye giriyor. Yeni sürümün yer aldığı version2 isim alanını inline yapıyoruz:

```CPP
namespace Networking {
	namespace Version1 {
		class TCPSocket {
			//..
		};
	}
	inline namespace Version2 {
		class TCPSocket {
			//..
		};
	}
	class UDPSocket {
		//..
	};
}
```

> Artık daha önce eski sürümü kullanıyor olan müşteri kodlar yeniden derlendiklerinde yeni sürümü kullanıyor olacaklar. 

**İnline isim alanları kütüphanenin gerçekleştirimini yapan programcıya varsayılan (default) bir isim alanı belirleme olanağı sağlıyor.**

> Yukarıdaki örnekte tüm kullanıcı kodların TCPSocket sınıfının son sürümünü kullanmaları için **Version2** isim alanınıinline yaptık. Belirli bir nedenden dolayı eski sürüme geri dönmemiz gerekirse bu kez **Version1** isim alanını inline yapabiliriz. İstediğimiz sayıda isim alanını inline yapabiliriz. Örneğin kütüphanemizin 3. sürümünde UDPSocket sınıfının da yenilendiğini düşünelim:

```CPP
namespace Networking {
	namespace Version1 {
		class TCPSocket;
		class UDPSocket;
	}
	inline namespace Version2 {
		class TCPSocket {
			//..
		};
	}
	inline namespace Verison3 {
		class UDPSocket;
	}
}
```
> Version3 isim alanı inline olarak tanımlandığından kulanıcı kodlar UDPSpcket sınıfının son sürümünü (Bu isim alanı içindeki son sürümünü) kullanıyor olacaklar. Dilediğimiz zaman bu içsel isim alanını inline olmaktan çıkartıp Version1 isim alanını inline yaparak o sürümdeki sınıfı kullanmaya geri dönebiliriz.


## Öneişlemci koşullu derleme ile Inline
**Inline anahtar sözcüğünün kullanımını önişlemci koşullu derleme (Conditional compiling) komutlarına da bağlayabiliriz:

```CPP
namespace Networking {
	namespace Version1 {
		class TCPSocket;
		class UDPSocket;
	}
	inline namespace Version2 {
		class TCPSocket;
	}
#ifndef USE_RAW_SOCKET
	inline
#endif
		namespace Version3 {
			class UDPSocket;
	}
#ifdef USE_RAW_SOCKETS
	inline
#endif
		namespace RawUDPSockets {
		class UDPSocket;
	}
}
```

Yukarıdaki kodda **USE_RAW_SOCKETS** makrosu tanımlanmamış ise **Version3** isim alanı inline yapılmış olacak. Böylece bu isim alanı içindeki UDPSocket sınıfı doğrudan Networking isim alanında görülüyor olacak. Eğer **USE_RAW_SOCKETS** makrosu tanımlanmamış ise bu kez RawUDPSockets isim alanı inline yapılmış olacak. Bu durumda da bu isim alanı içndeki UDPSocket sınıfı doğrudan Networking isim alanında görülüyor olacak. Bir başka deyişle UDPSocket sınıfının hangi sürümünün kullanılacağı **USE_RAW_SOCKETS** makrosunun tanımlanmış olupğ olmamasına bağlı.

## ADL ile inline (Argument dependent lookup) 

```CPP
namespace Nec {
	namespace Nested {
		class C {

		};
	}
	using namespace Nested;
	void func(Nested::C);
}

int main()
{
	Nec::Nested::C x;
	func(x); // Geçersiz
}
```

> Nec isim alanı içinde bildirilen func isimli işlevin parametresinin Nested isim alanı içinde tanımlanan C sınıfı türünden olduğunu görüyorsunuz. Nec isim alanı içinde yapılan using namespace bildirimi ile Nested isim alanı içindeki isimler Nec isim alanı içinde görünür kılınmış. Ancak main işlevi içinde yapılan func çağrısı geçerli değil. Yapılan using namespace bildirimine karşın argğmana bağlı isim arama (ADL) burada devreye girmiyor. Yeni kurallara göre Nested isim alanının inline olarak bildirilmesi durumunda argümana bağlı isi maram aile func isminin Nec isim alanında aranması garanti altında.

### Standart C++ kütüphanesinde inline kullanımı

**C++ standart kütüphanesi de inline isim alanlarını kullanıyor.** Örneğin başlık dosyasından gelen string_literals isim alanı ve bunu içine alan literals isim alanı inline olarak nitelenmişler:

```CPP
#include <string>

using namespace std;

int main()
{
	auto name = "necati"s;
}
```
> Yukarıdaki kodda kullanılan **user defined literal** operatör fonksiyonu **s** aslında **literals** isim alanı içerisindeki **string_literals** isim alanında bildirilmiş olmasına karşın nitelenmeden (unqualified) kullanılabiliyor.

```CPP
namespace std {
    inline namespace literals {
	inline namespace string_literals {
	    string operator""s(const char *str, size_t len);
	}
    }
}

```

Necati Ergin Notlarından Alıntıdır:
https://necatiergin2019.medium.com/inline-isim-alanlar%C4%B1-inline-namespace-8143ef0d0ef2













