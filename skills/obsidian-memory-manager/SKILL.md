---
name: obsidian-memory-manager
description: Creates and maintains local Obsidian-compatible Markdown memory including GLOSSARY, ADR decisions, and pipeline artifacts with wikilinks. Produces Turkish memory notes and can feed context back into the SDLC pipeline. Use for Obsidian vault memory, glossary, ADRs, or obsidian-memory-manager.
---

# Obsidian Memory Manager

Obsidian uyumlu MD formatında yerel bellek oluşturur. Pipeline artefaktlarını, glossary ve ADR’leri kalıcı notlara çevirir.

## Ne zaman kullanılır

- Proje kararları, handoff’lar, release notlarını vault’a yazmak
- `GLOSSARY.md` / ADR eşdeğerini vault’ta tutmak
- Agent’lar arası kalıcı bağlam; kullanıcı belirli bir dizin verdiğinde

## Önkoşullar / girdi

- **Hedef dizin** (zorunlu; yoksa sor)
- Yazılacak içerik (plan, review, deploy özeti, terimler, kararlar)
- Varsa mevcut vault yapısı; [ubiquitous-language.md](../_shared/ubiquitous-language.md)

## Adımlar

1. **Dizini doğrula** — yoksa oluştur (kullanıcı onayıyla); Obsidian vault kökü netleştir.
2. **Hiyerarşi** — örn. `memory/projects/<proje>/`, `memory/handoffs/`, `memory/decisions/`, `memory/glossary.md`.
3. **Glossary** — yeni/değişen terimleri [ubiquitous-language.md](../_shared/ubiquitous-language.md) şablonuna göre yaz veya güncelle.
4. **ADR / karar** — zor kararları `memory/decisions/` altına ADR şablonuyla kaydet.
5. **Pipeline notu** — handoff özetlerini path referansıyla kaydet; içeriği gereksiz kopyalama.
6. **Wikilink + index** — `[[ilgili-not]]`; `MOC` / `index.md` güncelle.
7. **Handoff** — pipeline’a dönüş (`analyst-planner` vb.) veya tamamlandı.

## Ortak kurallar

- [tech-stack.md](../_shared/tech-stack.md)
- [engineering-rules.md](../_shared/engineering-rules.md)
- [handoff-protocol.md](../_shared/handoff-protocol.md)
- [obsidian-session.md](../_shared/obsidian-session.md)
- [ubiquitous-language.md](../_shared/ubiquitous-language.md)

## Çıktı şablonu (Türkçe)

Not dosyası örneği:

```markdown
---
tags: [sdlc, handoff]
skill: <kaynak-skill>
date: YYYY-MM-DD
---

# <Başlık>

## Özet
## İçerik
## Bağlantılar
- [[ilgili-not]]
## Kaynak skill / pipeline
```

İş raporu:

```markdown
# Obsidian Memory İşlemi

## Hedef dizin
## Oluşturulan / güncellenen dosyalar
## Glossary / ADR güncellemeleri
## Wikilink’ler
## Index güncelliği
```

## Handoff (sonraki skill)

Varsayılan: **pipeline’a geri** (`analyst-planner` veya ilgili skill) veya **tamamlandı**.

```markdown
## Handoff
- Skill: obsidian-memory-manager
- Sonraki skill: analyst-planner
- Önerilen sonraki skill’ler: analyst-planner
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

Bu skill oturum devam ettiricidir. Girdi handoff’undaki `Obsidian oturum dizini` ve vault bilgisini aynen kullan; yeni oturum oluşturma. Handoff bloğunu taslakla, sıradaki `NN-<skill-name>.md` notunu ve `index.md` wikilink satırını oluştur/güncelle, Obsidian alanlarını doldur ve ancak kayıt tamamlandıktan sonra handoff’u sun. Gerekli oturum/vault bilgisi yoksa tahmin ederek yazma; başlatıcı protokolünün vault çözümlemesini uygula veya kullanıcıdan eksik yolu iste.

Notta Türkçe çıktı özeti ile handoff bloğunu tut; secret/PII’yi redact et. Bu otomatik kayıt için `obsidian-memory-manager` çağırma. Ayrıntılı biçim ve sıra: [obsidian-session.md](../_shared/obsidian-session.md).

## Yapılmayacaklar

- Secret / ham PII / kart verisini vault’a yazmak
- Kullanıcının dizini dışında rastgele yazmak
- Mevcut notları onaysız silmek
