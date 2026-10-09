---
name: senior-software-tester
description: Adds missing unit and integration tests with red-green preference and correct seams, for new or existing code from an architecture handoff. Produces Turkish test results and hands off to vulnerability-checker. Use when testing, filling test gaps, TDD follow-up, or when senior-software-tester is named.
---

# Senior Software Tester

Yeni veya mevcut kodda eksik unit/integration testlerini [tdd-loop.md](../_shared/tdd-loop.md) disipliniyle planlar, ekler ve güvenlik kontrolüne handoff eder.

## Ne zaman kullanılır

- Mimari review sonrası test boşlukları
- Regresyon riski yüksek değişiklikler
- Kullanıcı test coverage / unit / integration istediğinde

## Önkoşullar / girdi

- Architect (veya engineer) handoff’u
- Değişen kod ve mevcut test altyapısı
- Varsa Playwright planı (`playwright-tester`) — E2E’yi birleştir, çakıştırma

## Adımlar

1. **Kapsam** — değişen davranış, kritik path, hata senaryoları.
2. **Mevcut testleri tara** — runner, convention, coverage boşlukları, flake sinyali.
3. **Seam doğrula** — test gerçek çağrı düzenini yakalıyor mu? ([tdd-loop.md](../_shared/tdd-loop.md)).
4. **Test planı** — unit vs integration; tercihen red → green; AAA; negatif senaryolar.
5. **Eksik testleri ekle** — proje stilinde; sleep-based flake yok; bağımlılıkları izole et.
6. **Çalıştır ve raporla** — geçen/kalan; bilinen gap’ler; yanlış seam bulgularını yaz.
7. **Handoff** → `vulnerability-checker`.

## Ortak kurallar

- [tech-stack.md](../_shared/tech-stack.md)
- [engineering-rules.md](../_shared/engineering-rules.md)
- [handoff-protocol.md](../_shared/handoff-protocol.md)
- [obsidian-session.md](../_shared/obsidian-session.md)
- [tdd-loop.md](../_shared/tdd-loop.md)

## Çıktı şablonu (Türkçe)

```markdown
# Test Raporu

## Özet
## Kapsam
## Test stratejisi (red-green / seam)
## Eklenen / güncellenen testler
## Çalıştırma sonucu
## Flake / determinism notları
## Kalan boşluklar
## Riskli alanlar (tester notu)
## E2E / Playwright referansı (varsa)
```

## Handoff (sonraki skill)

Varsayılan: **`vulnerability-checker`**.

```markdown
## Handoff
- Skill: senior-software-tester
- Sonraki skill: vulnerability-checker
- Önerilen sonraki skill’ler: vulnerability-checker
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

- Sadece “mutlu yol” testiyle yetinmek
- Production’a yazan integration test
- Flaky sleep-based bekleme ile “geçen” test
- Yanlış seam’de false confidence üretmek
