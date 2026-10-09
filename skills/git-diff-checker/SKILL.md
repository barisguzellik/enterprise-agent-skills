---
name: git-diff-checker
description: Inspects active git changes for Spec fidelity, Standards smells, scope creep, breaking changes, merge-danger, and release risk. Produces a Turkish change review and hands off to release-engineer or back for fixes. Use when reviewing git diff, PR changes, or git-diff-checker.
---

# Git Diff Checker

Aktif geliştirmedeki git değişikliklerini Spec + Standards ve release riski açısından inceler.

## Ne zaman kullanılır

- Güvenlik kapısı sonrası release öncesi diff kontrolü
- PR / branch değişiklik özeti istendiğinde
- “Ne değişti?” risk değerlendirmesi

## Önkoşullar / girdi

- Vulnerability (veya önceki) handoff
- Git working tree / branch (status + diff)
- Beklenen plan / spec kapsamı

## Adımlar

1. **Diff topla** — staged, unstaged, branch vs base; secret içeren dosyaları işaretle (redact).
2. **Spec uyumu** — plana/kabul kriterlerine göre scope creep veya eksik davranış.
3. **Standards kokuları** — dead code, TODO blocker, debug log, sığ modül, test/docs eksikleri.
4. **Breaking change** — API, şema, config, event sözleşmesi.
5. **Merge-danger** — tek yön kapı (geri dönüş zor) vs çift yön; blast radius.
6. **Eksikler** — test, migration, docs, feature flag, rollback etkisi.
7. **Karar** — release’e uygun | düzeltme gerekli.
8. **Handoff** → uygunsa `release-engineer`; değilse engineer/tester.

## Ortak kurallar

- [tech-stack.md](../_shared/tech-stack.md)
- [engineering-rules.md](../_shared/engineering-rules.md)
- [handoff-protocol.md](../_shared/handoff-protocol.md)
- [obsidian-session.md](../_shared/obsidian-session.md)

## Çıktı şablonu (Türkçe)

```markdown
# Git Diff İncelemesi

## Özet
## Diff kapsamı (dosya / satır özeti)
## Spec uyumu
## Standards bulguları
## Breaking change’ler
## Merge-danger: tek-yön | çift-yön | blast radius
## Eksik artefaktlar (test / docs / migration)
## Risk listesi
| Severity | Bulgu | Öneri |
|---|---|---|
## Release önerisi: uygun | düzeltme gerekli
```

## Handoff (sonraki skill)

- Uygun → **`release-engineer`**
- Düzeltme → **`senior-software-engineer`** (veya ilgili tester)

```markdown
## Handoff
- Skill: git-diff-checker
- Sonraki skill: release-engineer
- Önerilen sonraki skill’ler: release-engineer
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

- Commit / push yapmak (kullanıcı istemedikçe)
- Diff’i okumadan genel yorum yazmak
- Secret’ları rapor gövdesinde açık göstermek
