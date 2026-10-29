# CIDR Squash OpenWrt Package

OpenWrt packaging for [cidr-squash](https://github.com/karen07/cidr-squash), an IPv4 CIDR
optimizer with optional bounded over-coverage. The package installs the command-line tool
on OpenWrt.

Пакет OpenWrt для [cidr-squash](https://github.com/karen07/cidr-squash) - оптимизатора IPv4
CIDR с ограничиваемым дополнительным покрытием адресов. Устанавливает утилиту командной
строки на OpenWrt.

## Описание

Пакет устанавливает бинарный файл `cidr-squash` в `/usr/bin` и не объявляет дополнительных зависимостей времени выполнения OpenWrt.

При разработке Makefile может собирать исходники из соседнего каталога `../cidr-squash`. Если такого каталога нет, OpenWrt загружает версию исходников по тегу, заданному в `PKG_VERSION`.

## Разработка и проверка изменений

**Основные точки изменения:**

- `cidr-squash/Makefile` - зависимости, версия и правила установки (исполняемая утилита);
- `openwrt-build.env` - параметры сборки для общего CI;
- `.github/workflows/openwrt-build.yml` - вызов переиспользуемого OpenWrt workflow.

**Выбор исходников и артефакт пакета:** `cidr-squash/Makefile` берёт соседний каталог `cidr-squash` при наличии его `CMakeLists.txt`; иначе получает Git-тег `v$(PKG_VERSION)` основного проекта. Пакет устанавливает бинарник в `/usr/bin/cidr-squash`. При проверке релиза отличайте сборку локальных исходников от сборки по тегу и сверяйте `PKG_VERSION` с нужной ревизией. Проверьте запуск CLI для IPv4 и IPv6, режимы CIDR и ranges после установки APK.

**Проверка изменений:** Изменения функциональности: алгоритм оптимизации находится в отдельном `cidr-squash`. Для упаковки проверяйте `Makefile`, `openwrt-build.env` и CI вместе; тестируйте итоговый пакет на нужной версии OpenWrt, поскольку сборка приложения сама по себе не проверяет установку и зависимости.

## Сборка

Сборка выполняется через GitHub Actions. Workflow этого репозитория вызывает общий reusable workflow из [openwrt-package-ci](https://github.com/karen07/openwrt-package-ci).

CI можно запустить:

- push тега вида `vX.Y.Z` - значение тега используется как версия OpenWrt;
- вручную через `workflow_dispatch`, указав версию OpenWrt и при необходимости фильтры target/subtarget.

Параметры этого пакета хранятся в `openwrt-build.env`. Общие `openwrt-build.sh`, `openwrt-matrix.py` и логика сборки через OpenWrt SDK находятся в `openwrt-package-ci`.

Для ручной сборки каталог `cidr-squash/` можно использовать как обычный package directory внутри OpenWrt buildroot/SDK.

## Структура проекта

- `cidr-squash/Makefile` - описание OpenWrt package;
- `openwrt-build.env` - параметры пакета для общего CI;
- `.github/workflows/openwrt-build.yml` - вызов общего reusable workflow.

## Связанные проекты

- [cidr-squash](https://github.com/karen07/cidr-squash) - основной проект и исходный код утилиты.

## Лицензия

Проект распространяется под лицензией GNU Affero General Public License v3.0. Подробности см. в файле [LICENSE](LICENSE).
