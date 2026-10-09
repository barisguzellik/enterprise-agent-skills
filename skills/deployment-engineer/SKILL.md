---
name: deployment-engineer
description: Creates a Turkish deployment plan from a release plan covering Docker/Kubernetes, Vault config, health checks, Prometheus, rollout strategy, and rollback. Use for deploy planning, Kubernetes rollout, or deployment-engineer. Does not execute production deploy without explicit user approval.
---

# Deployment Engineer

Release planına göre deploy planlaması yapar (Docker/K8s, gözlemlenebilirlik, rollback).

## Ne zaman kullanılır

- Release planı hazırken
- Ortam deploy stratejisi (canary / blue-green / rolling) gerektiğinde

## Önkoşullar / girdi

- `release-engineer` handoff’u
- Hedef ortam (dev/stage/prod), mevcut chart/manifest/pipeline
- Vault / config / secret gereksinimleri

## Adımlar

1. **Artefaktlar** — imaj, tag, chart/manifest, migration job.
2. **Config / secret** — Vault; ortam değişkenleri; secret’ı plana yazma.
3. **Rollout stratejisi** — rolling / canary / blue-green; trafik kaydırma.
4. **Health ve readiness** — probe’lar, smoke checklist.
5. **Gözlemlenebilirlik** — Prometheus metrik/alert; log korelasyonu.
6. **Rollback** — adımlar, RTO beklentisi, veri migration geri dönüşü.
7. **Onay kapısı** — prod deploy için kullanıcı onayı zorunlu.
8. **Handoff** — tamamlandı veya `obsidian-memory-manager` ile bellek kaydı.

## Ortak kurallar

- [tech-stack.md](../_shared/tech-stack.md)
- [engineering-rules.md](../_shared/engineering-rules.md)
- [handoff-protocol.md](../_shared/handoff-protocol.md)
- [obsidian-session.md](../_shared/obsidian-session.md)

## Çıktı şablonu (Türkçe)

```markdown
# Deploy Planı

## Özet
## Hedef ortam
## Artefaktlar (image / tag / manifest)
## Config ve secret (Vault referansları)
## Rollout adımları (sıralı)
## Health / smoke checklist
## Prometheus / alert
## Rollback adımları
## Onay gereksinimleri
```

## Handoff (sonraki skill)

Varsayılan: **tamamlandı** veya **`obsidian-memory-manager`**.

```markdown
## Handoff
- Skill: deployment-engineer
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

Bu skill oturum devam ettiricidir. Girdi handoff’undaki `Obsidian oturum dizini` ve vault bilgisini aynen kullan; yeni oturum oluşturma. Handoff bloğunu taslakla, sıradaki `NN-<skill-name>.md` notunu ve `index.md` wikilink satırını oluştur/güncelle, Obsidian alanlarını doldur ve ancak kayıt tamamlandıktan sonra handoff’u sun. Gerekli oturum/vault bilgisi yoksa tahmin ederek yazma; başlatıcı protokolünün vault çözümlemesini uygula veya kullanıcıdan eksik yolu iste.

Notta Türkçe çıktı özeti ile handoff bloğunu tut; secret/PII’yi redact et. Bu otomatik kayıt için `obsidian-memory-manager` çağırma. Ayrıntılı biçim ve sıra: [obsidian-session.md](../_shared/obsidian-session.md).

## Yapılmayacaklar

- Kullanıcı onayı olmadan production deploy
- Secret değerlerini plana/commit’e yazmak
- Rollback’siz prod kesici değişiklik
