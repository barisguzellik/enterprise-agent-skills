# Ortak Yazılım Geliştirme Kuralları

Tüm skill’ler bu kurallara uyar. Çelişki varsa güvenlik ve uyumluluk önceliklidir.

## SDLC

- Güncel SDLC akışına uy: analiz → plan → geliştirme → mimari review → test → güvenlik → diff kontrol → release → deploy.
- Her aşama bir sonraki skill için Türkçe, uygulanabilir handoff üretir ([handoff-protocol.md](handoff-protocol.md)).
- Kapsam dışı iş yapılmaz; varsayımlar handoff’ta listelenir.
- Plan öncesi hizalama: [grilling.md](grilling.md). Paylaşılan dil: [ubiquitous-language.md](ubiquitous-language.md).

## Mimari seçim

Gerekli yerde şu seçimlerden biri gerekçeyle yapılır:

| Seçenek | Ne zaman |
|---|---|
| **Monolith** | Küçük ekip/kapsam, tek deploy birimi yeterli, sınırlar henüz net değil |
| **Modular monolith** | Modül sınırları net, tek process/deploy tercih, ileride ayrışma ihtimali |
| **Microservice** | Bağımsız ölçek/deploy, net bounded context, ayrı veri sahipliği, operasyon olgunluğu |

Dağıtık sistemlerde: timeout, retry/backoff, idempotency, circuit breaker, outbox/inbox, eventual consistency ve gözlemlenebilirlik (log/metric/trace) planlanır.

## Tasarım ve kod kalitesi

- **SOLID** ilkelerine uy.
- **Deep module**: küçük/basit arayüz arkasında zengin davranış; sığ “geçiş” modüllerinden kaçın.
- **Async programming** I/O ve dış bağımlılıklarda doğru kullanılır; thread-block ve fire-and-forget kötüye kullanımı engellenir.
- Sistemler **decouple** edilir: net arayüzler, event/mesaj sınırları, paylaşılan DB anti-pattern’inden kaçınma.
- **Sonar** kuralları ve code smell’ler dikkate alınır; yeni kod kalite kapısını düşürmez.
- İsimlendirme ve domain dili [ubiquitous-language.md](ubiquitous-language.md) ile hizalıdır (`GLOSSARY.md` varsa oku).

## Feedback loop

- Ajan kör uçmaz: typecheck, otomatik test, gerekiyorsa browser/API sinyali.
- Yeni davranış için [tdd-loop.md](tdd-loop.md) tercih edilir.
- Zor bug’larda [bug-diagnosis-loop.md](bug-diagnosis-loop.md); kırmızı loop olmadan spekülatif fix yok.

## Güvenlik (her zaman ön planda)

- Secure by default: least privilege, input validation, output encoding, güvenli authN/authZ.
- Secret’lar Vault/secret store’da; repo, log ve client bundle’da secret yok.
- Tehdit modeli: injection, XSS, CSRF, IDOR, broken access control, insecure deserialization, dependency risk.
- Veri ve sistem güvenliği, zafiyet riskleri her plan ve review’da değerlendirilir.

## Uyumluluk ve veri koruma

İlgili olduğunda risk ve kontroller açıkça not edilir:

- **GDPR**
- **KVKK**
- **PCI-DSS** (ödeme/kart verisi varsa)

PII/PCI verisi için minimizasyon, maskeleme, şifreleme, saklama süresi ve erişim denetimi planlanır.

## Test ve doğrulama

- Kritik yollar unit + integration ile korunur.
- Değişiklikle gelen davranış için test eklenmeden “tamam” sayılmaz.
- Güvenlik ve uyumluluk bulguları severity ile raporlanır; kritik bulgu varken release önerilmez.

## Operasyon

- Deploy planı: health check, rollback, migration sırası, feature flag, metrik (Prometheus) içerir.
- Breaking change ve geriye dönük uyumluluk handoff’ta belirtilir.
