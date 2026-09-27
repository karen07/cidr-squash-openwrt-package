# cidr-squash OpenWrt package

This repository contains the OpenWrt package definition for [cidr-squash](https://github.com/karen07/cidr-squash), an IPv4 CIDR optimizer with configurable bounded over-coverage.

The package installs the `cidr-squash` binary into `/usr/bin` and does not declare additional OpenWrt runtime dependencies.

For development, the Makefile can build from a sibling `../cidr-squash` checkout. Otherwise OpenWrt fetches the tagged upstream source specified by `PKG_VERSION`.

## Описание

Этот репозиторий содержит описание пакета OpenWrt для [cidr-squash](https://github.com/karen07/cidr-squash), оптимизатора IPv4 CIDR с настраиваемым ограниченным дополнительным покрытием.

Пакет устанавливает бинарный файл `cidr-squash` в `/usr/bin` и не объявляет дополнительных зависимостей времени выполнения OpenWrt.

При разработке Makefile может собирать исходники из соседнего каталога `../cidr-squash`. Если такого каталога нет, OpenWrt загружает версию исходников по тегу, заданному в `PKG_VERSION`.

## Что находится в репозитории

- `cidr-squash/Makefile` - описание OpenWrt package;
- `openwrt-build.env` - параметры пакета для общего CI;
- `.github/workflows/openwrt-build.yml` - вызов общего reusable workflow.

## Сборка

Сборка выполняется через GitHub Actions. Workflow этого репозитория вызывает общий reusable workflow из [openwrt-package-ci](https://github.com/karen07/openwrt-package-ci).

CI можно запустить:

- push тега вида `vX.Y.Z` - значение тега используется как версия OpenWrt;
- вручную через `workflow_dispatch`, указав версию OpenWrt и при необходимости фильтры target/subtarget.

Параметры этого пакета хранятся в `openwrt-build.env`. Общие `openwrt-build.sh`, `openwrt-matrix.py` и логика сборки через OpenWrt SDK находятся в `openwrt-package-ci`.

Для ручной сборки каталог `cidr-squash/` можно использовать как обычный package directory внутри OpenWrt buildroot/SDK.

## Связанные проекты

- [cidr-squash](https://github.com/karen07/cidr-squash) - основной проект и исходный код утилиты.
