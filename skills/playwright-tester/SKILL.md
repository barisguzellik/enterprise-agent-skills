---
name: playwright-tester
description: Prepares Microsoft Playwright end-to-end test plans and scenarios with resilient selectors, flake reduction, and CI notes. Produces Turkish Playwright plans and hands off to senior-software-tester. Use for Playwright, E2E UI testing, browser automation plans, or playwright-tester.
---

# Playwright Tester

Microsoft Playwright ile UI/E2E test planları ve senaryolar hazırlar.

## Ne zaman kullanılır

- Kritik kullanıcı akışları için E2E
- UI regresyon riski
- CI’da browser test stratejisi

## Önkoşullar / girdi

- Uygulama URL / ortam, ana kullanıcı akışları
- Mevcut Playwright kurulumu (yoksa kurulum notu)
- Auth / test data stratejisi

## Adımlar

1. **Akış matrisi** — kritik path, alternatif, negatif.
2. **Selector stratejisi** — role/label/test-id; kırılgan CSS/XPath’ten kaçın.
3. **Flake azaltma** — auto-wait, network idle bilinçli kullanım, retry politikası; deterministik sinyal ([tdd-loop.md](../_shared/tdd-loop.md) ile uyumlu).
4. **Senaryo taslağı** — verilen/when/then; veri ve temizlik.
5. **CI notları** — paralel, artifact (trace/screenshot), ortam secret’ları.
6. **Handoff** → `senior-software-tester` (unit/integration ile birleştirme).

## Ortak kurallar

- [tech-stack.md](../_shared/tech-stack.md)
- [engineering-rules.md](../_shared/engineering-rules.md)
- [handoff-protocol.md](../_shared/handoff-protocol.md)
- [obsidian-session.md](../_shared/obsidian-session.md)
- [tdd-loop.md](../_shared/tdd-loop.md)

## Çıktı şablonu (Türkçe)

```markdown
# Playwright Test Planı

## Özet
## Kapsam / dışı
## Ortam ve önkoşullar
## Senaryo matrisi
| ID | Akış | Öncelik | Not |
|---|---|---|---|
## Selector ve page object yaklaşımı
## Flake / stabilite
## CI entegrasyon notları
## Örnek test iskeleti (gerekirse)
```

## Handoff (sonraki skill)

Varsayılan: **`senior-software-tester`**.

```markdown
## Handoff
- Skill: playwright-tester
- Sonraki skill: senior-software-tester
- Önerilen sonraki skill’ler: senior-software-tester
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

- Prod’da gerçek kullanıcı verisiyle yıkıcı E2E
- Sabit `waitForTimeout` ile “stabilize” etmek
- Unit test yerine yalnızca E2E ile coverage iddia etmek
