# Obsidian Oturum Protokolü

Pipeline çıktıları Obsidian’a **otomatik** yazılır. `obsidian-memory-manager` skill’ini her adımda çağırmaya gerek yoktur; o skill yalnızca manuel / ek bellek işleri içindir.

## Vault kökü çözümleme (öncelik sırası)

1. Çağrıda verilen açık path (`Hedef dizin` / `Obsidian vault`)
2. Ortam değişkeni: **`OBSIDIAN_VAULT_PATH`**
3. Yoksa kullanıcıya sor (başlatıcı skill’de zorunlu; rastgele dizin yasak)

## Başlatıcı skill’ler

Yeni oturum dizini **oluşturur** (gelen handoff’ta oturum yoksa):

- `analyst-planner` (ana zincir)
- `bug-finder`, `database-dba`, `database-report-agent`, `playwright-tester` (yan zincir başlangıcı)

Gelen handoff’ta `Obsidian oturum dizini` varsa **yeni oluşturma**; mevcut oturuma ekle.

## Oturum dizini

```text
$OBSIDIAN_VAULT_PATH/memory/sessions/YYYY-MM-DD-<kisa-slug>/
  index.md
  01-analyst-planner.md
  02-senior-software-engineer.md
  ...
```

- `<kisa-slug>`: görev/özetten 2–5 kelimelik ASCII/kebab (örn. `odeme-api-refactor`)
- İlk notta `index.md` oluştur; her skill sonrası index’e wikilink satırı ekle

## Her skill sonunda (zorunlu, otomatik)

Handoff bloğu taslaklandıktan hemen sonra, yanıtın sonunda sunulmadan önce:

1. Oturum dizinini handoff’tan veya (başlatıcıysa) yeni oluşturarak belirle.
2. `NN-<skill-name>.md` yaz (`NN` = oturumdaki sıradaki numara: 01, 02, …).
3. Not içeriği: skill’in Türkçe çıktı özeti + Handoff bloğu (secret/PII redact).
4. `index.md` güncelle: `- [[NN-skill-name]] — kısa özet`
5. Handoff taslağına Obsidian alanlarını doldur (aşağıdaki şablon); kayıt tamamlandıktan sonra bu handoff’u yanıtın sonunda sun.

`obsidian-memory-manager` skill’ini bu otomatik adım için **çağırma** (özyineleme / gereksiz orkestrasyon yok). Protokolü doğrudan uygula.

## Not dosyası şablonu

```markdown
---
tags: [sdlc, session]
skill: <skill-adı>
date: YYYY-MM-DD
session: <oturum-klasör-adı>
---

# <Skill görünen adı>

## Çıktı özeti
<skill çıktısının Türkçe özeti veya ana bölümleri>

## Handoff
<aynı handoff bloğu>

## Bağlantılar
- [[index]]
```

## Handoff Obsidian alanları

```markdown
- Obsidian vault: <kök path veya OBSIDIAN_VAULT_PATH>
- Obsidian oturum dizini: <tam path>
- Obsidian not: <yazılan NN-skill.md path>
```

## Manuel kullanım

Ek glossary/ADR düzenleme, eski oturumu yeniden yapılandırma veya vault bakımı için kullanıcı **`obsidian-memory-manager`** çağırır. Otomatik oturum yazımının yerine geçmez; tamamlar.
