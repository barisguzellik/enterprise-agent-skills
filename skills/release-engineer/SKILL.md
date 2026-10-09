---
name: release-engineer
description: Prepares a Turkish release plan from ready code plus test and security results, including changelog, semver/risk, migration order, feature flags, and rollback criteria. Hands off to deployment-engineer. Use for release planning, versioning, changelog, or release-engineer.
---

# Release Engineer

Geliştirme, test ve güvenlik sonuçlarına göre release planı hazırlar.

## Ne zaman kullanılır

- `git-diff-checker` sonrası release’e uygun değişiklikler
- Sürüm notu, semver, migration sırası ihtiyacı

## Önkoşullar / girdi

- Diff checker handoff’u (release uygun)
- Test + güvenlik özetleri
- Mevcut sürüm / changelog convention

## Adımlar

1. **Değişiklikleri sınıfla** — feature / fix / breaking / security / chore.
2. **Semver öner** — major / minor / patch gerekçesi.
3. **Changelog** — kullanıcı ve operasyon etkisi Türkçe.
4. **Migration / flag sırası** — DB, config, feature flag aç/kapa.
5. **Rollback kriterleri** — ne zaman geri alınır, nasıl doğrulanır.
6. **Kapı kontrolü** — açık kritik güvenlik/test engeli var mı?
7. **Handoff** → `deployment-engineer`.

## Ortak kurallar

- [tech-stack.md](../_shared/tech-stack.md)
- [engineering-rules.md](../_shared/engineering-rules.md)
- [handoff-protocol.md](../_shared/handoff-protocol.md)
- [obsidian-session.md](../_shared/obsidian-session.md)

## Çıktı şablonu (Türkçe)

```markdown
# Release Planı

## Özet
## Önerilen sürüm
## Changelog
## Breaking change’ler
## Migration / config / feature flag sırası
## Önkoşullar (test / güvenlik kapıları)
## Rollback kriterleri
## İletişim / risk notları
```

## Handoff (sonraki skill)

Varsayılan: **`deployment-engineer`**.

```markdown
## Handoff
- Skill: release-engineer
- Sonraki skill: deployment-engineer
- Önerilen sonraki skill’ler: deployment-engineer
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

- Kritik güvenlik/test engeli varken release önermek
- Tag/push/deploy yapmak (kullanıcı açıkça istemedikçe)
- Rollback’siz “ileriye tek yön” planı
