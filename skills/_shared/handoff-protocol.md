# Handoff Protokolü

Her skill çalışmasının sonunda **Türkçe** handoff üretir. Sonraki skill yalnızca bu handoff + ilgili artefaktlarla ilerler.

Her skill, handoff bloğunu taslakladıktan sonra yanıtın sonunda sunmadan önce çıktısını Obsidian oturumuna **otomatik** yazar; notta aynı handoff bloğu bulunur. Kayıt tamamlanınca Obsidian alanları doldurulmuş handoff sunulur. Ayrıntı: [obsidian-session.md](obsidian-session.md).

## Ana zincir (1→8)

1. `analyst-planner`
2. `senior-software-engineer`
3. `senior-software-architect`
4. `senior-software-tester`
5. `vulnerability-checker`
6. `git-diff-checker`
7. `release-engineer`
8. `deployment-engineer`

Not: `bug-finder` ana zincirin yanında çağrılabilir; bulgular genelde engineer veya tester’a döner. Numaralandırmada ayrı bir yan roldür (`bug-finder`).

## Yan roller

| Skill | Tipik çağrı | Tipik sonraki |
|---|---|---|
| `bug-finder` | hata / regresyon şüphesi | `senior-software-engineer` veya `senior-software-tester` |
| `database-dba` | şema / migration / performans | `analyst-planner` veya `senior-software-engineer` |
| `database-report-agent` | rapor / sorgu hazırlığı | kullanıcı veya `obsidian-memory-manager` |
| `playwright-tester` | UI E2E planı | `senior-software-tester` |
| `obsidian-memory-manager` | manuel bellek / glossary / ADR | pipeline’a geri besleme veya tamamlandı |

## Zorunlu handoff şablonu

Çıktının sonunda birebir bu yapıyı kullan:

```markdown
## Handoff
- Skill: <mevcut-skill-adı>
- Sonraki skill: <hedef-skill-adı>
- Önerilen sonraki skill’ler: <birincil + varsa alternatifler>
- Durum: tamamlandı | engellendi | kısmi
- Özet: <1-3 cümle>
- Üretilen artefaktlar: <path veya URL; içeriği tekrar yazma>
- Kararlar / kısıtlar: <mimari, tech, kapsam>
- Riskler (güvenlik, uyumluluk, performans): <varsa severity ile>
- Açık sorular: <yoksa "yok">
- Obsidian vault: <kök path>
- Obsidian oturum dizini: <session path>
- Obsidian not: <bu skill’in yazdığı md path>
- Sonraki skill için giriş: <somut, uygulanabilir talimat; oturum path’ini de ilet>
```

## Kurallar

- Dil: talimatlar ve handoff **Türkçe**.
- Artefaktları kopyalama: plan, diff, test raporu, ADR zaten dosyadaysa **path/URL** ver; gövdeyi tekrar etme.
- Secret, parola, ham PII, kart verisi handoff’ta **redact**.
- Durum `engellendi` ise sonraki skill’e geçilmez; engel ve gereken karar yazılır. Obsidian’a yine de durum notu yazılabilir.
- Durum `kısmi` ise tamamlanan / kalan iş ayrılır.
- Kritik güvenlik veya uyumluluk riski varsa sonraki skill’e net uyarı bırakılır.
- Zincir dışı skill çağrıldıysa handoff’ta ana zincire nasıl bağlanacağı belirtilir.
- `Önerilen sonraki skill’ler` birincil hedefi ve gerekirse yan rolü (ör. `database-dba`) listeler.
- Sonraki skill, gelen handoff’taki **Obsidian oturum dizinini** aynen kullanır; yeni oturum açmaz (başlatıcı değilse).
- Otomatik Obsidian yazımı için `obsidian-memory-manager` skill’ini çağırma; [obsidian-session.md](obsidian-session.md) uygula.
