# Windows 10 - 11 sık sorulan sorular
Aşağıda sorun çözümleri için verdiğim komutları uyguladıktan sonra sorun devam ederse mutlaka bilgisayarı yeniden başlatın.

### Windows 10'mu Windows 11'mi kurmalıyım?
Sistem gereksinimleri Windows 11'in ihtiyaçlarını karşılıyorsa Windows 11 kurabilirsiniz. Desteklemediği durumlarda TPM şartı arayan oyun veya uygulamalarda sorun yaşayabilirsiniz. Kurulum aşamalarında bu ihtiyaçları her ne kadar Bypass etme şansımız olsa da bu tarz durumlarda yaşayacağınız hatanın çözümü yoktur. Mecburen Windows 10 yüklemeniz gerekir. Windows 11'in bir sürüm sonra daha kararlı olacağını düşünüyorum. 22H2 sürümünü beklemekte fayda var.

### Sistemleri nasıl düzenliyorum?
Sistemlerde yaptığım değişikliklerin bir kısmını kendi hazırladığım Builder.bat ile yapıyorum geri kalan bölümleri NTLite ücretsiz versiyonu ile düzenliyorum. Builder'ı daha önceden isteyenler için paylaşıyordum ancak yaptığım değişikliklerden sonra paylaşmama kararı aldım. Yapılan değişiklikler hakkında çok detaylı bir rehber hazırlıyorum. Yayınladığımda oradan bakabilirsiniz. Lütfen Builder.bat için istekte bulunmayınız.

### Windows 8.1 sistem linkleri güncellenecek mi?
Windows 8.1 sistemler artık güncellenmeyecek. Bu bölümde güncellemeyi durdurduğum için Toolbox'a da güncelleme vermiyorum. 

### Microsoft Store ve Xbox yüklü mü?
Evet yüklüdür. Microsoft Store / Mail / Takvim / Hesap makinesi / Ekran Yakalama / Appx Installer ve Store için gerekli olan servisler yüklüdür. Uygulama veya oyunlarda herhangi bir hata almazsınız. 

### Yazıcı çalışmıyor, nasıl düzeltirim?
Yazıcı hizmetleri kapalıdır. Yazıcı hizmeti otomatik ayarın dışında çalışırken hata verdiği için ve yazıcı cihazı her evde bulunmadığından gereksiz işlem yükünü engellemek için kapattım. Açmak için Toolbox'dan  'Hizmetleri Yönet' bölümünden yazıcı hizmetini aktifleştirebilirsiniz. CMD üzerinden etkinleştirmek için aşağıdaki komutları yönetici yetkili CMD ekranına yapıştırın. Hizmetlerden açmak istiyorsanız 'Yazdırma biriktiricisi' ayarını otomatiğe alıp başlatınız.

    • sc config UmRdpService start= demand
    • sc config Spooler start= auto
    • net start Spooler /y
    
### Fax çalışmıyor, nasıl düzeltirim?
Fax hizmeti kaldırılmıştır. Fax cihazı evde bulunmayı geçtim artık normal şartlarda bile bulunması zor olan bir cihaz bundan dolayı hizmeti tamamen sildim. yeniden yüklemek için aşağıdaki komutları yönetici yetkili CMD ekranına uygulayabilirsiniz. 

    • Dism /Online /Add-Capability /CapabilityName:Print.Fax.Scan~~~~0.0.1.0
    • sc config Fax start= demand
    • sc config UmRdpService start= demand

### Spotlight çalışmıyor, nasıl düzeltirim?
Spotlight özelliği çalışmıyor, çalışmasını sağlayacak bir düzenleme şu an için mevcut değildir.
    
### Tarayıcı çalışmıyor, nasıl düzeltirim?
Tarayıcı hizmetleri kapatılmıştır. Tarayıcı cihazıda maalesef her evde bulunmuyor. Gereksiz işlem yükünü önlemek için kapatılmıştır. Açmak için yönetici yetkili CMD ekranına aşağıdaki komutları uygulayın. Toolbox'dan açmak için Hizmetleri yönet bölümünden 'Kamera ve Tarayıcı hizmetini' açabilirsiniz.

    • sc config WiaRpc start= demand
    • sc config StiSvc start= demand
    • sc config FrameServer start= demand
    • sc config FrameServerMonitor start= demand

### Hızlı kullanıcı değiştiremiyorum, nasıl düzeltirim?
Güncel sistemlerde bu ayar varsayılan olduğu için böyle bir sorun yaşamazsınız. Eski düzenlemelerimden birini kullanıyorsanız sorunu çözmek için aşağıdaki komutları yönetici yetkili CMD ekranına yapıştırın ve reset atın.

    • reg add "HKLM\SOFTWARE\Microsoft\Windows\CurrentVersion\Policies\System" /v "HideFastUserSwitching" /t REG_DWORD /d 0 /f 
    • reg add "HKLM\SOFTWARE\WOW6432Node\Microsoft\Windows\CurrentVersion\Policies\System" /v "HideFastUserSwitching" /t REG_DWORD /d 0 /f
    • sc config seclogon start= demand

### Kamera çalışmıyor, nasıl düzeltirim?
Kamera cihazının yönetimini sağlayan hizmet kapatılmıştır. Kameranızı çalışır ancak birden fazla uygulama kameraya erişmek istediğinden hata alabilirsiniz. Bu sorundan kurtulmak için tarayıcı cihazları için uyguladığımız komutları burada da uyguluyoruz. Açmak için yönetici yetkili CMD ekranına aşağıdaki komutları uygulayın. Toolbox'dan açmak için Hizmetleri yönet bölümünden 'Kamera ve Tarayıcı hizmetini' açabilirsiniz.

    • sc config WiaRpc start= demand
    • sc config StiSvc start= demand
    • sc config FrameServer start= demand
    • sc config FrameServerMonitor start= demand
    
### Mikrofon ayarlarına girerken alınan 'bellek taşma hatası' nasıl düzeltilir?
Toolbox'dan Optimizasyon bölümünden SVChost Ram Optimizasyonu bölümünü uyguladıysanız bu sorunu yaşamanıza sebebiyet verebilir. Düzeltmek için aynı yerden kapatma komutunu uygulayınız. 

Bir diğer ihtimal ise driver'dan kaynaklanır. Bunu çözmek için driverı donanım kimliği ile tespit edip indirmeniz gerekiyor. Eski driverı sildikten sonra yeni indirdiğiniz driverı uygulayarak çözebilirsiniz. Donanım kimliğiyle driver bulmayı bilmiyorsanız Google'dan aratıp bilgi sahibi olabilirsiniz. Birçok açıklayıcı rehber bulunmaktadır.

Bu iki yolda çözüme ulaştırmadıysa PC'nizde farklı bir sorun söz konusudur. Bildiğim başka bir çözümü yoktur.

### Driverlar otomatik yüklenmedi, nasıl düzeltilir?
Bazı geri bildirimlerde donanımı sorunlu olup pasif halde bırakarak kullanan kişilerin bu ayardan dolayı blue screen hatası aldığını tespit ettiğim için kapattım. Buradaki Blue Screen kullanıcının bozuk donanımından kaynaklanmaktadır. Ayrıca Windows Update her zaman güncel driverları kurmadığından kapatmak daha uygun geldi. Ancak bu bölümü kullanmak isteyenler toolbox üzerinden 'Hizmetleri Yönet' bölümünden 'Driver Yükle/Güncelle hizmetini' açabilir. CMD ile açmak isteyenler yönetici yetkili CMD ekranına aşağıdaki komutları uygulamalıdır.

    • reg add "HKLM\SOFTWARE\Microsoft\PolicyManager\current\device\Update" /v "ExcludeWUDriversInQualityUpdate" /t REG_DWORD /d 0 /f
    • reg add "HKLM\SOFTWARE\Microsoft\PolicyManager\default\Update" /v "ExcludeWUDriversInQualityUpdate" /t REG_DWORD /d 0 /f
    • reg add "HKLM\SOFTWARE\Microsoft\PolicyManager\default\Update\ExcludeWUDriversInQualityUpdate" /v "value" /t REG_DWORD /d 0 /f
    • reg add "HKLM\SOFTWARE\Microsoft\WindowsUpdate\UX\Settings" /v "ExcludeWUDriversInQualityUpdate" /t REG_DWORD /d 0 /f 
    • reg add "HKLM\SOFTWARE\Policies\Microsoft\Windows\WindowsUpdate" /v "ExcludeWUDriversInQualityUpdate" /t REG_DWORD /d 0 /f 
    • reg add "HKLM\Software\Policies\Microsoft\Windows\DriverSearching" /v "SearchOrderConfig" /t REG_DWORD /d 1 /f 

### Ayarlardan cihazlar bölümü açılmıyor, nasıl düzeltirim?
Bu sorun Toolbox'dan 'Hizmetleri Yönet' bölümünden 'Uzak Masaüstü/Akış/Ağ hizmetleri' kapatıldığında yaşanır. Sorunu çözmek için bu bölümü aktif hale getirin. Bu bölümü açtıktan sonra Windows Search hizmeti de açılır. Onu kapatabilirsiniz. 

### Görev çubuğundaki arama bölümü çalışıyor mu?
Evet, çalışıyor. Başlat menüsüne tıklayıp yazdığınızda zaten aynı işlevi gördüğü için arama simgesini sistemlerden kaldırdım. Görev çubuğuna sağ tıklayıp açabilirsiniz.

### EdgeWebView2 yüklenmiyor, nasıl düzeltilir?
EdgeWebView2'nin otomatik olarak yüklenmesini engelledim. Bazı ihtiyaç duyduğu alanlarda otomatik yüklenebiliyor. Ancak manuel kurulumlarda hata alabilirsiniz. CMD üzerinden etkinleştirmek için aşağıdaki komutları yönetici yetkili CMD ekranına yapıştırın.

    • reg add "HKLM\SOFTWARE\Policies\Microsoft\EdgeUpdate" /v "InstallDefault" /t REG_DWORD /d 1 /f

### Dikte hizmeti(Konuşarak yazdırma) çalışıyor mu? (Windows + H)
Hayır, çalışmıyor. Açılması yaptığım düzenlemeden dolayı mümkün değildir.

### Narrator Quick Start (Ekran okuma) çalışıyor mu? 
Hayır, çalışmıyor. Yapılan düzenleme kaldırılıp güncelleme sonrası yeniden yüklenme ihtimaline karşı regedit ile engellenmiştir.

### Defender yüklü mü?
Defender tamamen kaldırılmıştır. Güncelleme sonrası bazı bileşenleri yüklenebilir. Ancak hizmet çalışmayacaktır. Yeniden yüklenemez.

### Valorant oyununda sorun yaşanır mı?
Defender olmadığı için sorun yaşanacağını düşünenler olabiliyor. Herhangi bir sorun yok. Testler yapılmıştır. Valorant oyunu sorunsuz bir şekilde çalışmaktadır.

### Konum hizmeti çalışıyor mu?
Konum hizmeti kapatılmıştır. Toolbox 'Hizmetleri yönet' bölümününden açılabilir. CMD üzerinden etkinleştirmek için aşağıdaki komutları yönetici yetkili CMD ekranına yapıştırın.

    • reg delete "HKLM\SOFTWARE\Policies\Microsoft\Windows\LocationAndSensors" /v "DisableLocation" /f
    • reg add "HKLM\SOFTWARE\Microsoft\Windows\CurrentVersion\CapabilityAccessManager\ConsentStore\Location" /v "Value" /t REG_SZ /d "Allow" /f
    • reg add "HKLM\SOFTWARE\Microsoft\PolicyManager\current\device\System" /v "AllowLocation" /t REG_DWORD /d "1" /f
    • sc config NaturalAuthentication start= demand
    • net start NaturalAuthentication /y
    • sc config lfsvc start= demand
    • net start lfsvc /y

### Bluetooth hizmeti çalışıyor mu?
Evet, çalışıyor. Toolbox 'Hizmetleri Yönet' bölümündne açıp kapatabilirsiniz.

### VMD driverlarda sorun yaşanır mı?
VMD driverlar Setup alanı içine entegre edilmiştir. Herhangi bir sorun yaşanmaz. Driverları ekstradan indirip USB bellek içine atmanız gerekmez.

### Windows 11 sistem kurulumunda 'Bu bilgisayar Windows 11'i çalıştıramaz' hatası verir mi? 
Direkt olarak bypass seçeneği entegre edilmedi. Setup kısmında alt bölümde çıkan menüde Bypass logosuna basarak batch ile hazırladığım araç ile bu sorundan kurtulabilirsiniz. Rufus ile bypass'lı USB hazırlamanıza gerek yoktur. Sanal kurulumlarda da aynı şekilde bu engellemeyi bypass edebilirsiniz.

### Güncellemeler kapalı mı?
Hayır, güncellemeler kapalı değildir. Manuel moda alınmıştır. Yer yer otomatiğe alınmış şekilde davranabilir. 2050 yılına kadar ertelemek için Windows 10/11 Edit bölümünden 'Güncellemeleri 2050 yılına kadar ertele' seçeneğini kullanabilirsiniz. Bu şekilde kullanım sağlarsanız Microsoft Store gibi uygulamalarda sorun yaşamazsınız. Güncelleme hizmeti tamamen kapatılırsa sorunlar yaşanabilir.

### Güncelleme yapmalımıyız?
Evet, yapabilirsiniz. Güncelleme yaptıktan sonra bazı ayarlar bozulabilir. Bazı uygulamalar yeniden yüklenebilir. Bunları düzeltmek için Toolbox'dan 'Güncelleme Sonrası Temizlik' bölümünü çalıştırınız.

### Sistem geri yükleme kapalı mı?
Evet, kapalıdır. Sistem geri yükleme hizmeti zaman içinde fazla yer tutar ayrıca kullanıldığı zamanlarda sistemde aksamalara neden olabilir. Yeniden açmak için aşağıdaki komutları yönetici yetkili CMD ekranında uyguladıktan sonra reset atınız. Toolbox'dan açmak için 'Hizmetleri Yönet' bölümüne bakınız.
Bu bölümü açtığınızda Dosya geçmişi hizmeti, gölge kopya hizmetleri de açılacaktır. 

    • sc config SDRSVC start= demand 
    • net start SDRSVC /y
    • sc config VSS start= demand 
    • net start VSS /y
    • sc config swprv start= demand 
    • net start swprv /y
    • sc config wbengine start= demand 
    • net start wbengine /y
    • sc config fhsvc start= demand 
    • net start fhsvc /y
    • schtasks /change /TN "\Microsoft\Windows\SystemRestore\SR" /ENABLE 
    • reg add "HKLM\SOFTWARE\Policies\Microsoft\Windows NT\SystemRestore" /v "DisableConfig" /t REG_DWORD /d 0 /f
    • reg add "HKLM\SOFTWARE\Policies\Microsoft\Windows NT\SystemRestore" /v "DisableSR" /t REG_DWORD /d 0 /f

### Sysmain (hızlı getir) kapalı mı?
Evet, kapalıdır. SSD'ler için gereksiz bir hizmettir. Harddiskiniz var ve kullanmak isterseniz Toolbox'dan 'Hizmetleri Yönet' bölümüne bakınız. Komut ile açmak için aşağıdaki kodları yönetici yetkili CMD erkanına uyguladıktan sonra reset atınız.

    • sc config SysMain start=auto 
    • net start SysMain /y

### Hibernate (hızlı başlangıç) kapalı mı?
Evet, kapalıdır. Bazı durumlarda sistemin kapanmamasına yol açabiliyor. Bilgisayarın kendiliğinden açılmasına kadar bir takım hataları yer yer oluşabiliyor. Toolbox'dan 'Hizmetleri Yönet' bölümünden açabilirsiniz. Komut ile açmak için aşağıdaki kodları yönetici yetkili CMD erkanına uyguladıktan sonra güç ayarlarından aktifleştirin ve reset atın.

    • powercfg /hibernate on
    • reg add "HKLM\SYSTEM\CurrentControlSet\Control\Power" /v "HibernateEnabled" /t REG_DWORD /d 1 /f
    • reg add "HKLM\SYSTEM\CurrentControlSet\Control\Session Manager\Power" /v "HiberbootEnabled" /t REG_DWORD /d 1 /f

### Media Player kapalı mı?
Hayır, kapalı değildir.

### Internet Explorer kapalı mı?
Hayır, kapalı değildir.

### Bitlocker (Sürücü şifreleme) kapalı mı?
Evet, kapalıdır. Toolbox'dan açmak için 'Hizmetleri Yönet' bölümüne bakınız. Komut ile açmak için aşağıdaki kodları yönetici yetkili CMD erkanına uyguladıktan sonra reset atınız.

    • sc config BDESVC start= demand
    • net start BDESVC /y
    
### Sağ-tık sahiplik al ne işe yaramaktadır? Yönetici olarak çalıştırdan farkı nedir?
Bazı sistem dosyalarını düzenlemek veya silmek istediğimizde hata alırız. Bunu aşmak için öncelikle dosya yönetim yetkisini TrustedInstaller'den mevcut kullanıcıya almamız gerekir. Sahiplik al butonu bu işlemi tek tıkla yapar. Yönetici olarak çalıştırma seçeneği bu tarz sahiplik yetkilerini kapsamaz. O an için mevcut kullanıcıya en üst düzeyde yetki imkanı verir ancak bu kısıtlıdır.

### CompactOS nedir?
Sistem dosyalarını sıkıştırarak 3-4 GB'lık ek bir alan açar. Bunu uyguladıktan sonra sistem açılışı ağırlaşabilir.

### Driver hatalarında ne yapmalımıyım? Windows 10-11 için uygun driver yok, nasıl yükleyebilirim?
Uyumluluk hizmetleri kapatılmıştır. Bu tarz bir uyumsuzluk söz konusuysa Windows 7 veya Windows 8 için olan driver dosyasını yüklemeden önce sağ tık özellikler > Uyumluluk > Windows 7 veya 8 olarak değiştirdikten sonra yükleme işlemini başlatınız. Sorunsuz kurulum gerçekleştirecektir. Bunu yapmazsınız hata almanız doğaldır.

### Kurulumda hata alıyorum, nasıl çözerim?
Tüm sistemler yayınlanmadan önce 3 ayrı sistemde test edilip yükleniyor. Olası indirme hatalarına karşı ilgili sayfalarda batch ile hazırladığm HashChecker aracı bulunmaktadır. Bu araç ile ISO dosyasını kontrol edip, hatalı indirmeyi tespit edebilirsiniz. HashChecker dosyası ile ISO dosyasını ismini değiştirmeden aynı klasöre koyun. Klasör yolunda Türkçe karakter veya boşluk olmasın yoksa hata alırsınız. 
Alternatif olarak BIOS ayarlarınızı sıfırlayabilir. Uygun bir şekilde düzenlenmemiş ayarları düzeltebilirsiniz. Rufus ile cihazınıza uygun bir şekilde GPT / MBR kurulum için yapılandırmanız gerekiyor. 

### UEFI destekli cihazıma MBR kurulum yapılmış GPT kurulum yaparken hata alıyorum nasıl düzeltebilirim?
Rufus ile GPT disk biçiminde diski hazırlayın. BIOS ayarlarından UEFI aktifleştirin ve USB'den boot edip setup alanına ulaşın. Açılan ekrandan alt menüden setup alanını başlatın. Daha sonra Shift + F10 tuşlayarak CMD ekranını açın. Açılan komut ekranına sırasıyla aşağıdaki komutları girerek diski tamamen sıfırlayın. 
UYARI: Diskte yedeklenecek dosyaları farklı bir diske alın. Aşağıdaki işlemden sonra herşey silinecektir.

    • diskpart
    • list disk
      • Burada listelenecek disklerden diskinize ait olanın numarasını bulun.
    • select disk 0 (0 yazdığım yere disk numaranınızı yazacaksınız)
    • clean
    • convert gpt
    • exit
    • exit




















