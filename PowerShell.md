# Fazz | PowerShell Notes

**PowerShell bir komut satırı ortamı. Önceki komut satırı ortamı 40 yıla yakın bir süredir bizimle. PowerShell onun yerini alıyor.**

**Windows'Ta klasik komut satırına CMD komutuyla erişebiliriz. PowerShell'in kendi kısayolları var ama klasik komut satırından powershell komutuyla da PowerShell'e erişmek mümkün.**

**Microsoft PowerShell'e çok önem veriyor. PowerShell ile işletim sisteminin ve işletim sistemi üzerindeki tüm uygulamaların yönetilebilmesi amaçlanıyor.**

**Son sürümü olan PowerShell 6.0 ile PowerShell'in Linux ve MacOS üzerinde çalışması sağlandı.**

**Bu yüzden PowerShell'i öğrenmek daha da önem kazandı.**

<hr>

<h3>PowerShell'i Öğrenmeye basit komutlarla başlıyalım.</h3>

*Çalışmakta olan hizmetleri(Service) görmek için get-service komutunu verelim:*
```
get-service
```
*yazdırma Biriktiricisi (Spooler) adındaki hizmeti durduralım, yeniden başlatalım.*

**Gereken Komutlar:**
```
stop-service spooler ve start-service spooler komutları ile yapılabilir.
```
**Hizmeti durdurma komutu verd,ü,m,zde hata alabilirsiniz. Hatanın nedeni, PowerShell ortamı yönetici olarak açmamamız. Yeni bir PowerShell ortamını "Run as Administrator" şıkkıyla açarsak bu hatadan kurtulabiliriz.**

*Hizmetleri yeniden başlatmak için tek bir komutu, restart-service komutunu da kullanabiliriz.*

Tek bir hizmetin durumunu da **get-service** komutuyla inceleyebiliriz. Örneğin, "DHCP İstemcisi" (Kısaca DHCP) hizmetini incelemek için vermemiz gereken komut **get-service dhcp** şeklindedir.

*Hizmetleri durdurduğumuz gibi bilgisayarı da yeniden başatabiliriz ya da kapatabiliriz.*

Bilgisayarı yeniden başlatma komutu : **restart-computer**

Bilgisayarı kapatma komutu : **stop-computer**

Bilgisayarımızın DNS sunucusundan aldığı ve kaşelediği bilgieri görmek için **get-dnsclientcache** komutunu verebiliriz.

Kurulu sistemimizde tanımlı olan aygıt sürücülerini görmek için **get-windowsdriver-online** komutunu verebiliriz. Bu komuttaki "-online" parametresi şu anda çalışmakta olan işletim sistemi anlamına geliyor.

Yerel kullanıcıları görüntülemek için **get-localuser** komutunu verebiliriz.

Çalışmakta olan programları görmek için **get-process** komutunu verelim.

**Get-process** komutunda programların uzantılarının (.exe) gibi listelenmediğine dikkat edin.

Şimdi de **Get-process** komutuyla gördüğümüz bir programı, "calculator" programını sonlandıralım.

Bunun için vermemiz gereken komut **stop-process -name calculator**

Bir programı adıyla değil de ID'siyle (kimlik numarası) da sonlandırabilirsiniz. Bunun için vermemiz gereken komut: **stop-process -id 4188**

Yukarıdaki komutu verdiğimizde ID'si 4188 olan programı sonlandıracak.

```
Şu ana kadar gördüğümüz komutlar hep üzerinde bulunduğumuz makinede çalışıyordu.
Bu komutları ağdaki bir bilgisayarı yönetmek için de kullanıp o makinelerdeki hizmetleri görüntüleme, 
makineleri yeniden başlatma gibi işlemleri yapabiliriz.
Bunu sağlamak için hemen her PowerShell komutunda "-computername" benzeri bir parametre vardır.
Bu parametreyi kullanarak komutun hangi makine için işlem yapacağını belirtebiliyoruz.
Örneğin, "anasunucu" adındaki makinede bulunan hizmetleri görüntülemek için vermemiz gereken komut : 
(get-service -computername anasunucu) Şeklindedir. Bu makineyi kapatmak istersek
stop-computer -computername anasunucu komutunu kullanabiliriz.
Eğer kapatmayı zorla isterseniz "-force" parametresi yazabilirsiniz.
```

**Yardım Bilgisi**

Peki, stop-process'in parametreleri olan -name ya da -id ifadelerini nereden biliyoruz? Bu komutun başka parametreleri, örnek kullanımları var mıdır?

Bu soruların yanıtını **get-help** komutuyla alabiliriz. Get-help komutu bir PowerShell komutu hakkında bilgi verir.

```
get-help stop-process
get-help start-process
```

Yardım bilgisi bu haliyle çok yardımcı değil. Özellikle de kullanım örneklerini göremiyoruz. Stop-process komutunun örneklerini almak için:

**get-help stop-process -examples** şeklinde yazabiliriz.

Eğer bir komuta ilişkin yardım bilgilerinin hepsini (Örneklerle birlikte) almak istersek komutu **get-help stop-process -full** Şeklinde vermeliyiz.

Komutu biliyorsak onun kullanımıyla ilgili bilgileri get-help komutundan alabiliyoruz. Peki, get-process, stop-process gibi hangi komutlar var PowerShell'de?

Bu sorunun yanıtını da **get-command** ile alıyoruz. Get-command komutu kullanılabilecek komutları listeler.

**(getcommand).count** komutu ile bilgisayarınızda kaç adet komut olduğunu görebilirsiniz.

```
command -name *dns*
Komutu ile adında dns geçen komutları bulabilirsiniz.
(get-command -name *dns*).count
Komutu ile içinde DNS geçen komutların sayısını görebilirsiniz.
```


