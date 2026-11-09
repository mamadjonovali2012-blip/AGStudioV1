# AGStudio V1

Билингвальный OpenSCAD-style 3D-моделер. Пишете модель текстовыми командами — получаете 3D-объект, который можно вращать, раскрашивать и экспортировать в STL/OBJ.

Команды дублируются на русском и английском: `box(2)` = `cube(2)` = `куб(2)`.

## Возможности

- **20+ примитивов**: box/куб, cylinder/цилиндр, sphere/шар, capsule/капсула, ellipsoid, pyramid/пирамида, tetra, octahedron/октаэдр, hexagon/гексагон, star/звезда, ring/кольцо, slice, lathe, text/текст, polygon, tube/труба, hemisphere/полусфера.
- **Трансформации**: translate/перенос, rotate/поворот, scale/масштаб, mirror/зеркало, stretch/растяжение, skew/наклон, bend/изгиб, twist/скрутка, taper/сужение, jitter/шум, explode/распад, spiral/спираль, array/массив, wave/волна, project/проекция, clip/отсечение.
- **Составные операции**: union/объединение, difference/вычитание, intersection/пересечение, hull/оболочка.
- **Эффект glitch()** — деформация сетки.
- **Язык**: переменные, функции, циклы `for`, условия `if/else`, 20+ мат. функций (`sin`, `cos`, `lerp`, `rand`, `clo` и т.д.), `echo`.
- **Интерфейс**: редактор с подсветкой синтаксиса, 3D-просмотр с автовращением, каркасный режим, смена цвета, 16 встроенных примеров.
- **Экспорт**: STL и OBJ, сохранение/открытие исходника (`.ags`).

## Быстрый старт

```bash
npm install
npm start          # запуск в Electron
```

## Сборка установщиков

**Windows:**
```bash
npm run dist       # или npx electron-builder --win nsis
```
→ `release/AGStudioV1-Setup-3.0.0.exe`

**Linux:** скрипт `build-linux.sh` (запускать на Linux-машине):
```bash
bash build-linux.sh
```
→ соберёт `.deb`, `.AppImage`, `.rpm`, `.tar.gz` в `release/`.

> На Windows-машине реально собрать только портативные Linux-артефакты:
> `npx electron-builder --linux dir tar.gz`
> → `release/linux-unpacked/` и `release/agstudio-v1-3.0.0-x64.tar.gz`.

`.deb`/`.rpm`/`AppImage` требуют Linux (инструменты `fpm`, `mksquashfs`, права на symlink), поэтому их собирают на Linux-машине скриптом выше.

## Структура

```
electron/            главный процесс, preload, IPC (экспорт/файлы)
src/index.html       интерфейс
src/renderer/        editor.js (редактор), geometry.js (3D), main.js (логика), init.js (примеры)
src/lang/            токенизатор, парсер, интерпретатор, построитель геометрии
```

## Пример

```
// Вертушка
union {
  cylinder(0.15, 1);                 // ось
  for (i = 0; i < 4; i += 1) {
    rotate(0, i * 90, 0)
      translate(1.2, 0.5, 0)
      box(2, 0.1, 0.3);              // лопасть
  }
}
```

## Лицензия

MIT
