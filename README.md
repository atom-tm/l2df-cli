# `l2df-cli` - менеджер проектов и сборки

## Задача

К выходу первой релизной версии движка необходимо подготовить свой сборщик и менеджер проектов.
Основные задачи и требования данного инструмента:
- Быстрое и максимально простое создание проектов из пресетов;
- Управление зависимостями и автоматическое докачивание требуемой версии;
- Интеграция со следующими зависимостями: love, luarocks, busted и ldoc;
- Автоматическое добавление / подключение lurker'a для получения hot-reload в режиме разработки;
- Автоматизация сборки с несколькими режимами: love, luac, luajit;
- Сборка под разные платформы и архитектуры: web / linux / windows / osx / android и x86 / x86_64 / ARM;
- Опциональные обфускация, сжатие и минификация кода для создания релизных версий приложений;
- Установка инструмента в систему и добавление в PATH;
- Поддержка файлов-конфигураций для проектов. Например: `mygame.l2df-project`, который является lua-скриптом с описанием проекта и процесса его сборки.

Утилита является частью проекта `L2DF`, однако поставляется отдельно и является опциональной.

Предполагается использование данной утилиты в будущем для создания `l2df-ide` - плагина для Sublime Text и Atom, превращающий их в полноценное IDE для разработки на движке `l2df`.

## Обзор существующих решений

[love] - оптимизировано для love2d, сборка в .love
[min] - минификация кода
[zip] - сжатие кода
[obf] - обфускация / uglify кода (шифрование строк, переименование переменных)
[cc] - компиляция / статическая линковка нативного кода
[bc] - компиляция в байт-код
[pm] - инструменты по управлению проектом и его сборке с помощью конфигураций
[1] - упаковщики скриптов в один файл

* [MIT][1] https://github.com/mihacooper/luacc
* [MIT][1] https://github.com/siffiejoe/lua-amalg
* [MIT][1][pm][cc][bc][min][zip] https://github.com/jirutka/luapak
* [MIT][min][obf][bc][zip] https://github.com/LuaDist/squish
* [MIT][min][obf] https://github.com/jirutka/luasrcdiet
* [MIT][love][zip][bc] https://github.com/MisterDA/love-release
* [MIT][love][zip][pm] https://github.com/camchenry/boon
* [NoLicense][love][bc][zip] https://github.com/Snake174/Love2D-Helpers
* [MIT][pm] https://github.com/stevedonovan/Lake
* [MIT][pm] https://github.com/bkaradzic/GENie
* [СС0-1.0][cc][bc] https://github.com/ers35/luastatic
* [NoLicense][obf] https://github.com/Peepx0/LuaObfuscator

- В GENie именно тот синтаксис конфигурации проекта, который хотелось бы воссоздать
- luapak максимально близок к вышеуказанным требованиям, можно отталквиваться от него и оптимизировать под l2df

## Дополнительно

luarocks - менеджер пакетов, https://github.com/luarocks/luarocks
busted - юнит-тестирование, https://github.com/Olivine-Labs/busted
ldoc - генерация документации, https://github.com/stevedonovan/LDoc
qemu - позволит получить байт-код lua под другой архитектурой, http://lua-users.org/lists/lua-l/2014-04/msg00617.html