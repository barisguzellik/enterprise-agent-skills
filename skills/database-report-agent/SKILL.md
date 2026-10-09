---
name: database-report-agent
description: Prepares safe, preferably read-only parameterized queries and report outlines for a requested database, with PII masking and explicit approval before execution. Produces Turkish query readiness notes and may hand off to obsidian-memory-manager. Use for DB reports, analytics queries, or database-report-agent.
---

# Database Report Agent

İstenen DB üzerinde rapor/sorgu için hazırlık yapar. Varsayılan: salt-okuma, parametreli sorgu, PII maskeleme.

## Ne zaman kullanılır

- Rapor, analytics, ad-hoc sorgu ihtiyacı
- “Şu DB’den X metriklerini çek” talepleri
- DBA şema işi değil; sorgu hazırlığı

## Önkoşullar / girdi

- Hedef DB / şema bilgisi
- Rapor sorusu (ne ölçülecek)
- Ortam (prod ise ekstra dikkat + onay)

## Adımlar

1. **İhtiyacı netleştir** — kolonlar, filtreler, zaman aralığı, agregasyon.
2. **Salt-okuma öncelik** — SELECT; DML/DDL isteklerinde açık uyarı ve onay.
3. **Parametreli sorgu** — injection riski yok; limit/pagination.
4. **PII / uyumluluk** — maskeleme, minimizasyon, GDPR/KVKK/PCI-DSS.
5. **Performans** — açıklama planı notu; full scan uyarısı.
6. **Çalıştırma** — yalnızca kullanıcı onayı sonrası; sonucu özetle.
7. **Handoff** → kullanıcı veya `obsidian-memory-manager`.

## Ortak kurallar

- [tech-stack.md](../_shared/tech-stack.md)
- [engineering-rules.md](../_shared/engineering-rules.md)
- [handoff-protocol.md](../_shared/handoff-protocol.md)
- [obsidian-session.md](../_shared/obsidian-session.md)

## Çıktı şablonu (Türkçe)

```markdown
# Sorgu / Rapor Hazırlığı

## Amaç
## Ortam / DB
## Varsayımlar
## Önerilen sorgu (parametreli)
## PII / maskeleme
## Performans notları
## Çalıştırma onayı: gerekli | alındı
## Örnek çıktı şeması
```

## Handoff (sonraki skill)

Varsayılan: **kullanıcı** veya **`obsidian-memory-manager`**.

```markdown
## Handoff
- Skill: database-report-agent
- Sonraki skill: obsidian-memory-manager
- Önerilen sonraki skill’ler: obsidian-memory-manager
- Durum: tamamlandı | engellendi | kısmi
- Özet:
- Üretilen artefaktlar:
- Kararlar / kısıtlar:
- Riskler (güvenlik, uyumluluk, performans):
- Açık sorular:
- Obsidian vault:
- Obsidian oturum dizini:
- Obsidian not:
- Sonraki skill için giriş:
```

## Handoff öncesi Obsidian kaydı

Bu skill oturum başlatıcıdır. Girdi handoff’unda `Obsidian oturum dizini` varsa aynı oturuma devam et; yoksa `obsidian-session.md` öncelik sırasıyla vault kökünü çöz ve yeni `memory/sessions/YYYY-MM-DD-<kisa-slug>/` oturumu aç. Açık vault yolu ve `OBSIDIAN_VAULT_PATH` yoksa kullanıcıdan hedef vault yolunu iste; rastgele dizine yazma. Handoff bloğunu taslakla, sıradaki `NN-<skill-name>.md` notunu ve `index.md` wikilink satırını oluştur/güncelle, Obsidian alanlarını doldur ve ancak kayıt tamamlandıktan sonra handoff’u sun.

Notta Türkçe çıktı özeti ile handoff bloğunu tut; secret/PII’yi redact et. Bu otomatik kayıt için `obsidian-memory-manager` çağırma. Ayrıntılı biçim ve sıra: [obsidian-session.md](../_shared/obsidian-session.md).

## Yapılmayacaklar

- Onaysız prod’da yıkıcı SQL (UPDATE/DELETE/DROP/TRUNCATE)
- Ham PII’yi log/rapora dökmek
- Şema migration tasarlamak (`database-dba`)
