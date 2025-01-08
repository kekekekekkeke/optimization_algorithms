# Dengeden Optimizasyon (EO) Algoritması Dokümantasyonu

## Giriş

Dengeden Optimizasyon (Equilibrium Optimizer - EO), kontrol hacmi kütle dengesi modelinden esinlenerek geliştirilmiş yenilikçi bir optimizasyon algoritmasıdır. Bu algoritma, denge durumu kavramını kullanarak aday çözümleri iteratif olarak iyileştirir. Bu dökümantasyon, EO algoritmasının matematiksel temellerini, çalışma prensiplerini ve uygulama detaylarını açıklamaktadır.

## Matematiksel Formülasyon

### 1. Denge Havuzu Oluşumu
Algoritma, en iyi aday çözümleri içeren bir denge havuzu tutar:

\[
C_{eq} = \{C_{eq1}, C_{eq2}, C_{eq3}, C_{eq4}, \bar{C}_{eq}\}
\]

Burada:
- \( C_{eq1}, C_{eq2}, C_{eq3}, C_{eq4} \): Uygunluk değerine göre en iyi dört aday çözüm.
- \( \bar{C}_{eq} \): Bu çözümlerin ortalaması:

\[
\bar{C}_{eq} = \frac{C_{eq1} + C_{eq2} + C_{eq3} + C_{eq4}}{4}
\]

### 2. Aday Çözümlerin Güncellenmesi
Her bir aday çözüm \( C_i \) için güncelleme denklemi:

\[
C_i = C_{eq} + (C_i - C_{eq}) \cdot F + \frac{G}{\lambda V_{max}} (1 - F)
\]

Burada:
- \( F \): Keşif ve sömürü dengesini kontrol eden üstel terim:

\[
F = a_1 \cdot \text{sign}(r - 0.5) \cdot (e^{-\lambda t} - 1)
\]

- \( G \): Aday çözümlerin üretim oranı:

\[
G = G_0 \cdot F \quad \text{burada} \quad G_0 = GCP \cdot (C_{eq} - \lambda C_i)
\]

- \( \lambda \): Stokastik davranışı kontrol eden rastgele bir vektör.
- \( V_{max} \): Parçacıkların maksimum hızı.

### 3. Yakınsama Denklemi
Yakınsama davranışı şu denklemle kontrol edilir:

\[
t = \left(1 - \frac{l}{L}\right)^{a_2 \cdot \frac{l}{L}}
\]

Burada \( l \), mevcut iterasyon sayısını, \( L \) ise maksimum iterasyon sayısını ifade eder.

## Çalışma Prensibi

1. **Başlatma**:
    - Aday çözümler rastgele olarak \([lb, ub]\) sınırları içinde başlatılır.
    - Her bir adayın uygunluk değeri değerlendirilir.

2. **Denge Havuzunun Güncellenmesi**:
    - En iyi dört aday çözüm \( C_{eq1}, C_{eq2}, C_{eq3}, C_{eq4} \) belirlenir.
    - Ortalama denge çözümü \( \bar{C}_{eq} \) hesaplanır.

3. **Aday Güncellemesi**:
    - Her aday çözüm, yukarıdaki denklemler kullanılarak güncellenir.

4. **Yakınsama Kontrolü**:
    - Maksimum iterasyon sayısına veya hedef uygunluk değerine ulaşıldığında algoritma sonlandırılır.

5. **Sonuçların Döndürülmesi**:
    - En iyi çözüm ve yakınsama eğrisi çıktılanır.

## Algoritma Uygulaması

EO algoritması Python dilinde uygulanmıştır. Uygulamanın temel yapısı aşağıdaki gibidir:

- **`EO` Fonksiyonu**:
  - Girdi: Amaç fonksiyonu `objf`, alt sınırlar `lb`, üst sınırlar `ub`, boyut `dim`, popülasyon boyutu `PopSize`, iterasyon sayısı `iters`.
  - Çıktı: En iyi çözüm, yakınsama eğrisi, çalışma süresi.

- **Temel Parametreler**:
  - \( a_1 = 2 \), \( a_2 = 1 \): Keşif ve sömürü dengesini kontrol eden sabitler.
  - \( GP = 0.5 \): Üretim olasılığı.
  - \( V_{max} = 1 \): Maksimum hız.

# EO Çalıştırma
best_solution = EO(sphere, lb, ub, dim, PopSize, iters)
print("En İyi Çözüm:", best_solution)
```

## Kaynaklar

1. Faramarzi, A., Heidarinejad, M., Stephens, B., & Mirjalili, S. (2020). "Equilibrium optimizer: A novel optimization algorithm." *Knowledge-Based Systems*, 191, 105190. DOI: [10.1016/j.knosys.2019.105190](https://doi.org/10.1016/j.knosys.2019.105190).
2. Algoritmanın MATLAB uygulaması, Afshin Faramarzi tarafından makalede sunulmuştur.

---

Bu dokümantasyon, Dengeden Optimizasyon algoritmasını, matematiksel temelini ve pratik kullanımını kapsamlı bir şekilde açıklamaktadır. Daha fazla ayrıntı için yukarıda belirtilen kaynaklara başvurabilirsiniz.

