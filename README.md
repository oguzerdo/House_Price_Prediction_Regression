# House Price Prediction with Regression Models

<a href="https://www.oguzerdogan.com/">
    <img src="https://www.oguzerdogan.com/wp-content/uploads/2020/10/logo_oz.png" width="200" align="right"></a>



![banner](https://storage.googleapis.com/kaggle-competitions/kaggle/5407/media/housesbanner.png)



Bu proje ilk ciddi projemdi. Birçok tekniği denemek ve bilgimi güçlendirmek için mükemmel bir deneyim oldu. Üzerinde oldukça fazla araştırma yaptım ve sonucunda meyvesini Kaggle üzerindeki yarışmada top %1e girerek aldım. Çalışma başta İngilizce olarak hazırlanmış olup sonrasında bu çalışma ile ilgili çok fazla Türkçe kaynak olmaması sebebiyle Türkçe olarak paylaşılmıştır. 

Notebooktaki nihai amacımız Ames Lowa’daki konut evlerini neredeyse her açıdan tanımlayan 79 açıklayıcı değişken ile beraberindeki 1459 adet evin fiyatını minimum hata ile tahmin etmek.

Çalışmanın başında ExtraTreeRegressor ile bir base model kurup en iyi sayısal ve kategorik değişkenleri ayrı ayrı inceledim.

Çok fazla değişken olmasından dolayı değişkenler üzerinde aşağıdaki gibi bir excel sheet oluşturup python ve bu tablo ile eş zamanlı olarak değişken analizlerini yürüttüm. Image dosyasına tıklayarak Excel Sheeti inceleyebilirsiniz.

<a href="https://docs.google.com/spreadsheets/d/1P67BXoVlt8EIzFTtcENCCt5dABRdV4DqNRIIvbbYOrg/">
    <img src="https://www.oguzerdogan.com/wp-content/uploads/2020/11/aciklamalar.jpg">
</a>

**NA Value:** Veri setinde o özelliğe sahip olmayan değişkenlerin boş bırakıldığını gözlemledim. (örneğin havuzu olmayan evlerin pool değişkeninde boş bırakılması) ve bunlara 0 değerleri atadım. Bu tarzda olmayan diğer değişkenlere ise çeşitli kırılımlara göre atamalar yaptım.

**Outliers:**  Grafiklerde gözüme çarpan ve aykırı olduğunu düşündüğüm değerleri çıkarttım. ( skorumu en çok arttıran bu adım oldu)

**Box-Cox Dönüşümü** : Bazı sayısal değişkenler çok fazla sağa çarpık olduğu için ve regresyon modelleri üzerinden çalıştığım için box-cox dönüşümü uyguladım.

**Log Dönüşümü:** Target değişken `Sale Price` simetrik olmadığından ve regresyon modelleri üzerinde çalıştığımdan log transform uyguladım ve dönüşüm sonrası hedef değişkenin artık daha simetrik dağıldığını gözlemledim.

**RobustScaler:** Robust scalerın regresyon modellerinde outlierlara karşı güzel sonuçlar verdiğini okudum ve bunu denemek istedim. Çok fazla skor artışı olmasa da skora etkisi olduğunu söyleyebilirim.

**Modeller:** Log dönüşümden dolayı hatayı net olarak görmek mümkün olmadı, bunun için log dönüşüm olmadan da base modeller üzerinde bir test yaptım ve CatBoost ile 17.311 gibi bir RMSE skoru aldım. Diğer detaylı sonuçlara proje notebookundan bakabilirsiniz.

**Submission:** Araştırmalarıma göre yarışmaya katılanlar Blending Models kullanarak skorlarını daha da güzel almışlardı ve bunu denemek istedim. Ağırlıklarını belirleyerek modellerin karışımlarından oluşan bir submission hazırladım. Ve sonucunda Kaggle üzerinden top %1’e ulaştım.

---

# Öznitelikler

**Veri kümesindeki her özelliğin kısaca açıklaması söyledir:**

- SalePrice - mülkün dolar cinsinden satış fiyatı. Bu, tahmin etmeye çalışılan hedef değişkendir.
- MSSubClass: İnşaat sınıfı
- MSZoning: Genel imar sınıflandırması
- LotFrontage: Mülkiyetin cadde ile doğrudan bağlantısının olup olmaması
- LotArea: Parsel büyüklüğü
- Street: Yol erişiminin tipi
- Alley: Sokak girişi tipi
- LotShape: Mülkün genel şekli
- LandContour: Mülkün düzlüğü
- Utulities: Mevcut hizmetlerin türü
- LotConfig: Parsel yapılandırması
- LandSlope: Mülkün eğimi
- Neighborhood: Ames şehir sınırları içindeki fiziksel konumu
- Condition1: Ana yol veya tren yoluna yakınlık
- Condition2: Ana yola veya demiryoluna yakınlık (eğer ikinci bir yer varsa)
- BldgType: Konut tipi
- HouseStyle: Konut sitili
- OverallQual: Genel malzeme ve bitiş kalitesi
- OverallCond: Genel durum değerlendirmesi
- YearBuilt: Orijinal yapım tarihi
- YearRemodAdd: Yeniden düzenleme tarihi
- RoofStyle: Çatı tipi
- RoofMatl: Çatı malzemesi
- Exterior1st: Evdeki dış kaplama
- Exterior2nd: Evdeki dış kaplama (birden fazla malzeme varsa)
- MasVnrType: Duvar kaplama türü
- MasVnrArea: Kare ayaklı duvar kaplama alanı
- ExterQual: Dış malzeme kalitesi
- ExterCond: Malzemenin dışta mevcut durumu
- Foundation: Vakıf tipi
- BsmtQual: Bodrumun yüksekliği
- BsmtCond: Bodrum katının genel durumu
- BsmtExposure: Yürüyüş veya bahçe katı bodrum duvarları
- BsmtFinType1: Bodrum bitmiş alanının kalitesi
- BsmtFinSF1: Tip 1 bitmiş alanın metre karesi
- BsmtFinType2: İkinci bitmiş alanın kalitesi (varsa)
- BsmtFinSF2: Tip 2 bitmiş alanın metre karesi
- BsmtUnfSF: Bodrumun bitmemiş alanın metre karesi
- TotalBsmtSF: Bodrum alanının toplam metre karesi
- Heating: Isıtma tipi
- HeatingQC: Isıtma kalitesi ve durumu
- CentralAir: Merkezi klima
- Electrical: elektrik sistemi
- 1stFlrSF: Birinci Kat metre kare alanı
- 2ndFlrSF: İkinci kat metre kare alanı
- LowQualFinSF: Düşük kaliteli bitmiş alanlar (tüm katlar)
- GrLivArea: Üstü (zemin) oturma alanı metre karesi
- BsmtFullBath: Bodrum katındaki tam banyolar
- BsmtHalfBath: Bodrum katındaki yarım banyolar
- FullBath: Üst katlardaki tam banyolar
- HalfBath: Üst katlardaki yarım banyolar
- BedroomAbvGr: Bodrum seviyesinin üstünde yatak odası sayısı
- KitchenAbvGr: Bodrum seviyesinin üstünde mutfak Sayısı
- KitchenQual: Mutfak kalitesi
- TotRmsAbvGrd: Üst katlardaki toplam oda (banyo içermez)
- Functional: Ev işlevselliği değerlendirmesi
- Fireplaces: Şömineler
- FireplaceQu: Şömine kalitesi
- Garage Türü: Garaj yeri
- GarageYrBlt: Garajın yapım yılı
- GarageFinish: Garajın iç yüzeyi
- GarageCars: Araç kapasitesi
- GarageArea: Garajın alanı
- GarageQual: Garaj kalitesi
- GarageCond: Garaj durumu
- PavedDrive: Garajla yol arasındaki yol
- WoodDeckSF: Ayaklı ahşap güverte alanı
- OpenPorchSF: Kapı önündeki açık veranda alanı
- EnclosedPorch: Kapı önündeki kapalı veranda alan
- 3SsPorch: Üç mevsim veranda alanı
- ScreenPorch: Veranda örtü alanı
- PoolArea: Havuzun metre kare alanı
- PoolQC: Havuz kalitesi
- Fence: Çit kalitesi
- MiscFeature: Diğer kategorilerde bulunmayan özellikler
- MiscVal: Çeşitli özelliklerin değeri
- MoSold: Satıldığı ay
- YrSold: Satıldığı yıl
- SaleType: Satış Türü
- SaleCondition: Satış Durumu

# Dosyalar

- *datasets/train.csv* - Training set
- *datasets/test.csv* - Test set
- *datasets/data_description.txt* - Full Description of each column
- *house-pricing-project-regression-models.ipynb* - Project Notebook

## Libraries Used

```
pandas
numpy
matplotlib
sklearn
scipy
pickle
catboost
lightgbm 
xgboost
mlxtend.regressor # This is for stacking part, works well with sklearn and others...
```

## Author

- Oğuz Han Erdoğan - [oguzerdo](https://github.com/oguzerdo)
