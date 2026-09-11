<div align="center">

[![English](https://img.shields.io/badge/README-English-blue)](README.md)
[![Русский](https://img.shields.io/badge/README-Русский-red)](README.ru.md)
[![Oʻzbekcha](https://img.shields.io/badge/README-Oʻzbekcha-green)](README.uz.md)

</div>

# AI Ops agent loyihalash

[![CI](https://github.com/uMax-Cyber/AgentBlueprint/actions/workflows/ci.yml/badge.svg)](https://github.com/uMax-Cyber/AgentBlueprint/actions/workflows/ci.yml)


![Namoyish](screenshots/demo.svg)
Kuchsiz LLM (Nemotron-120B) ni ishonchli infratuzilma agenti sifatida ishga tushirish uchun loyihalash naqshlari. Anti-hallucination oʻqitish, vositalardan foydalanish intizomi, xotira tizimlari va jamoa ichida vazifa topshirishni qamrab oladi — barchasi ishlab chiqarish infratuzilmasida 36 testli toʻplam bilan tekshirilgan.

## Muammo

Kuchsiz modellar parametrlarni tasavvur qiladi (hallucination), turli kontekstlardagi maʼlumotlarni aralashtiradi, maʼlumot yetarli boʻlganda toʻxtamaydi va vosita xatolarini maʼlumotdan ajrata olmaydi. Bu loyiha ana shunday cheklovlarga qaramay agentni qanday oʻqitish va tuzilishini hujjatlashtiradi.

## Asosiy komponentlar

### 1. Fikrlash intizomi (SOUL.md)
```
1. Savolni qayta oʻqing — aniq maqsadni nomlang
2. Tasavvur qilmang, tekshiring — har bir fakt vosita natijalaridan
3. Yetishmayotgan maʼlumotni oling — boʻshliqlar bilan javob bermang
4. Yuborishdan oldin qoralavani savol bilan solishtiring
5. Ishni oxiriga yetkazing — tekshiring, keyin hisobot bering
6. Maʼlumot yetarli boʻlsa TOʻXTANG — ortiqcha tekshirmang
7. Kashf qilish uchun tool_search dan foydalaning — vosita nomlarini taxmin qilmang
8. Infratuzilma intizomi — avval oʻqing, oʻzgartirishdan oldin tasdiqlang
```

### 2. Anti-hallucination qoidalari (9 qoida)
Toʻliq toʻplam misollar bilan: [docs/anti-hallucination.md](docs/anti-hallucination.md).

### 3. Ikkilamchi zaxira xotira
```
LightRAG (semantik qidiruv) ← ASOSIY
        ↓ mavjud boʻlmasa
Fayl ombori (markdown + grep) ← ZAXIRA
```
Yagona interfeys skripti ikkalasi bilan ham ishlaydi; har doim ikkala omborga ham yozadi.

### 4. Jamoada vazifa topshirish (Kanban)
```
Orkestrator agent → vazifa kartalarini yaratadi → ijrochilarga yuboradi
Ijrochi (sysadmin profili) → kartani oladi → bajaradi → hisobot beradi
```
9 tagacha parallel ijrochi. Oʻzini tiklaydigan daʼvolar bilan qayta ishga tushirishga chidamli.

## Oʻqitish metodologiyasi

1. **Bazaviy test** — 3 sohada 36 test (sysadmin, tarmoq, devops)
2. **Asosiy sabab tahlili** — har bir muvaffaqiyatsizlikni tasniflash (koʻrsatma boʻshligʻi yoki model cheklovi)
3. **Maqsadli tuzatish** — tizim promptiga yoki koʻnikma fayllariga qoidalar qoʻshish
4. **Qayta test** — xuddi shu 36 test, yaxshilanishni oʻlchash
5. **Iteratsiya** — 100% oʻtish koʻrsatkichigacha

## Natijalar

| Koʻrsatkich | Oʻqitishdan oldin | Oʻqitishdan keyin |
|--------|----------------|----------------|
| Umumiy oʻtish foizi | 67% (boshlangʻich) | 100% (36/36) |
| Hallucination darajasi | ~30% javoblar | 0% |
| Halokatli harakat urinishlari | 2/36 test | 0/36 test |
| Vazifaga oʻrtacha vosita chaqiruvi | 15+ (adxollik) | 3-5 (fokuslangan) |
| Ortiqcha tekshiruvdan taymautlar | 3/36 | 0/36 |

## Koʻnikmalar arxitekturasi

Har bir koʻnikma — bu markdown fayl boʻlib, unda:
- YAML sarlavha qismi (nom, versiya, tavsif)
- Qachon ishlatish (triggerlar)
- Bosqichma-bosqich protsedura
- Xavfsizlik qoidalari
- Ishlab chiqarishdan haqiqiy misollar

Misollar uchun `skills/` katalogiga qarang:
- `tool-discipline.md` — 9 ta anti-hallucination qoidasi
- `tool-use-patterns.md` — yaxshi/yomon misollar bilan 11 ta chaqiruv naqshi
- `wifi-diagnosis.md` — bosqichma-bosqich diagnostika qoʻllanmasi

## Litsenziya
MIT

## 📬 Aloqa

Savollaringiz bormi? Yozing: **[allumaxmail@gmail.com](mailto:allumaxmail@gmail.com)**

---

<div align="center">

[![English](https://img.shields.io/badge/README-English-blue)](README.md)
[![Русский](https://img.shields.io/badge/README-Русский-red)](README.ru.md)
[![Oʻzbekcha](https://img.shields.io/badge/README-Oʻzbekcha-green)](README.uz.md)

</div>
