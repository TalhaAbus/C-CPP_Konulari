Necati Ergin'in C++ Kursundan Notlar

# Tür Dönüştürme Operatör Fonksiyonları


- Bir sınıf türünden nesneyi bir başka türe dönüştürmek için kullanacağımız fonksiyonlardır. Yani derleyici durumdan vazife çıkartıp bu fonksionlara çağrı yaparak sınıf türünden nesneyi başka bir türe dönüştürme olanağına sahip olacak. 
**Bir notu hatırlayalım:**
> Normale mümkün olmayan bir dönüşüm eğer bir fonksiyon bildirimiyle, derleyicinin o fonksiyona çağrı yapması halinde gerçekleştiriliyorsa böyle dönüşümlere user-defined conversion deniliyordu. Şimdiye kadar biz user defined conversion un conversion constructorlar ile yapılcabileceğini gördük. Yani derleyici sınıfın conversion constructor ına çağrı yaparak sınıf türünden olmayan bir değeri sınıf türüne dönüştürebiliyordu. 

- Şimdi user defined conversion ın yapılcabileceği ikinci bir yol öğrenceğiz. Sınıf türünden olan bir nesnenin başka bir türe dönüştürülmesini sınıfın tür dönüştürme operator fonksiyonları ile gerekleştirebiliriz. 

**Bir örnek:**

```CPP
class Myclass{

};

int main()
{
    Myclass m;
    int ival = m;
}
```

> Sentaks hatası, Myclass sınıfından int türüne otomatik dönüşümyok. Hata mesajı: cannot convert from Myclass to int 

> Peki ben bir fonksiyon bildirsem - Bir sınıf türünden nesneyi bir başka türe dönüştürmek için kullanacağımız fonksiyonlardır. Yani derleyici durumdan vazife çıkartıp bu fonksionlara çağrı yaparak sınıf türünden nesneyi başka bir türe dönüştürme olanağına sahip olacak. 

**Bir notu hatırlayalım:**

> Normale mümkün olmayan bir dönüşüm eğer bir fonksiyon bildirimiyle, derleyicinin o fonksiyona çağrı yapması halinde gerçekleştiriliyorsa böyle dönüşümlere user-defined conversion deniliyordu. Şimdiye kadar biz user defined conversion un conversion constructorlar ile yapılcabileceğini gördük. Yani derleyici sınıfın conversion constructor ına çağrı yaparak sınıf türünden olmayan bir değeri sınıf türüne dönüştürebiliyordu. 



- Şimdi user defined conversion ın yapılcabileceği ikinci bir yol öğrenceğiz. Sınıf türünden olan bir nesnenin başka bir türe dönüştürülmesini sınıfın tür dönüştürme operator fonksiyonları ile gerekleştirebiliriz. 



**Bir örnek:**



```CPP

class Myclass{



};



int main()

{

    Myclass m;

    int ival = m;

}

```




> Sentaks hatası, Myclass sınıfın derleyici bu fonksiyona çağrı yaparak Myclass türünden bir nesneyi int türüne dönüştürebilir mi? Evet. Bu dönüşümleri gerçekleştirecek fonksiyonlara tür dönüştürme operatör fonksiyonları denir. 

> Peki böyle bir fonksiyon nasıl bildirilecek? Bu da bir opratör fonksiyonu olduğu için yine operator keyword u kullanılacak. Bunun yanına hangi türe dönüşüm gerçekleşecekse o tür yazılcak.

**örnek:**

**Myclass türünden bir nesneyi:**
- int türüne dönüştürecek fonksiyonun ismi operator int
- double türüne dönüştürecek olan operator double
- int * türüne dönüştürecek olan operator operator int*

> operator int fonksiyonunun geri dönüş değeri int. Bu geri dönüş değeri yazılmayacak.

**Örnek bir dönüşüm:**

```CPP
class Myclass {
public:
	operator int(const)
	{
		std::cout << "Myclass::operator int() this =" << this << "\n";
		return 1;
	}
};

int main()
{
	Myclass m;

	int x = m;
}
```
> Bir sentaks hatası yok.

**Aynı örnek üzerinden:**

```CPP
class Myclass {
public:
	operator int(const)
	{
		std::cout << "Myclass::operator int() this =" << this << "\n";
		return 1;
	}
};

int main()
{
	Myclass m;
	double dval;
	dval = m;
}
```
> Burada Myclass nesnesi int e dönüştürülecek sonrasında int double a dönüştürülecek. Birincisi user defined converison ve ikincisi standart conversion.

**Aynı örnek üzerinden:**

```CPP
class Myclass {
public:
	operator int(const)
	{
		std::cout << "Myclass::operator int() this =" << this << "\n";
		return 1;
	}
};

int main()
{
	Myclass m;

	if(m){}
}
```
> Sentaks hatası olmayacak. Derleyici sınıfın operator int fonksiyonunu çağıracak. int türünden de bool türüne dönüşüm olduğu için kod geçerli olacak.

- Bu örtüülü dönüşüm bazen bizim yararımıza olmayabilir. Tür dönüştürme operator fonksiyonları modern CPP öncesinde explicit olamıyordu. 

**Örnek:**

```CPP
class Myclass {
public:
	explicit operator int(const)
	{
		std::cout << "Myclass::operator int() this =" << this << "\n";
		return 1;
	}
};
```
> burada explicit yapıp yapmamak bizim seçeneğimiz. Bu dömüşümün otomatik olarak gerçekleşmesi gerekiyorsa explicit yapılmayacak. Ama birçok örnekte explicit olasında fayda var çünkü isteğimiz dışında tür dönüşümü gerçekleştirebilir.

**Örnek:**

```CPP
class Myclass {
public:
	explicit operator int(const)
	{
		std::cout << "Myclass::operator int() this =" << this << "\n";
		return 1;
	}
};

int main()
{
	int x = 5;
	Myclass m;

	x = m;
}
```

> Artık kod legal değil çünkü tür dönüştürme operatörü explicit. Burada örtülü dönüşüm sentaks hatası ama biz kendimiz static_cast operatörü ile dönüşüm gerçekleştirebiliriz.

```CPP
x = static_cast<int>(m);
```

**Bir Öneri:**
Makul bir neden olmadıkça tür dönüştürme operatörlerini explicit yapınız.

- Bir sınıf türü bool gerektiren hiçbir yerde kullanılamaz. Ama sınıfın bool türüne dönüşüm yapan bir fonksiyonu varsa kullanılabilir. 

**Örnek:**

```CPP
class Nec {
public:
	operator int()const;
};

int main()
{
	Nec nec1, nec2;
	!nec1;
	nec1&& nec2;
	nec1 || nec2;
	nec1 ? 10 : 20;
	if (nec1);
}
```
> Kodların hepsi geçerli oldu. Derleyici artık boolean değer beklenen yerde sınıfın operator int fonksiyonunu çağırdı ve bunu geri dönüş değerini de standart conversion ile bool türüne dönüştürdü. 

**Örnek:**

```CPP
class Nec {
public:
	operator bool()const;
};

int main()
{
	Nec mynec;

	int x = mynec;

	if (mynec) {

	}
}
```

> Burada kod geçerli. Önce bool türüne dönüşecek ardından bool türünden int türüne dönüşecek. If kısmında ise derleyici sınıfın operator bool fonksiyonunu çağıracak. 

**Ama explicit yaptığım zaman:**

```CPP
class Nec {
public:
	explicit operator bool()const;
};

int main()
{
	Nec mynec;

	int x = mynec;

	if (mynec) {

	}
}
```

> if deyimi geçerliliğini koruyacak çünkü boolean context ama bir üstteki sentaks hatası. 
- Bazı C++ standart kütüphanesinin sınıfları operator bool fonksiyonuna sahip ve bunlar explicit. Yani boolean context varsa dönüşüm sağlıyorlar ama boolean contexct dışında dönüşüm sağlamıyorlar.

**Bir mülakat sorusu:**
```CPP
class Nec {
public:
	operator bool()const
	{
		return true;
	}
};

int main()
{
	Nec x, y;
	auto val = x + y;
	std::cout << "val =" << val << "\n";
}
```

> val değişkeninin değeri int Ama değeri 2. operator bool fonksiyonu explicit olsaydı sentaks hatası olacaktı. 

**Örnek:**

```CPP
int main()
{
	using namespace std;

	unique_ptr<string> up;

	if (up) {
		std::cout << "not empty!\n";
	}
	else {
		std::cout << "empty!\n";
	}
}
```
> if parantezi içinde unique_ptr nesnesini kullanıdım zaman unique_ptr nesnesinin oıperator bool fonksiyonu çağırılıyor. Bu fonksiyon true ya da false döndürecek. True demek, unique_ptr nesnesinin hayatını kontrol etmekte olduğu dinamik ömürlü bir string söz konusu. Eğer false döndürürse unique_ptr nesnesi boş. Aslında derleyici if içindeki ifadeyi operator bool fonksiyonuna yapılan çağrıya dönüştürdü. unique_ptr nin operator bool fonksiyonu explicit bir fonksiyondur. Gerektiği yerde (if içinde) dönüştürüldü.



































































