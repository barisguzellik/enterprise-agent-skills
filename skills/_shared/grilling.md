# Grilling (Hizalama Döngüsü)

Amaç: ajan ile kullanıcı arasında yanlış anlaşılmayı plan/kod üretmeden önce kapatmak.

## Ne zaman

- `analyst-planner` plan yazmadan önce (zorunlu tur)
- Büyük karar, belirsiz epic veya “ne istediğimizi bilmiyoruz” sinyali

## Kurallar

- Varsayımları gizli tutma; her varsayımı soru veya açık “varsayım” satırı yap.
- Tasarım ağacını dal dal kapat: her açık dal için netleşene kadar sor.
- Aynı anda tek karar noktasına odaklan; cevap gelmeden sonraki dala atlama.
- Kullanıcı AFK / kısa cevap verdiyse bilinenlerle ilerleme notu yaz; kapanmayan dalları `Açık sorular`da bırak.
- **Kritik belirsizlik kapanmadan** `senior-software-engineer` handoff’u `tamamlandı` olmaz → `kısmi` veya `engellendi`.

## Soru örnekleri (TR)

- Başarı ölçütü nedir? Ne “bitti” sayılır?
- Kim etkilenir? Hangi ortam (dev/stage/prod)?
- Monolith / modular monolith / microservice tercihi ve gerekçe?
- Veri sahipliği, tutarlılık, PII/ödeme verisi var mı?
- Bilinçli olarak dışarıda bırakılanlar neler?

## Çıktı

Grilling özeti plana veya handoff’a gömülür:

```markdown
## Grilling özeti
- Kapanan kararlar:
- Hâlâ açık dallar:
- Varsayımlar (onaylanmış / varsayılan):
```
