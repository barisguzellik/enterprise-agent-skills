# Ubiquitous Language (Paylaşılan Dil)

Amaç: proje jargonunu kısa, tutarlı terimlere indirgemek; ajanın 20 kelimeyle anlattığını 1 terimle konuşmak.

## Kaynak dosya

- Tercih: repo kökünde `GLOSSARY.md`
- Alternatif: Obsidian vault içinde `memory/glossary.md` veya eşdeğer (`obsidian-memory-manager`)
- Varsa ADR’ler: `docs/adr/` veya vault `memory/decisions/`

Her ilgili skill çalışmaya başlamadan önce glossary’yi oku (varsa).

## GLOSSARY.md şablonu

```markdown
# Glossary

| Terim | Anlam | Yanlış / kaçınılacak |
|---|---|---|
| ÖrnekTerim | Kısa tanım | Eski uzun ifade |
```

## ADR kısa şablonu

```markdown
# ADR-NNN: Başlık

- Durum: önerilen | kabul | reddedildi | süpersede
- Bağlam:
- Karar:
- Sonuçlar:
```

## Kurallar

- Kod, plan ve handoff’ta glossary terimlerini kullan.
- Yeni kavram çıkarsa glossary’ye ekle veya `obsidian-memory-manager` ile kaydet; sessizce uydurma.
- Aynı kavram için birden fazla isim kullanma.
- Dosya/sınıf/modül adlarını mümkün olduğunca glossary ile hizala.
