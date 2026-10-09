# Kurumsal Yazılım Geliştirme için Agent Skills

Kurumsal yazılım geliştirme yaşam döngüsünde coding agent’lara yapılandırılmış, tekrar kullanılabilir iş akışları sağlayan 13 skill. Planlama, uygulama, mimari inceleme, test, güvenlik, release ve deployment adımlarını ortak kurallar ve standart handoff’larla birbirine bağlar.

Talimatlar ve skill çıktıları Türkçedir; skill adları İngilizcedir. Kaynak dosyalar `skills/` altındadır. Repo, Codex, Claude Code ve Cursor için keşif dizinlerini göreli symlink’lerle sağlar.

## Neler içerir?

**Ana geliştirme akışı:**

1. `analyst-planner` — gereksinim, mimari ve iş planı
2. `senior-software-engineer` — planı izleyen geliştirme ve TDD
3. `senior-software-architect` — plan uyumu ve mimari inceleme
4. `senior-software-tester` — unit ve integration testleri
5. `vulnerability-checker` — güvenlik ve uyumluluk incelemesi
6. `git-diff-checker` — değişiklik ve release hazırlığı incelemesi
7. `release-engineer` — sürüm ve geri alma planı
8. `deployment-engineer` — dağıtım ve operasyon planı

**Duruma göre kullanılabilen skill’ler:** `bug-finder`, `database-dba`, `database-report-agent`, `playwright-tester`, `obsidian-memory-manager`.

`skills/_shared/` altında teknoloji yığını, mühendislik kuralları, grilling, TDD, bug teşhisi, glossary, handoff ve Obsidian oturum protokolleri bulunur. Handoff’lar sonraki adıma kapsamı, kararları, riskleri ve artefakt yollarını taşır. Pipeline sonuçları, vault yolu sağlandığında Obsidian oturumuna otomatik kaydedilir.

## Kurulum

Repo’yu klonlayıp kök dizinde aşağıdaki komutu çalıştırın. macOS ve Linux’ta Codex, Claude Code ve Cursor keşif yollarını `skills/` içindeki kanonik kaynaklara bağlar:

```bash
mkdir -p .cursor/skills .claude/skills .agents/skills

for name in \
  analyst-planner senior-software-engineer senior-software-architect \
  senior-software-tester vulnerability-checker git-diff-checker bug-finder \
  release-engineer deployment-engineer database-dba database-report-agent \
  playwright-tester obsidian-memory-manager
do
  ln -sfn "../../skills/$name" ".cursor/skills/$name"
  ln -sfn "../../skills/$name" ".claude/skills/$name"
  ln -sfn "../../skills/$name" ".agents/skills/$name"
done
```

Doğrulamak için:

```bash
test -f .agents/skills/analyst-planner/SKILL.md && echo "Codex skill bağlantısı hazır"
test -f .claude/skills/analyst-planner/SKILL.md && echo "Claude Code skill bağlantısı hazır"
test -f .cursor/skills/analyst-planner/SKILL.md && echo "Cursor skill bağlantısı hazır"
```

Windows’ta symlink oluşturma yetkisi/Developer Mode gerekebilir. Alternatif olarak `skills/<skill-adı>/` klasörlerini ilgili aracın skill keşif dizinine kopyalayın; ortak dosya bağlantıları için `skills/_shared/` klasörünü de aynı göreli yapıda tutun.

## Kullanım

- Yeni bir özellik veya proje için `analyst-planner` ile başlayın.
- İlgili skill’in `SKILL.md` dosyasını coding agent’a verin veya agent’ın keşif dizininden çağırın.
- Handoff’taki sonraki skill’i ve iletilen artefaktları kullanarak akışa devam edin.
- Bug, veritabanı veya UI E2E işleri için duruma uygun yan skill’i doğrudan çağırın.
- Otomatik oturum kaydı için `OBSIDIAN_VAULT_PATH` ayarlayın veya vault yolunu açıkça belirtin. Ayrıntılar: [`obsidian-session.md`](skills/_shared/obsidian-session.md).

Bu skill’ler karar desteği ve iş akışı sağlar; üretim değişiklikleri, erişim yetkileri, test kanıtları ve kurumsal politika uyumu ekip tarafından doğrulanmalıdır. Skill talimatları organizasyonunuzun güvenlik, gizlilik ve değişiklik yönetimi kurallarının yerini almaz.

## Katkıda bulunma

Katkı ve düzeltmeler için [CONTRIBUTING.md](CONTRIBUTING.md) yönergelerini izleyin. Yeni bir skill eklerken ortak handoff ve oturum protokollerini uygulayın; `skills/` dışındaki agent keşif yollarını kanonik kaynaklarla uyumlu tutun.

## Lisans

MIT lisansı altında yayımlanır. Ayrıntı için [LICENSE](LICENSE) dosyasına bakın.
