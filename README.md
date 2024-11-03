Ses Verisi ile Harf Tanıma Modeli
Bu proje, ses verisi kullanarak Türk alfabesindeki harfleri tanıyabilen bir yapay zeka modelidir. Model, konuşulan harfleri tanıyabilmek için MFCC (Mel-frekans kepstrum katsayıları) özellik çıkarımı kullanılarak eğitilmiştir. Veri çeşitliliğini artırarak modeli daha başarılı hale getirmek amacıyla veri çoğaltma teknikleri kullanılmıştır. Model, TensorFlow ile oluşturulmuş olup .h5 ve TensorFlow Lite .tflite formatlarında kaydedilmiştir, bu sayede flutter yazlım dilinde kullanılabilmektedir.
Proje Yapısı

Veri Yolu: /content/drive/MyDrive/alfabeses2/
Her bir harf etiketi için alt klasörler içerir (A-Z), bu alt klasörlerde ise konuşulmuş harflerin .wav veya .mp3 formatında kayıtları bulunmaktadır.

Model Çıktıları:
model.h5: Eğitilmiş Keras modeli, daha sonra kullanılmak üzere kaydedildi.
model.tflite: TensorFlow Lite formatında dönüştürülmüş model.
labels.txt: Modelde kullanılan harf etiketlerinin listesi.

Veri Kümesi
Toplam Örnek Sayısı: Yaklaşık 1,800 ses dosyası.
Etiketler: 29 adet farklı sınıf, Türk alfabesindeki harfleri temsil etmektedir.

Veri Çoğaltma:
Zaman esnetme: Sesin hızını artırıp veya azaltarak farklı varyasyonlar oluşturulmaktadır.
Gürültü ekleme: Rastgele gürültü eklenerek gerçek dünyadaki ses çeşitliliği simüle edilmektedir.
Model Mimarisi
Model, ileri beslemeli sinir ağı (feedforward neural network) mimarisi kullanılarak MFCC özelliklerini işlemek ve harfleri tanımak amacıyla tasarlanmıştır:

Girdi Katmanı: 40 boyutunda MFCC özelliklerini alır.

Ara Katmanlar:
256 birimlik yoğun (dense) katman (ReLU aktivasyonu), Batch Normalizasyon ve Dropout.
128 birimlik yoğun katman (ReLU aktivasyonu), Batch Normalizasyon ve Dropout.

Çıkış Katmanı: Her harfi temsil eden 29 birimli Softmax katmanı.

Eğitim
Optimizasyon Yöntemi: Adam

Kayıp Fonksiyonu: Sparse Categorical Crossentropy
Batch Boyutu: 16
Erken Durdurma: Doğrulama kaybı art arda 5 epoch boyunca iyileşmediğinde eğitimi durdurur.
Özellik Çıkarma
MFCC (Mel-frekans kepstrum katsayıları) kullanılarak ses verisi, modelin daha iyi yorumlayabileceği bir özellik setine dönüştürülür. MFCC’lerin ortalaması hesaplanarak modelin giriş özellikleri olarak kullanılır.

Veri Çoğaltma
augment_data fonksiyonu her bir ses dosyası için üç yeni varyasyon oluşturur:

Zaman esnetme:
