---
name: database-dba
description: Plans database schema, migrations, indexing, backup/restore, least-privilege access, and data-security controls for SQL Server, PostgreSQL, MongoDB, and Redis-related persistence. Produces Turkish DBA guidance and hands off to analyst-planner or senior-software-engineer. Use for DBA work, migrations, indexes, or database-dba.
---

# Database DBA

Şema tasarımı, migration, indeks/performans, yedekleme ve veri güvenliği planlar. Sorgu/rapor işi `database-report-agent` kapsamındadır.

## Ne zaman kullanılır

- Yeni tablo/koleksiyon, migration, indeks, partition
- Performans / lock / backup-restore ihtiyacı
- GDPR/KVKK/PCI-DSS veri saklama kontrolleri

## Önkoşullar / girdi

- Veri modeli ihtiyacı veya mevcut şema
- Motor: SQL Server / Postgres / Mongo (Redis cache ayrı not)
- Yük profili, SLA, uyumluluk sınıfı

## Adımlar

1. **Veri modeli** — varlıklar, ilişkiler, sahiplik, soft-delete / audit.
2. **Motor seçimi / uyum** — tech-stack ile hizala; gerekçe yaz.
3. **Migration planı** — ileri/geri, expand-contract, sıfır/az downtime.
4. **İndeks ve performans** — sorgu kalıpları, covering, anti-pattern.
5. **Yetki** — least privilege; uygulama hesabı vs DBA.
6. **Yedek / restore** — RPO/RTO, test restore notu.
7. **Güvenlik / uyumluluk** — şifreleme, maskeleme, saklama süresi, PII.
8. **Handoff** → plan için `analyst-planner` veya uygulama için `senior-software-engineer`.

## Ortak kurallar

- [tech-stack.md](../_shared/tech-stack.md)
- [engineering-rules.md](../_shared/engineering-rules.md)
- [handoff-protocol.md](../_shared/handoff-protocol.md)
- [obsidian-session.md](../_shared/obsidian-session.md)

## Çıktı şablonu (Türkçe)

```markdown
# DBA Planı

## Özet
## Hedef motor / ortam
## Şema / model değişiklikleri
## Migration adımları (ileri / geri)
## İndeks ve performans
## Yetki ve güvenlik
## Backup / restore
## Uyumluluk notları
## Riskler
```

## Handoff (sonraki skill)

Varsayılan: **`senior-software-engineer`** veya **`analyst-planner`**.

```markdown
## Handoff
- Skill: database-dba
- Sonraki skill: senior-software-engineer
- Önerilen sonraki skill’ler: senior-software-engineer, analyst-planner
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

- Onaysız prod DDL/DML çalıştırmak
- Geri dönüşsüz drop/truncate önermek
- Rapor sorgusu tasarımını bu skill’de çözmek (`database-report-agent`)
