# TDD Döngüsü

Amaç: kör kod yazmak yerine kırmızı sinyal → düzeltme → sadeleştirme ile dikey dilim ilerlemek.

## Döngü

1. **Red** — doğru seam’de başarısız test (kullanıcı semptomunu veya kabul kriterini yakalar).
2. **Green** — testi geçiren en küçük değişiklik.
3. **Refactor** — davranış aynı kalırken tasarımı sadeleştir; testler yeşil kalsın.

Bir dilim bitmeden sonraki dilime geçme.

## Seam seçimi

- Test, **gerçek çağrı düzenini** yansıtan seam’de olmalı.
- Yanlış seam (çok sığ unit, bug zincirini yakalamayan mock denizi) → false confidence; not düş ve doğru seam ara.
- Doğru seam yoksa bunu bulgu olarak yaz (mimari engel); yine de mümkün olan en yakın kırmızı sinyal kur.

## İyi / kötü sinyal

| İyi | Kötü |
|---|---|
| Belirli semptom / kabul kriteri assert | “Çökmedi” assert |
| Hızlı, deterministik | Flaky sleep / rastgele sıra |
| Tek davranış odaklı | God test |
| Glossary terimleriyle isim | Belirsiz `test1` |

## Ajan çalışma ritmi

- Sık: typecheck + ilgili tek test dosyası.
- Dilim sonunda: ilgili suite.
- İş bitiminde (engineer/tester): mümkünse full suite bir kez.

Ayrıntılı E2E için `playwright-tester`; birim/entegrasyon boşlukları için `senior-software-tester`.
