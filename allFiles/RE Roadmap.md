## ![📌](https://cdn.jsdelivr.net/joypixels/assets/8.0/png/unicode/64/1f4cc.png "Pushpin    :pushpin:") **Общий роадмап по реверс-инжинирингу**​[](https://yougame.biz/threads/356861/?ysclid=mo8r0bju3a632549215#-pushpin-obshchii-roadmap-po-revers-inzhiniringu "Permanent link")

---

### ![🧱](https://cdn.jsdelivr.net/joypixels/assets/8.0/png/unicode/64/1f9f1.png "Bricks    :bricks:") ЭТАП 1: БАЗА​[](https://yougame.biz/threads/356861/?ysclid=mo8r0bju3a632549215#-bricks-etap-1-baza "Permanent link")

> Понимание того, как работает компьютер на низком уровне.

#### 1. **Основы архитектуры ОС**​[](https://yougame.biz/threads/356861/?ysclid=mo8r0bju3a632549215#-1-osnovy-arkhitektury-os "Permanent link")

- Понимание памяти (stack, heap, data segment)
- Системные вызовы
- Процессы и потоки
- Виртуальная память, адресация

#### 2. **Язык C/C++**​[](https://yougame.biz/threads/356861/?ysclid=mo8r0bju3a632549215#-2-yazyk-c-c "Permanent link")

- Указатели, структуры
- Работа с памятью (`malloc`, `free`, и т.п.)
- Компиляция, линковка, бинарные форматы

#### 3. **Ассемблер x86/x64**​[](https://yougame.biz/threads/356861/?ysclid=mo8r0bju3a632549215#-3-assembler-x86-x64 "Permanent link")

- Регистры, стек
- Инструкции (`mov`, `call`, `jmp`, `cmp`, `ret` и т.д.)
- Соглашения о вызовах (cdecl, stdcall, fastcall)
- ABI/Calling conventions

![📚](https://cdn.jsdelivr.net/joypixels/assets/8.0/png/unicode/64/1f4da.png "Books    :books:") Ресурсы:  

- «PC Assembly Language» — Paul Carter
- «Reverse Engineering for Beginners» — Dennis Yurichev

---

### ![🔍](https://cdn.jsdelivr.net/joypixels/assets/8.0/png/unicode/64/1f50d.png "Magnifying glass tilted left    :mag:") ЭТАП 2: ИНСТРУМЕНТЫ РЕВЕРСА​[](https://yougame.biz/threads/356861/?ysclid=mo8r0bju3a632549215#-magnifying-glass-tilted-left-etap-2-instrumenty-reversa "Permanent link")

> Умение читать и анализировать чужие бинарники.

#### Основные инструменты:​[](https://yougame.biz/threads/356861/?ysclid=mo8r0bju3a632549215#-osnovnyye-instrumenty "Permanent link")

- **IDA Pro / Ghidra / Binary Ninja** — дизассемблирование, декомпиляция
- **x64dbg / OllyDbg** — отладка
- **Radare2 / Cutter** — CLI/GUI дизассемблер
- **Procmon, Process Hacker, API Monitor** — анализ поведения

![🎯](https://cdn.jsdelivr.net/joypixels/assets/8.0/png/unicode/64/1f3af.png "Direct hit    :dart:") Умения:  

- Загрузка бинарника, понимание секций PE/ELF
- Навигация по функциям
- Комментирование и восстановление логики программы
- Нахождение точек входа (entry, main, WinMain и т.п.)

---

### ![🧠](https://cdn.jsdelivr.net/joypixels/assets/8.0/png/unicode/64/1f9e0.png "Brain    :brain:") ЭТАП 3: ОСОЗНАННОЕ ПРИМЕНЕНИЕ​[](https://yougame.biz/threads/356861/?ysclid=mo8r0bju3a632549215#-brain-etap-3-osoznannoye-primeneniye "Permanent link")

> Начинаешь понимать, что делают программы и как они защищены.

#### Темы:​[](https://yougame.biz/threads/356861/?ysclid=mo8r0bju3a632549215#-temy "Permanent link")

- Работа с защитами: Obfuscation, Packing (UPX, VMProtect), Anti-debug
- Распаковка и декриптинг malware
- Символьное выполнение и контроль потока
- Работа с API Windows (WinAPI)

![📚](https://cdn.jsdelivr.net/joypixels/assets/8.0/png/unicode/64/1f4da.png "Books    :books:") Книги:  

- _Practical Malware Analysis_ — Sikorski & Honig
- _The IDA Pro Book_ — Chris Eagle
- _Reversing: Secrets of Reverse Engineering_ — Eilam

---

### ![🎯](https://cdn.jsdelivr.net/joypixels/assets/8.0/png/unicode/64/1f3af.png "Direct hit    :dart:") ЭТАП 4: ПРАКТИКА​[](https://yougame.biz/threads/356861/?ysclid=mo8r0bju3a632549215#-direct-hit-etap-4-praktika "Permanent link")

> Учишься применять знания на деле.

#### ![🔧](https://cdn.jsdelivr.net/joypixels/assets/8.0/png/unicode/64/1f527.png "Wrench    :wrench:") Что делать:​[](https://yougame.biz/threads/356861/?ysclid=mo8r0bju3a632549215#-wrench-chto-delat "Permanent link")

- Решать задачи на CTF (реверс и pwn)
- Участвовать в RE задачах на платформах:
    - Пожалуйста, [авторизуйтесь](https://yougame.biz/login) для просмотра ссылки.
        
        (noad
    - Пожалуйста, [авторизуйтесь](https://yougame.biz/login) для просмотра ссылки.
        
        (noad
    - Пожалуйста, [авторизуйтесь](https://yougame.biz/login) для просмотра ссылки.
        
        (noad
    - Пожалуйста, [авторизуйтесь](https://yougame.biz/login) для просмотра ссылки.
        
        (noad

---

### ![🔐](https://cdn.jsdelivr.net/joypixels/assets/8.0/png/unicode/64/1f510.png "Locked with key    :closed_lock_with_key:") ЭТАП 5: УГЛУБЛЕНИЕ В SECURITY​[](https://yougame.biz/threads/356861/?ysclid=mo8r0bju3a632549215#-locked-with-key-etap-5-uglubleniye-v-security "Permanent link")

> Взлом и защита программ, эксплойтинг, изучение вредоносных ПО.

#### Темы:​[](https://yougame.biz/threads/356861/?ysclid=mo8r0bju3a632549215#-temy-2 "Permanent link")

- Эксплойтинг (stack overflow, format string)
- DEP/ASLR bypass
- Reverse shell, payload injection
- Анализ троянов, руткитов, ботнетов

![📚](https://cdn.jsdelivr.net/joypixels/assets/8.0/png/unicode/64/1f4da.png "Books    :books:") Курсы:  

- RE for Beginners (Dennis Yurichev)
- Malware Unicorn RE101
- OpenSecurityTraining