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
CMD’yi yönetici olarak çalıştırın. Aşağıda verilen adımları sırası ile uygulayın.
> conda create -n sanalOrtamınİsmi pip python=kullanmak istediğinsürüm

<br>(Tensorflow =1.15.0 ile python=3.6 uyumlu sürümlerdir.)

` conda create -n kelebek pip python=3.6 `

> conda activate sanalOrtamınİsmi

` conda activate kelebek `

> python -m pip install --upgrade pip

> pip install tensorflow-addons[tensorflow]

> conda install tensorflow-gpu==1.15.0

> pip install tensorflow==1.15.0

> conda install -c anaconda protobuf

> python -m pip install tf_slim pywin32==225 pycocotools-windows

> python -m pip install lvis

> pip install pillow lxml cython jupyter matplotlib pandas opencv-python numpy

<br> Çevre değişkenini tanımlayalım. CMD’yi her yeniden açtığımızda bu kısmı tekrarlayalım.
> set PYTHONPATH=C:\dosyaİsmi\models;C:\dosyaİsmi\models\research;C:\dosyaİsmi\models\research\slim

` set PYTHONPATH=C:\kelebek\models;C:\kelebek\models\research;C:\kelebek\models\research\slim `

<br> Protobufları derleyelim ve setup.py dosyasını çalıştıralım.
<br> Protobuf : Gerçek ismi Protocol Buffers olan, Google’ın kendi içindeki veri iletisiminde de bolca kullandığı bir veri transfer protokolüdür. 
<br> Gerekli dizine gidelim.
> cd C:\dosyaİsmi\models\research

` cd C:\kelebek\models\research `

<br>Aşağıdaki kodu çalıştıralım.
> protoc --python_out=. .\object_detection\protos\anchor_generator.proto .\object_detection\protos\argmax_matcher.proto .\object_detection\protos\bipartite_matcher.proto .\object_detection\protos\box_coder.proto .\object_detection\protos\box_predictor.proto .\object_detection\protos\eval.proto .\object_detection\protos\faster_rcnn.proto .\object_detection\protos\faster_rcnn_box_coder.proto .\object_detection\protos\grid_anchor_generator.proto .\object_detection\protos\hyperparams.proto .\object_detection\protos\image_resizer.proto .\object_detection\protos\input_reader.proto .\object_detection\protos\losses.proto .\object_detection\protos\matcher.proto .\object_detection\protos\mean_stddev_box_coder.proto .\object_detection\protos\model.proto .\object_detection\protos\optimizer.proto .\object_detection\protos\pipeline.proto .\object_detection\protos\post_processing.proto .\object_detection\protos\preprocessor.proto .\object_detection\protos\region_similarity_calculator.proto .\object_detection\protos\square_box_coder.proto .\object_detection\protos\ssd.proto .\object_detection\protos\ssd_anchor_generator.proto .\object_detection\protos\string_int_label_map.proto .\object_detection\protos\train.proto .\object_detection\protos\keypoint_box_coder.proto


<br> Gerekli dizine gidelim.
> cd C:\dosyaİsmi\models\research\object_detection\packages\tf1

<br> Burada da dikkat etmemiz gereken kısım tenserflow 1 sürümü için olan setup.py dosyası kullanılmıştır. Eğer tensorflow 2 sürümü için kullanmak istiyorsanız tf1’i tf2 olarak değiştirin.

` cd C:\kelebek\models\research\object_detection\packages\tf1 `

Gerekli dizine gidildikten sonra setup.py dosyası için olan işlemler yapılır.

> python setup.py build

> python setup.py install


## 5. Fotoğraf Toplama ve Resimleri Etiketleme
Oluşturmak istediğiniz modeli ne üzerine eğiteceğinize karar verdikten sonraki önemli adım gerekli verileri toplamaktır. Biz bu örneğimizde kelebekleri bulan bir model eğittiğimiz için internetten çeşitli kelebekler resmi bulup indirildi. İndirdiğiniz fotoğrafların %80ini train için %20’sini test için ayırıyoruz. Resimlerin çeşitli olmasına dikkat edin. Ne kadar çok veri o kadar iyi eğitilmiş bir model.
<br>Resimleri bulduktan sonra onları etiketlememiz gerekmekte. Fotoğrafta hangi karede istediğimiz nesne var ve bu nesnenin ismi nedir gibi çeşitli bilgileri belirtmemiz lazım. Bunun için kullanacağımız uygulama ise "LabelImg".
<br> [LabelImg](https://tzutalin.github.io/labelImg/) linkten indirelim ve çıkaralım. Çıkardığımız dosyanın içerisindeki uzantısı .exe olan dosyayı çalıştırdığımızda uygulama başlayacaktır. 
> C:\dosyaİsmi\models\research\object_detection\images 

<br> dizinine gidelim ve .csv uzantılı dosyaları silelim. Train ve test dosyalarının içerisindeki verilerinde tamamını silelim. İndirdiğimiz resimleri yukarıda söylenen yüzdelere göre bir kısmını train dosyasına geri kalanını da test dosyası içerisine koyalım. Resimlerin;
> %20’sini "C:\dosyaİsmi\models\research\object_detection\images\test\"

> %80’ni "C:\dosyaİsmi\models\research\object_detection\images\train\"

<br>LabelImg uygulamasını çalıştıralım ve sol tarafta bulunan simgelerden “Open dir” seçelim ve resimlerimizin olduğu dosyaya gidelim. Gidilmesi planlanan dosya dizi: 
> C:\dosyaİsmi\models\research\object_detection\images 

<br>Resimler karşımıza gelecek ve sol tarafta “Create RectBox” simgesine tıklayalım ve nesnemizin bulunduğu alanı kare içerisine alalım. Kare içerisine aldıktan sonra ismini girelim. (İstediğiniz herhangi bir isim olabilir. Nesnenizle uyumlu olması iyi olacaktır. Save edip devam edelim. Bütün resimler için aynı işlemi yapalım.
<br>İşlemler bittiğinde test ve train dosyalarının içerisinde resimlerinizin tek tek .xml şeklinde dosyaların oluşturulduğunu göreceksiniz.
> C:\dosyaİsmi\models\research\object_detection

Dizinin içerisindeki “xml_to_csv.py” dosyasını verdiğim linkteki “xml_to_csv.py” dosyası ile değiştirin.
[Link](https://github.com/merveabd20/xml_to_csv.py)

> C:\dosyaİsmi\models\research\object_detection dizinine gidin.

` cd C:\kelebek\models\research\object_detection `

<br> Çalıştırın;
> python xml_to_csv.py  

<br>İşlem başarılı olduysa images dosyası içerisinde iki tane .csv uzantılı dosya göreceksiniz.
<br>generate_tfrecord.py dosyasını düzenleyelim. Etiket haritasını kendi haritanızla değiştirin.
Bundan;
<br>#TO-DO replace this with label map
def class_text_to_int(row_label):
    if row_label == 'nine':
        return 1
    elif row_label == 'ten':
        return 2
    elif row_label == 'jack':
        return 3
    elif row_label == 'queen':
        return 4
    elif row_label == 'king':
        return 5
    elif row_label == 'ace':
        return 6
    else:
        None
<br>Buna;
<br>#TO-DO replace this with label map
def class_text_to_int(row_label):
    if row_label == 'kelebek':
        return 1
    else:
        None

<br>Eğitilen modelimizde bir tane etiket olduğu için diğer kısımlar silindi ve etiketin ismi kendi etiket ismimiz olarak düzeltildi. Sizin kaç tane etiketiniz varsa o kadar ekleyebilirsiniz.
<br>Düzeltme işlemi yapıldıktan sonra 
> C:\dosyaİsmi\models\research\object_detection 

<br>Dizini içerisine gidip aşağıdaki kodları çalıştırıyoruz. 
` C:\kelebek\models\research\object_detection `

> python generate_tfrecord.py --csv_input=images\train_labels.csv --image_dir=images\train --output_path=train.record

> python generate_tfrecord.py --csv_input=images\test_labels.csv --image_dir=images\test --output_path=test.record

<br>Dikkat etmeniz gereken bir şey ise bu kodları sırası ile çalıştırdığınızda “Successfully created the TFRecords:…” yazısını görmelisiniz. Aksi takdirde üst kısımlarda bir hata vermişse örneğin “Windows fatal exception: access violation” gibi ve siz bunu gözden kaçırırsanız işlemlerin devamında hatalarla karşılaşabilirsiniz. Dikkat edin!

## 6. Dosya düzenleme
> C:\dosyaİsmi\models\research\object_detection\training dizinine gidin

` C:\kelebek\models\research\object_detection\training`

<br>Dizinindeki “labelmap.pbtxt” dosyayı açıp düzenleyin.
<br>Bundan;
item {
  id: 1
  name: 'nine'
}
item {
  id: 2
  name: 'ten'
}
item {
  id: 3
  name: 'jack'
}
item {
  id: 4
  name: 'queen'
}
item {
  id: 5
  name: 'king'
}
item {
  id: 6
  name: 'ace'
}

<br>Buna;
item {
  id: 1
  name: 'kelebek'
}

<br>Sizin kaç tane bulmak istediğiniz nesne varsa o kadar item silebilir / ekleyebilirsiniz.
<br> C:\dosyaİsmi\models\research\object_detection\training dizininde bulunan `“faster_rcnn_inception_v2_pets.config”` dosyasını açıp düzenleyin.

<br>**Satır 9’daki** num_classes değerini kameraya algılatmak istediğiniz nesne sayısı ile değiştirin.

`num_classes: 1`

<br>**Satır 110’daki** 
> fine_tune_checkpoint: "C:/dosyaİsmi/models/research/object_detection/faster_rcnn_inception_v2_coco_2018_01_28/model.ckpt" 

<br>Dizini kendi dizin isminize göre değiştirin.

` fine_tune_checkpoint: "C:/kelebek/models/research/object_detection/faster_rcnn_inception_v2_coco_2018_01_28/model.ckpt" `

<br>**Satır 126’daki**
> input_path: "C:/dosyaİsmi/models/research/object_detection/train.record"

<br>Dizini kendi dizin isminize göre değiştirin.

` input_path: "C:/kelebek/models/research/object_detection/train.record" `

<br>**Satır 128’deki**
> label_map_path: "C:/dosyaİsmi/models/research/object_detection/training/labelmap.pbtxt"

Dizini kendi dizin isminize göre değiştirin.

` label_map_path: "C:/kelebek/models/research/object_detection/training/labelmap.pbtxt" `

<br>**Satır 132’deki**

` num_examples: 67 `

> "C:\dosyaİsmi\models\research\object_detection\images\test"

Klasörünün içindeki resim sayısıyla değiştirin.

<br>**Satır 140’taki**
> input_path: "C:/dosyaİsmi/models/research/object_detection/test.record"

Dizini kendi dizin isminize göre değiştirin.

` input_path: "C:/kelebek/models/research/object_detection/test.record" `

<br>**Satır 142’deki** 
> label_map_path: "C:/dosyaİsmi/models/research/object_detection/training/labelmap.pbtxt"

Dizini kendi dizin isminize göre değiştirin.

` label_map_path: "C:/kelebek/models/research/object_detection/training/labelmap.pbtxt" `

<br>**Satır 116’daki**

<br>num_steps parametresi, eğitim aşamasının kaç adımda biteceğini belirtir. Bu sayı gerçekten veri kümenizin boyutuna ve bir dizi başka faktöre bağlıdır (modelin ne kadar süre çalışmasına izin vermek istediğiniz dahil). Eğitime başladığınızda, her bir eğitim adımının ne kadar sürdüğünü görmenizi ve buna göre num_steps'i ayarlamanızı öneririm.
<br>Örnek bir proje yaptığım için bu sayısı 4000 olarak ayarladım. 

`  num_steps: 4000 `
Siz kendi modelinizin işlevine göre bu sayıyı değiştirebilirsiniz.
<br>Son olarak dosyalarınızdaki değişiklikleri kaydedin ve çıkın.


## 7. Modeli Eğitme
Bu işlem süresi kartlarınızın performansına göre değişiklik gösterir. 
<br> Birkaç saat ile birkaç gün arasında.

> C:\dosyaİsmi\models\research\object_detection\legacy 

<br>Klasörünün içinde bulunan “train.py” dosyayı object_detection klasörüne kopyalayın.

<br>Belirtilen komutu "C:\dosyaİsmi\models\research\object_detection" klasörünün içinde çalıştırın:

` cd C:\kelebek\models\research\object_detection `

` python train.py --logtostderr --train_dir=training/ --pipeline_config_path=training/faster_rcnn_inception_v2_pets.config `

## 8. Modeli Çıkartma
Eğitim işlemi tamamlandığında, en son model dosyamızı oluşturmalıyız(.pb uzantılı).
<br>Aşağıdaki komutta "XXXX" değerini "C:\dosyaİsmi\models\research\object_detection\training" klasöründeki en büyük sayı ile değiştirin. 

> python export_inference_graph.py --input_type image_tensor --pipeline_config_path training/faster_rcnn_inception_v2_pets.config --trained_checkpoint_prefix training/model.ckpt-XXXX --output_directory inference_graph

<br>Daha sonra belirtilen komutu "C:\dosyaİsmi\models\research\object_detection" klasörünün içinde çalıştırın:

` cd C:\kelebek\models\research\object_detection `

` python export_inference_graph.py --input_type image_tensor --pipeline_config_path training/faster_rcnn_inception_v2_pets.config --trained_checkpoint_prefix training/model.ckpt-4000 --output_directory inference_graph `

## 9. Modeli Kullanma
Verilen bir resimdeki nesneleri tanımak istiyorsak
<br>"C:\dosyaİsmi\models\research\object_detection" klasörünün içinde yer alan "Object_detection_image.py" dosyasını çalıştırın.
<br>"Object_detection_image.py" dosyasını çalıştırmadan önce "NUM_CLASSES = tanıttığınızNesneSayısı" şeklinde düzenleyin. 

` NUM_CLASSES=1 `

<br>"C:\dosyaİsmi\models\research\object_detection" test edeceğiniz resmi bu dizine kopyalayın.
<br>IMAGE_NAME = 'test.jpg' bölümünü kendi resim dosyanızın ismi olacak şekilde düzenleyin.

` IMAGE_NAME = 't2.jpg' `

<br>Son olarak aşağıdaki komutu çalıştırın:

` python Object_detection_image.py `


## 10.Kapanış ve Sonuçlar
> conda deactivate 

<br>Yazarak kapatabilirsiniz.
