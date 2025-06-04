# 🪟 MOES MS-108ZR + Home Assistant + Zigbee2MQTT

Инструкция по интеграции модуля MOES MS-108ZR с Home Assistant через Zigbee2MQTT для управления приводами штор с фазным управлением и возможностью позиционного управления (например, открыть на 30% или 80%).

---

![Устройство MOES MS-108ZR](https://cdn.shopify.com/s/files/1/0555/6422/1436/files/详情页_03_480x480.jpg)

---

## ✅ Поддержка позиционного управления

Модуль MOES MS-108ZR позволяет управлять положением штор в процентах (`position` от 0 до 100). Это реализуется через Zigbee2MQTT и отображается в Home Assistant как сущность типа `cover`.

📚 [Документация на zigbee2mqtt.io](https://www.zigbee2mqtt.io/devices/MS-108ZR.html)

---

## 🛠️ Инструкция по настройке

### 1. Подключение и калибровка

1. **Подключите модуль** к приводу штор согласно схеме в [инструкции MOES (PDF)](https://fr.manuals.plus/m/5a1bdcfa9fb50c51ad10a817cd8ca122afd984700c1076a971787ddd455c9ee7_optim.pdf).
2. **Включите Zigbee-паринг**: нажмите и удерживайте кнопку сброса >7 сек до появления быстрого звукового сигнала.
3. **Добавьте устройство в Zigbee2MQTT**. Убедитесь, что оно распознано как `cover` с параметрами:
   - `state`
   - `position`
   - `calibration_time`
   - `motor_reversal`
   - `moving`
4. **Установите время калибровки** (в секундах для полного открытия/закрытия):
```json
{
  "calibration_time": 15
}
```

---

### 2. Управление положением штор

#### Через MQTT:
```json
{
  "position": 30
}
```

#### Через Home Assistant:
```yaml
service: cover.set_cover_position
data:
  entity_id: cover.your_cover_name
  position: 30
```

---

![Управление через Home Assistant](https://cdn.shopify.com/s/files/1/0555/6422/1436/files/详情页_08.jpg)

---

## ⚠️ Возможные проблемы и решения

- **Неправильное отображение (открыто/закрыто)**:
  Установите `invert_cover: true` в конфигурации Zigbee2MQTT.

- **Разная скорость открытия и закрытия**:
  Уточните `calibration_time` или подберите среднее значение.

- **Проблемы с калибровкой**:
  Проверьте, что вы корректно завершили режим калибровки (см. инструкцию MOES).

---

## 📌 Заключение

Модуль MOES MS-108ZR полностью совместим с Home Assistant через Zigbee2MQTT и поддерживает позиционное управление. При правильной настройке вы сможете точно управлять положением штор.

---

## 🔗 Источники

- [zigbee2mqtt.io — MS-108ZR](https://www.zigbee2mqtt.io/devices/MS-108ZR.html)
- [Home Assistant Community](https://community.home-assistant.io/t/moes-ms-108zr-curtain-switch-rf433-module-zigbee-has-anyone-had-experience-with-this/350862)
- [Официальная страница MOES](https://moeshouse.com/products/zigbee-diy-curtain-switch-module)

