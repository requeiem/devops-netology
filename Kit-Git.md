# Домашнее задание к занятию «Инструменты Git»

## Задание

В клонированном репозитории:

1. Найдите полный хеш и комментарий коммита, хеш которого начинается на `aefea`.

Команда:
```bash
git show aefea --pretty=format:'%H %n %s' -q
```
Вывод:
```bash
aefead2207ef7e2aa5dc81a34aedf0cad4c32545
 Update CHANGELOG.md
```

2. Ответьте на вопросы.

* Какому тегу соответствует коммит `85024d3`?

Команда:
```bash
git tag --points-at 85024d3
```
Вывод:
```bash
v0.12.23
```

* Сколько родителей у коммита `b8d720`? Напишите их хеши.

Команда:
```bash
git show b8d720^ --format=%p
```
Вывод:
```bash
58dcac4b79 ffbcf55817
```

* Перечислите хеши и комментарии всех коммитов, которые были сделаны между тегами  v0.12.23 и v0.12.24.

Команда:
```bash
git log --pretty=format:' %H %s' v0.12.23..v0.12.24^
```
Вывод:
```bash
 b14b74c4939dcab573326f4e3ee2a62e23e12f89 [Website] vmc provider links
 3f235065b9347a758efadc92295b540ee0a5e26e Update CHANGELOG.md
 6ae64e247b332925b872447e9ce869657281c2bf registry: Fix panic when server is unreachable
 5c619ca1baf2e21a155fcdb4c264cc9e24a2a353 website: Remove links to the getting started guide's old location
 06275647e2b53d97d4f0a19a0fec11f6d69820b5 Update CHANGELOG.md
 d5f9411f5108260320064349b757f55c09bc4b80 command: Fix bug when using terraform login on Windows
 4b6d06cc5dcb78af637bbb19c198faff37a066ed Update CHANGELOG.md
 dd01a35078f040ca984cdd349f18d0b67e486c35 Update CHANGELOG.md
 225466bc3e5f35baa5d07197bbc079345b77525e Cleanup after v0.12.23 release
```

* Найдите коммит, в котором была создана функция `func providerSource`, её определение в коде выглядит так: `func providerSource(...)` (вместо троеточия перечислены аргументы).

Команда:
```bash
git log -S 'func providerSource(' --pretty=oneline
```
Вывод:
```bash
8c928e83589d90a031f811fae52a81be7153e82f main: Consult local directories as potential mirrors of providers
```

* Найдите все коммиты, в которых была изменена функция `globalPluginDirs`.

Это можно выполнить с помощью "git log -L фунция:путь", но для этого необходимо узнать где находится функция.
Команда:
```bash
git grep --break --heading 'func globalPluginDirs'
```
Вывод:
```bash
plugins.go
func globalPluginDirs() []string {
```
Теперь когда мы имеем название файла, можно найти все коммиты, в которых была изменена функция globalPluginDirs
Команда:
```bash
git log -L:'globalPluginDirs':plugins.go --oneline  -q
```
Вывод:
```bash
78b1220558 Remove config.go and update things using its aliases
52dbf94834 keep .terraform.d/plugins for discovery
41ab0aef7a Add missing OS_ARCH dir to global plugin paths
66ebff90cd move some more plugin search path logic to command
8364383c35 Push plugin discovery down into command package
```

* Кто автор функции `synchronizedWriters`? 

Команда:
```bash
git log -S 'func synchronizedWriters' --pretty=format:'%an'
```
Вывод:
```bash
James Bardin
Martin Atkins
```
*В качестве решения ответьте на вопросы и опишите, как были получены эти ответы.*
