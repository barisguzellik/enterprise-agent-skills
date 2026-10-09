---
name: bug-finder
description: Diagnoses bugs with a phased feedback-loop-first method (reproduce, minimise, hypothesize, instrument) before fix recommendations. Produces Turkish bug analysis and hands off to senior-software-engineer or senior-software-tester. Use when debugging, diagnosing, finding bugs, investigating failures, or bug-finder.
---

# Bug Finder

Verilen repoda veya aktif geliştirmede bug’ları [bug-diagnosis-loop.md](../_shared/bug-diagnosis-loop.md) ile teşhis eder; spekülatif fix yok.

## Ne zaman kullanılır

- Hata / regresyon / flaky / performans şüphesi
- “Neden bozuldu?” / “diagnose” / “debug” kök neden analizi
- Ana zincir dışında yan rol olarak

## Önkoşullar / girdi

- Semptom, hata mesajı, repro adımları (varsa)
- Repo / branch / ilgili log veya test çıktısı
- Beklenen davranış; varsa `GLOSSARY.md`

## Adımlar

1. **Semptomu netleştir** — gözlenen vs beklenen; ortam; secret redact.
2. **Faz 1 — sıkı loop** — bu bug’a kırmızı düşen komut/sinyal kur; yoksa hipoteze geçme.
3. **Faz 2 — reproduce + minimise** — kırmızı gör; repro’yu küçült.
4. **Faz 3 — hipotez** — 3–5 yanlışlanabilir hipotez; kullanıcıya göster.
5. **Faz 4 — instrument** — hipoteze bağlı probe; `[DEBUG-xxxx]` öneki.
6. **Etki / öncelik** — kullanıcı etkisi, veri kaybı, güvenlik.
7. **Fix yönü** — doğru hipotez + regresyon seam önerisi; geniş fix’i engineer’a bırak (Faz 5–6 notları).
8. **Handoff** → fix: `senior-software-engineer`; test: `senior-software-tester`.

## Ortak kurallar

- [tech-stack.md](../_shared/tech-stack.md)
- [engineering-rules.md](../_shared/engineering-rules.md)
- [handoff-protocol.md](../_shared/handoff-protocol.md)
- [obsidian-session.md](../_shared/obsidian-session.md)
- [bug-diagnosis-loop.md](../_shared/bug-diagnosis-loop.md)

## Çıktı şablonu (Türkçe)

```markdown
# Bug Analizi

## Özet
## Semptom
## Beklenen davranış
## Feedback loop komutu (kırmızı kanıt)
## Minimise edilmiş repro
## Hipotezler (sıralı)
## Kanıtlar / instrument
## Kök neden (doğrulanmış / olası)
## Etki ve öncelik: kritik | yüksek | orta | düşük
## Önerilen düzeltme yönü
## Regresyon test / seam önerisi
## Cleanup checklist
```

## Handoff (sonraki skill)

Varsayılan: **`senior-software-engineer`** (fix) veya **`senior-software-tester`** (test).

```markdown
## Handoff
- Skill: bug-finder
- Sonraki skill: senior-software-engineer
- Önerilen sonraki skill’ler: senior-software-engineer, senior-software-tester
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

- Kırmızı loop olmadan spekülatif fix / büyük refactor
- Secret’ı çıktıda göstermek
- Production’da yıkıcı debug işlemi
- Cleanup’siz `[DEBUG-...]` bırakmak (fix aşamasına not düş)
