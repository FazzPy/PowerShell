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
