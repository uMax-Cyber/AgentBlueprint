<div align="center">

[![English](https://img.shields.io/badge/README-English-blue)](README.md)
[![Русский](https://img.shields.io/badge/README-Русский-red)](README.ru.md)
[![Oʻzbekcha](https://img.shields.io/badge/README-Oʻzbekcha-green)](README.uz.md)

</div>

# AI Ops agentini loyihalash

[![CI](https://github.com/uMax-Cyber/AgentBlueprint/actions/workflows/ci.yml/badge.svg)](https://github.com/uMax-Cyber/AgentBlueprint/actions/workflows/ci.yml)


![Namoyish](screenshots/demo.svg)
Kuchsiz LLM (Nemotron-120B) ni ishonchli infratuzilma agentiga aylantirish boʻyicha dizayn naqshlari: anti-hallucination oʻqitish, tool ishlatish intizomi, xotira tizimlari va jamoada vazifa boʻlishish — hammasi production infratuzilmada 36 testli toʻplamdan oʻtgan.

## Muammo

Kuchsiz modellar parametrni oʻylab topadi, turli kontekstdagi maʼlumotni aralashtiradi, maʼlumot yetarli boʻlgach ham toʻxtamaydi, tool xatosini maʼlumotdan ajrata olmaydi. Loyiha ana shunday cheklovlarga qaramay agentni qanday ishonchli qilishni koʻrsatadi.

## Asosiy komponentlar

### 1. Fikrlash intizomi (SOUL.md)
```
1. Savolni qayta oʻqing — aniq maqsadni nomlang
2. Oʻylab topmang, tekshiring — har bir fakt tool natijasidan
3. Yetishmayotgan maʼlumotni oling — javobni boʻshliqlar bilan yubormang
4. Yuborishdan oldin qoralavani savolga solishtiring
5. Ishni oxirigacha olib boring — tekshiring, soʻng hisobot bering
6. Maʼlumot yetarli boʻlsa TOʻXTANG — ortiqchasini tekshirmang
7. Yangi tool izlashda tool_search dan foydalaning — nomini taxmin qilmang
8. Infratuzilma intizomi — avval oʻqing, oʻzgartirishdan oldin tasdiq oling
```

### 2. Anti-hallucination qoidalari (9 ta)
Toʻliq toʻplam misollar bilan: [docs/anti-hallucination.md](docs/anti-hallucination.md).

### 3. Zaxirali xotira
```
LightRAG (semantik qidiruv) ← ASOSIY
        ↓ ishlamay qolsa
Fayl ombori (markdown + grep) ← ZAXIRA
```
Yagona interfeys skripti ikkalasi bilan ishlaydi; yozuv har doim ikkala omborga tushadi.

### 4. Jamoada vazifa boʻlishish (Kanban)
```
Orkestrator agent → vazifa kartasini yaratadi → ijrochilarga tarqatadi
Ijrochi (sysadmin profili) → kartani oladi → bajaradi → hisobot beradi
```
Bir vaqtda 9 tagacha ijrochi ishlaydi. Qayta ishga tushirilsa ham jarayon uzilmaydi — daʼvolar oʻzini tiklaydi.

## Oʻqitish metodikasi

1. **Bazaviy test** — 3 sohada 36 test (sysadmin, tarmoq, devops)
2. **Sabab tahlili** — har bir ishdan chiqishni tasniflang: koʻrsatmada kamchilikmi yoki modelning cheklovi
3. **Aniq tuzatish** — system prompt yoki skill faylga qoida qoʻshing
4. **Qayta test** — oʻsha 36 test; yaxshilanishni oʻlchang
5. **Iteratsiya** — 100% oʻtishga qadar

## Natijalar

| Koʻrsatkich | Oʻqitishdan oldin | Oʻqitilgandan keyin |
|--------|----------------|----------------|
| Umumiy oʻtish foizi | 67% (boshlangʻich) | 100% (36/36) |
| Hallucination darajasi | ~30% javoblarda | 0% |
| Halokatli harakatga urinish | 2/36 test | 0/36 test |
| Vazifaga oʻrtacha tool chaqiruvi | 15+ (adashib yurish) | 3-5 (aniq maqsadda) |
| Ortiqcha tekshiruvdan timeout | 3/36 | 0/36 |

## Skill arxitekturasi

Har bir skill — markdown fayl, tarkibida:
- YAML frontmatter (nom, versiya, tavsif)
- Qachon ishlatiladi (triggerlar)
- Bosqichma-bosqich protsedura
- Xavfsizlik qoidalari
- Productiondan olingan haqiqiy misollar

Namunalar `skills/` katalogida:
- `tool-discipline.md` — 9 ta anti-hallucination qoidasi
- `tool-use-patterns.md` — yaxshi va yomon misollar bilan 11 ta chaqiruv naqshi
- `wifi-diagnosis.md` — bosqichma-bosqich diagnostika runbooki

## Litsenziya
MIT

## 📬 Aloqa

Savol boʻlsa yozing: **[allumaxmail@gmail.com](mailto:allumaxmail@gmail.com)**

---

<div align="center">

[![English](https://img.shields.io/badge/README-English-blue)](README.md)
[![Русский](https://img.shields.io/badge/README-Русский-red)](README.ru.md)
[![Oʻzbekcha](https://img.shields.io/badge/README-Oʻzbekcha-green)](README.uz.md)

</div>
