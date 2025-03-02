# Общее описание

Этот пример показывает полносистемный фаззинг ПО архитектуры `x86-64` с помощью модифицированной `QEMU` и скриптов на языке `Lua`.

В поддиректории `app` должна находится виртуальная машина, в которой происходит фаззинг (виртуальная машина доступна вместе с релизом фаззера). Также в этой директории находятся исходники приложения-примера, которое будет фаззиться.
В поддиректории `testing` - скрипты и материалы для запуска эмуляции и фаззинга.

# Фаззинг

Находясь в директории `testing` запустить скрипт `./fuzz.sh`; он принимает один аргумент - путь до `fuzz_manager`.

Запустить в другом терминале `UI` фаззера (укажите актуальные пути):
```shell
/path/to/crusher/bin_x86-64/ui --outdir /path/to/out
```

Как только будут найдены аварийные завершения, значение поля `unique_crashes` (в окне `UI` - наверху справа) станет не нулевым.

Прервать фаззинг (в первом терминале, `Ctrl + C`).

В данном примере фаззер обнаруживает одно уникальное завершение, соответствующее дефекту (см. исходный код).

### Важные замечания
1. В текущий момент полносистеный фаззинг ПО поддерживается только на одном ядре. При попытке запустить фаззинг на нескольких ядрах фаззер работает некорректно
2. В случае ошибки запуска фаззинга имеет смысл попробовать увеличить таймаут ожидания через ключ `-t`

# Эмуляция

Для запуска эмуляции - скрипт `./emulate.sh`; он принимает один аргумент - путь до исполняемого файла `QEMU`;
Входные данные находятся в файле `input`.

QEMU x86-64: `/path/to/crusher/bin_x86-64/QIT/QemuLuaFull/qemu-system-x86_64`

# Воспроизведение аварийного завершения

Записать найденные фаззером вх.данные ав.завершения (например, `out/EAT_OUT/crashes/id_crash_0`)
в файл `input` и запустить эмуляцию (как описано выше).

Более подробное описание см. в документации.
