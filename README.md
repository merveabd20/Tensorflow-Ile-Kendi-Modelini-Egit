# TENSORFLOW İLE KENDİ MODELİNİ EĞİTME-ÖRNEK BİR PROJE
![This is an image](https://software.intel.com/content/dam/develop/public/us/en/images/logos/tensorflow-logo-rwd.png.rendition.intel.web.864.486.png)

Tensorflow ile kendi modelimi eğitirken yaşadığım sorunlar nedeniyle ve benim gibi kendi modelini eğitmek isteyenlere yardımcı olmak amacıyla bu yazıyı hazırladım. 
<br>Tensorflow ile kendi modelimizi eğitmeden önce Tensorflow’un kısaca ne olduğundan bahsedelim.
<br>TensorFlow, derin öğrenme destekli yapay zekâ uygulamaları üretenler için Google tarafından geliştirilmiş olan açık kaynaklı bir kütüphanedir. Esnek yapısı sayesinde, tek bir API ile platform fark etmeksizin hesaplamaları, bir veya birden fazla CPU, GPU kullanarak deploy etmenize olanak sağlar.
<br>Tensorflow, Google tarafından yıllar süren bir çalışma sonucunda oluşturulmuş, yapay zekanın derin öğrenme çalışmaları yapan geliştiriciler için üretilmiş, 2015 yılından beri kullanıcıların kullanımına açılmış açık kaynaklı bir kütüphanedir. İlk olarak sadece Python kullanılarak geliştirilmiş olan bu framework, günümüzde Pyhton’un yanında JavaScript, R, C#, C++ gibi akıllara gelebilecek en popüler yazılım dilleri tarafından desteklenmiş durumdadır. Yazılım dillerinin bu desteği TensorFlow’u herhangi bir yazılım diline hâkim olan yazılım geliştiricilerin rahat bir şekilde kullanmasına olanak sağlamaktadır. TensorFlow’un bu kadar bilinen ve kullanılan bir kütüphane olmasının da temel sebebi budur. TensorFlow, tek bir platforma hizmet eden bir kütüphane değildir. Çok çeşitli alanlar için bilgi sağlayarak geliştiricilerin kullanımına sunan bir frameworktür.
<br>Şimdi ise bir örnek proje yaparak adım adım kendi modelimizi nasıl eğiteceğimize geçelim. Bu projede makinemize kelebekleri tanıtalım 😊 Let’s go!

## 1. Microsoft Build Tools for Visual Studio İndirme
Kendi modelimi eğitmeye çalışırken karşılaştığım bir sorunda incelediğim sitelerden birinde çözüm olarak “Microsoft Build Tools for Visual Studio” indirmemizi gerektiğinden bahsedilmişti. 
<br>Sizlerde en başta bu toolsu indirerek eğitme aşamasında karşılaşılması olası bir sorundan kurtulun.
<br> “https://www.maplesoft.com/documentation_center/maplesim/Setting-Up-MSVC-Build-Tools-2019.pdf ” dokümanını inceleyerek “Microsoft Build Tools for Visual Studio” indirin. (C++ build tools indirdiğinizden emin olun.)


## 2. Anaconda Kurulumu
Anaconda; veri bilimi ve bu alandaki benzer diğer bilişsel uygulamalar için kullanılan ortam yöneticisidir. İçeriğinde 1500’den fazla açık kaynak paket yer almaktadır. 
<br>Google “anaconda download” yazıp indirin. Kurulum dosyasını açın ve basit olan kurulumu (Next → Next → Setup :))tamamlayın.

## 3. Gerekli Dosyaların İndirilmesi ve Diğer İşlemler
Bu adımda sanal ortamda projeyi oluşturup diğer adımlara geçeceğiz. Bu sanal ortam neden gerekli diye düşünebilirsiniz? Önce sanal ortamın ne olduğuna dair bir tanım yapalım.
<br>Virual Environment (sanal ortam), projelerimizde gerekli olan paketleri, sistemden bağımsız bir şekilde kurup, kullanmamızı olanak sağlayan bir yapıdır. 
<br>Neden sanal ortam üzerine projemizi oluşturuyoruz sorusuna gelirsek. Örneğin daha önceden tensorflow ile bir proje geliştirmiş olalım. Daha sonraki günlerde yine tensorflow ile başka bir proje geliştirmek isteyelim. Tensorflow ve tensorflowu kullanmamız için gerekli olan kütüphaneler sürekli güncellenmekte. Ama önemli bir sorun ise bir sürümün diğer güncel sürümle çalışmıyor olması, yani birbirlerine uyumsuzlar. Bir önceki projede kullandığınız sürümler bir sonraki projenizde aynı olmayabilir. Bu durumda sürümleri güncellediğinizde yeni oluşturacağınız proje çalışacaktır fakat eski projenin birbirine uyumlu sürümlerini değişmiş olacaksınız. Böylece çalışan projeniz artık çalışmayacak. Böyle bir durum yaşamamak için çözüm yollarından biri sanal ortam kullanmaktır. Her projeyi bir sanal ortam üzerine kurup o sanal ortam üzerine gerekli kütüphaneleri yükleriz böylece biri diğerine karışmamış olur. Birinde sürümleri güncellerken diğerinde sürümler aynı kalacaktır. Çünkü oluşturulan sanal ortamlar birbirinden bağımsız olacak ve bir sorun teşkil etmeyecek.


#### 3.1. Tensorflow Models Dosyasının İndirilmesi
[Tensorflow Model](https://github.com/tensorflow/models) linkten modeli indirelim.<br> Yeni bir dosya oluşturalım. Dosya ile sanal ortamın ismi aynı olsun. Yeni dosyamızın içerisine yeni bir dosya oluşturup ismini models yapalım ve bu dosyanın içerisine indirdiğimiz model dosyasını çıkaralım. 
<br>Oluşturulan dosya dizini şu şekilde olmalı: 
> dosyaİsmi/models/indirilenModeldosyaları
<br> ` C:\kelebek\models`


#### 3.2. Edje Electronics Repository İndirilmesi
[Edje Electronics repository](https://codeload.github.com/EdjeElectronics/TensorFlow-Object-Detection-API-Tutorial-Train-Multiple-Objects-Windows-10/zip/master) linkten dosyaları indirelim.
> C:\dosyaİsmi\models\research\object_detection 
dizinine indirdiğimiz dosyaları çıkaralım.


#### 3.3. Faster-RCNN-Inception-V2-COCO İndirilmesi
Burada dikkat etmemiz gereken şey kullandığımız Tensorflow’un sürümüdür. Aşağıda verilen link Tensorflow 1 sürümleri için geçerlidir. Eğer siz 2 sürümünü kullanıyorsanız uygun bir modeli indirin!
<br>[faster_rcnn_inception_v2_coco](https://github.com/tensorflow/models/blob/master/research/object_detection/g3doc/tf1_detection_zoo.md) modelini TensorFlow'un model zoo kısmından indirelim.


## 4. CMD Üzerinden Gerekli Kütüphanelerin Kurulması
> CMD’yi yönetici olarak çalıştırın. Aşağıda verilen adımları sırası ile uygulayın.
<br> ` conda create -n sanalOrtamınİsmi pip python=kullanmak istediğinsürüm `
(Tensorflow =1.15.0 ile python=3.6 uyumlu sürümlerdir.)
> conda create -n kelebek pip python=3.6
> conda activate sanalOrtamınİsmi
> conda activate kelebek

python -m pip install --upgrade pip
pip install tensorflow-addons[tensorflow]
conda install tensorflow-gpu==1.15.0
pip install tensorflow==1.15.0
conda install -c anaconda protobuf
python -m pip install tf_slim pywin32==225 pycocotools-windows



## 5. Fotoğraf Toplama ve Resimleri Etiketleme
## 6. Modeli Eğitme
## 7. Modeli Çıkartma
## 8. Modeli Kullanma
## 9.Kapanış ve Sonuçlar
