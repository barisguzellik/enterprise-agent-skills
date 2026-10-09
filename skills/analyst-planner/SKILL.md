---
name: analyst-planner
description: Analyzes software tasks or projects and produces a Turkish development plan with architecture choice, tech-stack fit, security/compliance notes, and a handoff for senior-software-engineer. Use at the start of a project or task, or when the user asks for analysis, planning, SDLC plan, grilling, or analyst-planner.
---

# Analyst Planner

Projeye veya göreve başlamadan önce grilling ile hizalanır, gereksinimleri ayrıştırır, geliştirme planı hazırlar ve `senior-software-engineer` için handoff üretir.

## Ne zaman kullanılır

- Yeni proje / epic / feature başlangıcı
- Kullanıcı “plan”, “analiz”, “SDLC planı”, “analyst-planner” istediğinde
- Mimari seçim (monolith / modular monolith / microservice) netleştirilmeden kod yazılmamalıysa

## Önkoşullar / girdi

- İş ihtiyacı, kabul kriterleri veya problem tanımı (eksikse varsayımları açık yaz)
- Varsa mevcut repo, kısıtlar, deadline, uyumluluk gereksinimleri
- Varsa `GLOSSARY.md`, ADR’ler, Obsidian memory veya DBA notları

## Adımlar

1. **Glossary oku** — varsa [ubiquitous-language.md](../_shared/ubiquitous-language.md); terimleri planda kullan.
2. **Grilling turu** — [grilling.md](../_shared/grilling.md); kritik dallar kapanmadan planı `tamamlandı` sayma.
3. **Bağlam topla** — hedef, kullanıcılar, başarı ölçütü, kısıtlar, mevcut sistem.
4. **Gereksinimleri ayır** — fonksiyonel / non-fonksiyonel; belirsizlikleri listele.
5. **Mimari seç** — monolith, modular monolith veya microservice; gerekçeyi yaz. Dağıtık ise timeout, idempotency, tutarlılık modelini not et.
6. **Tech-stack eşle** — [tech-stack.md](../_shared/tech-stack.md) içinden seç; sapma varsa gerekçe yaz.
7. **Güvenlik ve uyumluluk** — tehditler, veri sınıflandırması, GDPR/KVKK/PCI-DSS ([engineering-rules.md](../_shared/engineering-rules.md)).
8. **İş kırılımı** — uygulanabilir görevler, bağımlılıklar, sıra, test/güvenlik kapıları; TDD seam notu ([tdd-loop.md](../_shared/tdd-loop.md)).
9. **Glossary / ADR** — yeni terim veya karar varsa güncelleme notu veya `obsidian-memory-manager` öner.
10. **Handoff** — [handoff-protocol.md](../_shared/handoff-protocol.md); sonraki skill: `senior-software-engineer`.

## Ortak kurallar

- [tech-stack.md](../_shared/tech-stack.md)
- [engineering-rules.md](../_shared/engineering-rules.md)
- [handoff-protocol.md](../_shared/handoff-protocol.md)
- [obsidian-session.md](../_shared/obsidian-session.md)
- [grilling.md](../_shared/grilling.md)
- [ubiquitous-language.md](../_shared/ubiquitous-language.md)

## Çıktı şablonu (Türkçe)

```markdown
# Geliştirme Planı

## Özet
## Grilling özeti
## Problem / hedef
## Kabul kriterleri
## Varsayımlar
## Mimari karar
- Seçim: monolith | modular monolith | microservice
- Gerekçe:
- Bounded context / modül sınırları:
- Veri sahipliği:
## Teknoloji seçimleri
## Glossary / ADR notları
## Güvenlik ve uyumluluk
## İş kırılımı (sıralı)
1. ...
## Test stratejisi (üst seviye / TDD seam’leri)
## Operasyon notları (deploy / gözlemlenebilirlik)
## Riskler
## Açık sorular
```

## Handoff (sonraki skill)

Varsayılan sonraki skill: **`senior-software-engineer`**.

DB şema/migration belirsizse `database-dba` öner. UI E2E ihtiyacı yüksekse `playwright-tester` notu bırak. Kritik grilling dalı açıksa durum `kısmi` veya `engellendi`.

```markdown
## Handoff
- Skill: analyst-planner
- Sonraki skill: senior-software-engineer
- Önerilen sonraki skill’ler: senior-software-engineer
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

- Kod yazmak, PR açmak, deploy etmek
- Belirsizliği gizleyerek “hazır plan” sunmak
- Grilling atlayıp engineer’a geçmek
- Güvenlik/uyumluluk değerlendirmesini atlamak
