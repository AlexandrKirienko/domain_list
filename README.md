# domain_list

Готовые rule-sets для [sing-box](https://sing-box.sagernet.org/) в бинарном формате (`.srs`). Каждый файл — набор доменов (`domain_suffix`, покрывает и поддомены) по тематике.

## Наборы правил

| Файл | Сервисы | Доменов |
|------|---------|---------|
| `cursor.srs` | Cursor, xAI (x.ai, spacex.ai), Vercel Storage, ToDesktop | 9 |
| `copilot.srs` | GitHub Copilot (включая api.github.com) | 5 |
| `kinowatch.srs` | KinoPub / kino.watch и их CDN | 25 |
| `vps.srs` | VDSina, avocado-sw, serv.host, on1x.cloud | 5 |

## Прямые ссылки (raw)

```
https://raw.githubusercontent.com/AlexandrKirienko/domain_list/main/cursor.srs
https://raw.githubusercontent.com/AlexandrKirienko/domain_list/main/copilot.srs
https://raw.githubusercontent.com/AlexandrKirienko/domain_list/main/kinowatch.srs
https://raw.githubusercontent.com/AlexandrKirienko/domain_list/main/vps.srs
```

## Пример конфига sing-box

```json
{
  "route": {
    "rules": [
      { "rule_set": ["cursor", "copilot"], "outbound": "proxy" }
    ],
    "rule_set": [
      {
        "tag": "cursor",
        "type": "remote",
        "format": "binary",
        "url": "https://raw.githubusercontent.com/AlexandrKirienko/domain_list/main/cursor.srs",
        "download_detour": "proxy",
        "update_interval": "24h"
      },
      {
        "tag": "copilot",
        "type": "remote",
        "format": "binary",
        "url": "https://raw.githubusercontent.com/AlexandrKirienko/domain_list/main/copilot.srs",
        "download_detour": "proxy",
        "update_interval": "24h"
      }
    ]
  }
}
```

Для локального использования (файл уже на устройстве) замените `type` на `local` и укажите `path` вместо `url`.

## Примечания

- Формат rule-set: version 2 (sing-box 1.8+). Для компиляции из исходников: `sing-box rule-set compile rules.json --output rules.srs`.
- `raw.githubusercontent.com` кэширует файлы ~5 минут — после обновления набора изменения подтягиваются с небольшой задержкой.
