# О программе Vfdmod
Vfdmod это user-space компонент LinuxCNC, предназначенный для управления любыми частотно-регулируемыми приводами (ЧРП, VFD), которые поддерживают стандартный протокол MODBUS RTU.

# Особенности
- Установка скорости с помощью команд MODBUS 0x06 (write holding register) и 0x10 (write multiple holding registers).
- Установка настроек с помощью команд MODBUS 0x06, 0x10, 0x05 (write coil) и 0x0F (write multiple coils).
- Чтение произвольного количества пользовательских параметров с помощью функций MODBUS 0x01 и 0x03.
- Поддерживается четыре типа пользовательских параметров: bit, float, s32 и u32.
- Встроенный генератор PyVcp.
- Мониторинг состояния соединения RS485, в том числе общее количество ошибок и код последней ошибки.
- Автоматическое переподключение при физическом отключении адаптора USB-to-RS485.
- *ЧРП фирмы Huanyang не поддерживаются, поскольку они используют нестандартные коды MODBUS.*

# Скриншоты
![](images/hc1-cplus-axis.png) ![](images/hc1-cplus-hal.png)


# Документация
См. вики vfdmod: [https://github.com/aekhv/vfdmod/wiki](https://github.com/aekhv/vfdmod/wiki)

# Сборка
Ниже приведен пример сборки программы в ОС LinuxCNC 2.9.4.

Установка зависимостей:
```bash
sudo apt-get install qtbase5-dev libmodbus-dev
```

Сборка:
```bash
git clone https://github.com/kang2k10/vfdmod.git
cd vfdmod
mkdir build
cd build
qmake ../vfdmod.pro
make
```

# Загрузки
Новейшие версии DEB-пакеты: [https://github.com/aekhv/vfdmod/releases](https://github.com/aekhv/vfdmod/releases)

# Поддержка
Англоязычный форум поддержки: [https://forum.linuxcnc.org/](https://forum.linuxcnc.org/24-hal-components/38733-vfdmod-an-easy-vfd-control-over-modbus-rtu)

Русский форум поддержки: [http://www.cnc-club.ru/](http://www.cnc-club.ru/forum/viewtopic.php?p=557679)

# Историй изменений
Vfdmod 0.3.2:
- User defined HAL pins may be boolean (bit type):
  - Function code 0x01 (read coils) supported.
  - Function code 0x03 (read holding registers, used by default) may be used to get any single bit within returned 16-bit data.

Vfdmod 0.3.1:
- Function codes 0x05 (write single coil) and 0x0F (write multiple coils) are supported.
- PyVcp generator: fault reset button fixed.
- Blank config file now includes all parameters and short description of each.

Vfdmod 0.3.0:
- Reconnection feature added, it's useful when serial device has been re-attached.
- Fault reset added.
- Function codes 0x06 (write single register) and 0x10 (write multiple registers) are supported.

Vfdmod 0.2.0:
- PyVcp generator added.

Vfdmod 0.1.0:
- First release.
