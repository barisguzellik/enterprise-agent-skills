# Bug Diagnosis Loop

Amaç: spekülatif fix yerine kanıtlı teşhis. Faz atlama yalnızca gerekçeyle.

**Secret redact:** komut/çıktı/artefaktta secret gösterme; `<REDACTED>` kullan.

## Faz 1 — Sıkı feedback loop (asıl iş)

Bu bug’a **kırmızı** düşen tek komut/sinyal kur (test, curl, CLI, Playwright, replay, harness…).

Tamam kriteri:

- [ ] Kullanıcının **tam semptomunu** yakalar (yanlış yakın hata değil)
- [ ] Deterministik (veya yüksek repro oranı)
- [ ] Mümkün olduğunca hızlı
- [ ] Ajanın çalıştırabildiği

Loop yokken Faz 2–3’e geçme. Kuramazsan denenenleri listele ve kullanıcıdan ortam/artefakt iste.

## Faz 2 — Reproduce + minimise

Loop’u kırmızı gör. Girdileri tek tek küçült; her kesimden sonra tekrar çalıştır. Her kalan parça yük taşıyıcı olsun.

## Faz 3 — Hipotez

3–5 sıralı, **yanlışlanabilir** hipotez:

> “X neden ise, Y yapınca bug kaybolur / kötüleşir.”

Listeyi kullanıcıya göster (ucuz checkpoint); AFK ise kendi sıranla ilerle.

## Faz 4 — Instrument

Her probe bir hipotez tahminine bağlı olsun. Bir anda bir değişken. Tercih: debugger → hedefli log (`[DEBUG-xxxx]` öneki). Perf’te önce ölç, sonra düzelt.

## Faz 5 — Fix + regresyon

Doğru seam varsa: önce kırmızı regresyon testi, sonra fix, sonra orijinal (minimize edilmemiş) loop yeşil. Seam yoksa mimari engeli not et.

## Faz 6 — Cleanup

- [ ] Orijinal loop yeşil
- [ ] Regresyon testi (veya seam yok notu)
- [ ] `[DEBUG-...]` temiz
- [ ] Throwaway harness silindi / işaretlendi
- [ ] Doğru hipotez handoff/commit notunda

Fix uygulaması genelde `senior-software-engineer`; bu skill teşhisi bitirmeden geniş refactor yapmaz.
