## Настройки проекта

### * Вкратце и поверхностно, на коленке написано :3 Обязательно пройдись по всем ссылкам — в каждой есть информация, которая может помочь именно в твоём кейсе.

### Специальные зарезервированные папки проекта Unity

У Unity есть много специальных зарезервированных папок, две из них напрямую могут влиять на размер сборки.
Что бы ни лежало в папках StreamingAssets и Resources, оно попадёт в билд. Поэтому:
- [ ] Папка **StreamingAssets** (если есть) — нужно убрать из неё всё лишнее.
- [ ] Папки **Resources** (если есть) — нужно убрать из них всё лишнее.

### Ограничение размера спрайтов и текстур в редакторе
- [ ] Ограничить все ресурсы проекта, включая readonly плагины, до 512х512 или 1024х1024.
  <img width="684" alt="Pasted image 20241227150757" src="https://github.com/user-attachments/assets/2bafd128-4844-4f88-86fc-efc70c6fcb1d" />

### Build Settings
- [ ] Режим упаковки кода (Code Optimization) ставь **Disk Size** или **Disk Size LTO**.
  <img width="689" alt="Pasted image 20241227150936" src="https://github.com/user-attachments/assets/d5d0f7d4-d9c2-4563-bb22-f568b39ff29a" />

- [ ] Удали лишние или неиспользуемые сцены из **Scenes in Build**, так как они добавляются в билд.
  <img width="683" alt="Pasted image 20241227151104" src="https://github.com/user-attachments/assets/4acafb9e-087b-400b-99ef-39b3a9392b46" />

- [ ] В **IL2Cpp Code Generation** выбери режим **Faster (smaller) builds**.
  <img width="681" alt="Pasted image 20241227151231" src="https://github.com/user-attachments/assets/3cc22881-514d-4b70-bf1c-fa129be1324a" />

- [ ] Протестируй режим GZip для своего проекта. Если размер сборки уменьшился, оставь его, если увеличился — выбери Brotli. Это зависит от проекта.
  <img width="668" alt="Pasted image 20241227151548" src="https://github.com/user-attachments/assets/f96902b4-785f-44dd-bc03-9692325b501e" />

- [ ] Удаление или отключение лишних пакетов значительно уменьшит вес игры.
  <img width="692" alt="Pasted image 20241227153331" src="https://github.com/user-attachments/assets/90ffb13b-80a9-4c40-bf84-4e604c7d01dc" />

- [ ] В папке **Packages** есть файл `manifest.json`. Удали из него лишние строки.
  Вот пример, выделенные строки можно удалить. Однако это только пример — нужно удалить вообще всё лишнее.
  <img width="848" alt="Pasted image 20241227153549" src="https://github.com/user-attachments/assets/5ec67380-a43b-499a-9c85-54c9b0738514" />

- [ ] Для релизной сборки или минимального размера рекомендуется собирать проект как clean build, пример ниже.
  <img width="824" alt="Pasted image 20241227153751" src="https://github.com/user-attachments/assets/4dea149d-981a-4893-b2a8-cae13b125592" />

---

## Assets (Ассеты)

### **Audio**
Для WebGL параметр **Load Type** должен быть установлен на **Decompression On Load**, иначе работа на WebGL не гарантируется. Остальные настройки на твоё усмотрение. Видео ниже покажет, как именно можно оптимизировать аудио.
- [ ] Вот пример оптимизации аудио [ссылка](https://www.youtube.com/watch?v=r19FVjZYMAM)

### **Sprites**
Важно, чтобы все изображения:
- [ ] Оптимизировались через атласы и правильные настройки. Пример [видео](https://youtu.be/ex9Ie8KcIEM).
- [ ] Видео на YouTube от Яковлева, часть 1 [ссылка](https://www.youtube.com/watch?v=uJaMrKX0DZg).
- [ ] Видео на YouTube от Яковлева, часть 2 [ссылка](https://www.youtube.com/watch?v=3DBufWKuHeo).

### **Fonts**
Если используешь **TMP Pro**, можно удалить все лишние шрифты из папок плагина, включая те, которые не используются. Они находятся в папке **Resources** плагина, поэтому будут попадать в билд, даже если ты используешь свои. Это сразу сэкономит до 2 мегабайт.
- [ ] Шрифты весят много, вот статья по оптимизации [ссылка](https://vk.com/@-210544836-optimizaciya-proekta-unity).
- [ ] Дополнительная документация от Unity [ссылка](https://docs.unity3d.com/ru/530/Manual/ReducingFilesize.html).

### **External Compress**
- [ ] Все изображения для фонов нужно прогнать через сервисы для уменьшения веса фото.
- [ ] Все видео для фонов нужно прогнать через сервисы для уменьшения веса видео.
- [ ] Все аудио для фонов нужно прогнать через сервисы для уменьшения веса аудио.

### **Environment**
- [ ] Оптимизация моделей: [ссылка](https://www.youtube.com/watch?v=W1JxCJRVjdo).
- [ ] Настройка 3D-моделей (их FBX-файлов): [ссылка](https://www.youtube.com/watch?v=uJaMrKX0DZg) и [ссылка](https://www.youtube.com/watch?v=3DBufWKuHeo).

### **Scene**
- [ ] Все объекты на сцене должны быть префабами или композициями префабов. Иначе Unity будет воспринимать каждый объект как уникальный, что увеличивает размер игры.
- [ ] Если возможно, генерируй окружение через код. Это значительно уменьшит вес сборки, так как объекты не будут заранее созданы и добавлены в сцену.
- [ ] Минимизируй использование сложных физических коллайдеров. Избегай **MeshCollider** и **Tilemap Collider** без **Composite Collider**. Чем больше сложных коллайдеров, тем больше вес сборки. Например, сравни сцену с Tilemap и коллайдером и без него, чтобы увидеть разницу.

---

## Ссылки на статьи по теме
0. [Инструкция по уменьшению веса сборки](https://vk.com/@-210544836-optimizaciya-proekta-unity)
1. Гайд от Кабанчика [ссылка](https://t.me/archivekaban/7)
2. Видео на YouTube от Alex Sosnovskiy [ссылка](https://www.youtube.com/watch?v=oj7-ge_Oi0k)
3. "100 и 1 проблема Unity в WebGL" [ссылка](https://maksimsazanovich.github.io/roundedbox/#100_and_1_problem_of_unity_in_webgl)
4. Видео на YouTube от "Unity без воды" [ссылка](https://www.youtube.com/@Unity3dWithoutWater)
5. Видео на YouTube от Яковлева, часть 1 [ссылка](https://www.youtube.com/watch?v=uJaMrKX0DZg)
6. Видео на YouTube от Яковлева, часть 2 [ссылка](https://www.youtube.com/watch?v=3DBufWKuHeo)