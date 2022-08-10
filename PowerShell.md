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
<h3>Whatif ve Confirm Parametreleri</h3>

PowerShell ile çok şey yapılabiliyor. Yakında "çok şey" yerine "her şey" de diyebileceğiz. Bu durum da PowerShell'i dikkatli kullanma gereğini ortaya çıkarıyor.

Hemen her komutta bulunan -whatif ve -confirm parametrelerini kullanarak PowerShell komutlarımızı, programlarımızı daha temkinli duruma getirebiliriz.

Whatif parametresi "bunu yapsaydım ne gibi işem gerçekleşecekti?" demek oluyor. Bir komutta bu parametreyi kullandığımızda komut yerine getirilmiyor, yalnızca getirilseydi ne olurdu, bu durum rapor ediliyor.

Örnek olarak, hesap makinesi programı'nı (calculator) durdurmak istediğimizi varsayalım. Komutumuz **stop-process -name calculator** şeklinde olacak.

Komutu bu haliyle verirsek hesap makinesi programı sonlandırılır. Ama komutu **stop-process -name calculator -whatif** şeklinde verirsek program sonlandırılmaz.

Yalnızca komut çalışsaydı ne yapılacağı rapor edilir.

Diğer parametremiz de **-confirm**. Bu parametreyi kullanarak komutun yalnızca biz onay verirsek işletilmesini sağlayabiliriz. Bu da bir derece daha dikkatli olmamızı sağlayacaktır.

**Komut Tarihçesi**

PowerShell oturumunda verdiğiniz komutlar saklanır. Yukarı ve aşağı ok tuşlarınızı kulanarak girilen komutlar arasında dolaşabilirsiniz. Bir oturum içinde verdiğiniz komutların tümünü görmek isterseniz **get-history** komutunu verebilirsiniz. **Clear-History** komutu ile geçmişi temizleyebilirsiniz.

**PowerShell ISE**

PowerShell bir komut satırı ortamı. Ama işler tek tek verilen komutlardan çıkıp programlar yazmaya gelince bir program geliştirme ortamı kullanmak yararlı olabilir.
PowerShell ISE (Integrated Scripting Environment) tam da bu iş için var. Programlarımızı PowerShell ISE içinde de yazabilir ve test edebiliriz.

ISE açıldığında ".ps1" uzantılı bir dosyanın içinde bulunuyoruz. Ps1 uzantılı dosyalar PowerShell betikleridir (Script). Betik içinde bir ya da birden fazla PowerShell komutu ve diğer programlama yapıları bulunur. Bir betik çalıştırıldığında içindeki komutlara ve diğer yönergelere göre çeşiti işlemler yapılır, çıktılar üretilir.

Untitled.ps1  adlı betik dosyasında çalışıyoruz. Bu dosyadaki ilk satırda get-process komutu yer alıyor. ISE ortamındaki Çalıştır "Run Script (F5)" düğmesiyle kodu çalıştırabiliyoruz, sonucunu aşağıdaki bölümde alabiliyoruz. Sağdaki sütundaysa kulanılabillecek PowerShell komutları görülüyor. Bu ve buna benzer kolayıklar sayesinde program geliştirmek kolaylaşıyor.

Bu Repo'da ISE'de değil de doğrudan komut satırı ortamında çalışacağız.

**PowerShell Profilleri**

PowerShell profillerile çalışma ortamımızı kendimize göre şekilendirebiliyoruz. Konsol ortamına girdikten sonra yapabileceğimiz her türlü özelleştirmeyi profil dosyalarında yaparak her seferinde bunları yeniden yapmaktan kurtuluruz.

Profiller Profile.ps1 adındaki dosyalardan oluşturuluyor. Profil dosyalarında bazı değişkenlere değer atayabilir ya da komutlar çalıştırabiliriz. Bunların yardımıyla örneğin, konsol ortamının görünüşünü değiştirebiliriz. Klasik ortama göre en büyük farklardan birisi PowerShell ortamının renkli oluşudur: Arka plan rengi mavidir, ön plandaki harfler sarıdır, hatalar kırmızı renkle gösterilir vb.

*Ben daha çok siyah-beyaz severim bu yüzden aşağıdaki kodlar siyah-beyaz yapmak içindir.*

```
$host.UI.RawUI.BackgroundColor="Black"
Set-PSReadLineOption -TokenKind comment -ForegroundColor white
Set-PSReadLineOption -TokenKind none -ForegroundColor white
Set-PSReadLineOption -TokenKind command -ForegroundColor white
Set-PSReadLineOption -TokenKind parameter -ForegroundColor white
Set-PSReadLineOption -TokenKind variable -ForegroundColor white
Set-PSReadLineOption -TokenKind type -ForegroundColor white
Set-PSReadLineOption -TokenKind number -ForegroundColor white
Set-PSReadLineOption -TokenKind string -ForegroundColor white
Set-PSReadLineOption -TokenKind operator -ForegroundColor white
Set-PSReadLineOption -TokenKind member -ForegroundColor white
cls
```

Profil dosyasının konulacağı klasör de önemli. Profiller ile bilgisayardaki tüm kullanıcıların ortamını ya da yalnızca kendi ortamımızı düzeneyebiliriz. Eğer tüm kullanıcıların ortamını ya da yalnızca kendi ortamımızı düzenleyebiliriz. Eğer tüm kullanıcıların ortamını düzenlemek istiyorsak profil dosyasını **$pshome** değişkeninin gösterdiği klasörde tutmalısınız.

Eğer profil dosyanızdaki ayarları yalnızcakendi kullanıcınız için istiyorsanız o zaman dosyayı **$home** değişkeninin göstediği klasöre kopyalayın.

**Eğlenceli işlemler**

Birinci işlemimiz PowerShell'i konuşturmak. Aşağıdaki iki satırla istediğimiz metnin sesendirilmesini sağlayabiliyoruz:

```powershell
$voice = New-Object -ComObject "sapi.spvoice"
$voice.Speak("Fazz çoh iyidir ama Fazz bi tuhk daha iyidur")
```

Aşağıdaki kod kullanıcıdan gelen bilgiye dayanarak onun karşısına bir mesaj kutusu çıkartıyor:

```powershell
$isim=read-host -prompt "Lütfen adınızı giriniz"
$mesaj="Sen ne iyi bir insansın "+$isim
$wshell = New-Object -ComObject Wscript.Shell
$wshell.Popup($Mesaj,0,"Günün Mesajı",0x1)
```

Aşağıdaki kod da bilgisayardaki DVD sürücüyü açıyor:

```powershell
$Disk = New-Object -ComObject IMAPI2.MsftDiscMaster
$DiskKaydedici = New-Object -ComObject IMAPI2.MsftDiscRecorder2
$DiskKaydedici.InitializeDiscRecorder($Disk)
$diskkaydedici.ejectmedia()
```
Şimdi de üç satırlık bir kodla Youtube'dan bir videonun çalınmasını sağlayalım:

```powershell
$Video=new-object -com internetexpoler.application
$Video.navigate2("https://www.youtube.com/watch?v=GUT0gem7W0Y")
$Video.visible=$true
```

Son olarak da, eğlenceli olduğu kadar yararlı bir komut görelim: test-computersecurechannel.

Test-computersecurechannel komutu, çalıştırıldığı makine ie etki alanı arasındaki güven ilişkisini(trust) denetler. Sonucu da True (Güven ilişkisi var) ya da False (Güven ilişkisi yok) şeklinde döndürür. Burayı biraz açalım: Bir etki alanında (domain), etki alanını denetleyen Domain Controller (DC) ile üye makineler arasında güven ilişkisi kurulur. Bu ilişki haftada iki kez tazelenir. Üye makinenin DC ile güven ilişkisi bozulmuşsa, üye makineye etki alanı kulanıcısıyla oturum açmak istediğimizde "bu makinenin etki alanıyla güven ilişkisi bozulmuştur" şeklinde bir hata mesajı alırız ve oturum açamayız. Böyle bir durumda yaptığımız şey, genelde makineye yerl administrator olarak girip makineyi etki alanından çıkarmak, sonra da tekrar üye olarak eklemektir. Bunları yaparken üye makine iki kez yeniden başatılır.

Ama test-computersecurechannel komutunun -repair ve -credentia parametrelerini kullanıp aradaki güven ilişkisini kolayca yenilememiz mümkün. Bunu yapmak için söz konusu makineye yine yerel administrator olarak girip PowerShell içinden şöyle bir komut vermemiz gerekiyor:

```powershell
Test-computersecurechannel -repair -credential fazz\administrator
```

Komut içindeki -credential parametresinde etki alanının yöneticilerinden birisini verebiliriz. Bu komutu verdiğimşzde bizden o kullanıcının parolasını girmemizi istenecektir. Parolayı girince güven ilişkisi tazelenmiş olur. Makineyi etki alanından çıkarmak, yeniden üye yapmak, bu sırada iki kez yenideen başlatmak gibi işlemlerden de kurtulmuş oluruz.


PowerShell komutlarının nesneleri, işletim sistemindeki ya da uygulamalardaki nesnelerdir. İşletim sistemimiz Windows, nesne tabanlı (Object Oriented) bir işletim sistemidir. Bilgisayardaki sabit disk, kullanıcılar, yazıcılar, programlar hep birer nesnedir.

PowerShell bu nesneleri yönetmek için kullanılır.

Nesnelerin yönetiöinde kullanılabilecek bazı standart işlemler vardır. Örneğin, yerel kullanıcı nesnesi (local user) için şunları yapabiliriz: Yeni bir yerel kullanıcı nesnesi yaratabiliriz, bir yerell kullanıcı nesnesinin bilgilerini getirebiliriz, bir yerel kullanıcının bilgilerini değiştirebiliriz, bir yerel kullanıcı nesnesini silebiliriz, yerel kuanıcı nesnesini devre dışı bırakabilir ya da etkinleştirebiliriz. Yapabileceğimiz bu işlemlere karışık gelen PowerShell komutları da şu şekildedir:

```powershell
Get-localuser : Yerel kullanıcılların hepsinin ya da bir tanesinin bilgisini getirir.

Set-localuser : Bir yerel kullanıcının bilgisini değiştirir.

Enable-localuser : Bir yerel kullanıcıyı etkinleştirir.

Disable-localuser : Bir yerel kullanıcıyı devreden çıkartır.

New-locauser : Bir yerel kullanıcı yaratır.

Remove-localuser : Bir yerel kullanıcıyı siler.

Rename-localuser : Bir yerel kullanıcının adını değiştirir.
```

**Komutların Çıktısını Filtreleme**

PowerShell komutları genelde çok fazla çıktı üretir. Çıktılar ekranda akıp gider. Çoğunlukla da istediğimiz çıktı ekranda görünenlerin küçük bir alt kümesidir. Bu nedenle, komutların tam istediğimiz bilgiyi bize getirmesini sağlamak önemlidir.


Birçok komutta bilgilerin tümünü değil de istenenleri getirmek için parametreler bulunur. Örnek olarak, olay günlüklerindeki kayıtları getiren get-eventlog komutuna bakalım. Aşağıdaki komut "System" günlüğündeki tüm olay kayıtlarını getirir.

```powershell
Get-Eventlog system
```

System günşüğündeki yalnızca son 20 olayı görmek isterseniz komutun "-newest" parametresini kullanabiliriz. Örneğin, **Get-Eventlog System -newest 20** komutu System günlüğündeki son 20 olayın bilgisini getirir.

Bir başka örnek olalrak get-aduser komutunu verebiliriz. Active Directory'deki tüm kullanıcıların bilgisini getirmek için get-aduser filter * komutunu veririz. Ama örneğin yanızca Active Directory'de "GothamBolge" adındaki yapısal birime (OU) bulunan kullanıcıların listesini almak için "-searchbase" (Arama başlangıç noktası) parametresini kullanarak aşağıdaki komutu verebiliriz:

```powershell
Get-aduser -filter * -searchbase "ou=GothamBolge, dc=anadolu, dc=com"
```
Get-aduser komutunda olduğu gibi bir çok komutta da "-Filter" parametresi bulunur. Bu parametreyle istediğimiz bigileri "süzebiliriz". Örneğin, aşağıdaki komutla tüm kullanıcıları değil de "Office" alanında "Ek Bina" yazan kullanıcıları getirebiliriz:

```powershell
Get-aduser -filter {Office -eq "Ek Bina"}
```
Yukarıdaki örnekleri birleştirip hem "Office" alanında "Ek Bina" yazan hem de "GothamBolge" yapısal biriminde olanları getirebilir, böylce istediğimiz bilgiyi daha duyarlı tanımlayabiliriz.

```powershell
Get-aduser -filter {Office -eq "Ek Bina"} -searchbase "ou=GothamBolgei dc=anadolu, dc="com"
```
"-filter" parametresini kullanabilecek komutların listesini amak için get-command -paramatername filter komutunu verebiliriz.

