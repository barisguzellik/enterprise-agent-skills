# Ortak Teknoloji Yığını

Skill’ler plan, geliştirme, review, test, release ve deploy üretirken bu yığını önce tercih eder. Projede farklı bir teknoloji zorunluysa gerekçeyi handoff’ta açıkça yaz.

## Backend

- **.NET / C#** — servisler, API’ler, domain ve application katmanları
- **Node.js / JavaScript / TypeScript** — BFF, tooling, hafif API’ler, script’ler
- **Microservices** — bağımsız deploy, net bounded context ve veri sahipliği gerektiğinde

## Frontend

- **React.js** — bileşen tabanlı SPA / admin / ürün UI
- **Vue** — mevcut Vue kod tabanları ve yeni Vue UI’lar
- **TypeScript** — yeni frontend ve Node kodunda varsayılan tip güvenliği

## Veri ve önbellek

- **SQL Server** — ilişkisel / kurumsal OLTP
- **PostgreSQL** — ilişkisel OLTP, JSONB ve açık ekosistem ihtiyaçları
- **MongoDB** — doküman modeli, esnek şema
- **Redis** — cache, session, rate-limit, kısa ömürlü state
- **Elasticsearch** — arama, log/analytics indeksleri

## Mesajlaşma

- **Kafka** — yüksek hacimli event stream, log benzeri dağıtım
- **RabbitMQ** — iş kuyruğu, routing, klasik messaging

## Altyapı ve operasyon

- **Docker** — imaj, yerel ve CI paketleme
- **Kubernetes** — orkestrasyon, scaling, health, rollout
- **Vault** — secret yönetimi (kodda secret yok)
- **Prometheus** — metrik, alert, SLO gözlemi

## Mimari seçim ilkesi

Teknoloji seçimi tek başına karar değildir. Önce sınırlar (bounded context), veri sahipliği, tutarlılık ve operasyon maliyeti değerlendirilir; ardından yığından en uygun araç seçilir. Ayrıntılar için [engineering-rules.md](engineering-rules.md).
