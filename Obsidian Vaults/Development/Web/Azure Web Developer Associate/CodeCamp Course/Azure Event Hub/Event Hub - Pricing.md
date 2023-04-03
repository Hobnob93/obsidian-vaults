#azure #az-204 #az-tiers 

Pricing is based on a few measurements:
- Capacity Unit (CU)
- Processing Unit (PU)
- Throughput Unit (TU)

|                    | Basic             | Standard          | Premium          | Dedicated        |
| ------------------ | ----------------- | ----------------- | ---------------- | ---------------- |
| Capacity           | $0.015/hour/TU    | $0.03/hour/TU     | $1.233/hour/PU   | $6.849/hour/CU   |
| Ingress events     | $0.028/mil events | $0.028/mil events | Included         | Included         |
| Capture            | No                | $73/month/TU      | Included         | Included         |
| Apache Kafka       | No                | Yes               | Yes              | Yes              |
| Schema Registry    | No                | Yes               | Yes              | Yes              |
| Max Retention      | 1 day             | 7 days            | 90 days          | 90 days          |
| Storage Retention  | 84 GB             | 84 GB             | 1 TB/PU included | 1 TB/CU included |
| Extended Retention | No                | No                | $0.012/GB/month  | $0.12/GB/month   |
