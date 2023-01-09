# Referanslar 

## Referanslar nasıl tanımlanır?

- Nasıl bir tanımlanırken gösterici ismin önüne * atomu koyuluyorsa, bir referans tanımlanırken de referans isminden önce & atomu yazılır.

**Örnek:**

```CPP
int i = 20;
double d = 10.2;

int& ri = i;	// ri int türden bir referanstır.
double& rd = d;	// rd double türden bir referanstır.
```

> Gösterici değişkenlerden farklı olarak, bir referans aynı türden bir nesne ile ilk değer verilerek tanımlanmalıdır.

> Yukarıdaki örnekte ri referansı int türünden i nesnesi ile, rd referansı double türünden d nesnesi ile ilkdeğer verilerek tanımlanıyor. Tanımlamalarda kullanılan '&' bir işleç değildir. Yalnızca tanımlanan nesnenin bir referans olduğunu derleyiciye bildirir. Referansın ilk değer verilmeden tanımlanması geçersizdir.

- Bir referans ilk değer olarak ona atanan nesnenin yerine geçer.

```CPP
int &r = b;
```

> Bu tanımlamadan sonra artık r nesnesi, görülebilir olduğu her kaynak kod dosyasında b değişkeninin yerine geçer.

> Artık b değişkenine ulaşmanın bir başka yolu da r ismini kullanmaktır. r referansı b değişkenine bağlanmıştır.




























