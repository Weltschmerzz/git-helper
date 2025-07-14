# Git и командная строка — Конспект по темам

## 📁 Навигация по файловой системе (bash)

```bash
pwd                 # показать текущую директорию
ls                  # список файлов и папок
ls -a               # включая скрытые файлы (например, .git)
ls ~                # содержимое домашней директории
ls ..               # содержимое родительской директории
cd ~                # перейти в домашнюю директорию
cd имя_папки        # перейти в указанную директорию
cd ..               # перейти на уровень выше
cd /c/Users/wayp1/Desktop  # абсолютный путь
```

## 📄 Работа с файлами и папками

```bash
touch file.txt                                # создать файл
touch ../../file.txt                          # создать файл на два уровня выше
touch first-project/data.txt first-project/table.csv  # создать несколько файлов

mkdir dir_name                                 # создать директорию
mkdir -p dir1/dir-inside/dir-deeper-inside     # создать вложенные директории
mkdir ~/my-git-projects                        # создать папку в домашней директории

cp index.html dir/         # копировать файл в директорию
mv data.txt Desktop/test   # переместить файл (или переименовать)
cat myfile.txt             # показать содержимое файла

rm example.txt             # удалить файл
rmdir some-dir             # удалить пустую директорию
rm -r some-dir             # удалить директорию с содержимым
```

## 🔗 Комбинирование команд

```bash
mkdir second-project && cd second-project && touch index.html style.css
# последовательно: создаём папку, переходим в неё, создаём файлы
```

## ⚙️ Настройка Git

```bash
git config --global user.name "User Namovich"       # задать имя
git config --global user.email username@yandex.ru   # задать email
cat ~/.gitconfig                                     # просмотреть конфиг
git config --list                                    # список всех настроек
```

## 🧱 Репозиторий Git

```bash
git init                      # инициализировать репозиторий
rm -rf .git                   # удалить репозиторий ("разгитить")
```

> 🔸 Ключи:
>
> * `-r` — рекурсивно
> * `-f` — принудительно (без подтверждений)

## 📌 Работа с коммитами

```bash
git status                   # статус изменений
git add --all                # добавить все файлы в отслеживание
git add .                    # добавить всё из текущей папки
git add fileName.txt         # добавить конкретный файл
git commit -m "Сообщение"    # создать коммит

git log                      # история коммитов
```

## 🌐 Связь с удалённым репозиторием

```bash
git remote add origin git@github.com:Weltschmerzz/first-project.git  # задать удалённый репозиторий
git remote -v                                                  # список удалённых репозиториев

git push -u origin main     # пуш с установкой отслеживания
```

## 🛡 SSH-ключи

```bash
ls -la .ssh/                   # список ssh ключей в директории
ssh-keygen -t ed25519 -C email       # создать ssh ключ ed25519
ssh-keygen -t rsa -b 4096 -C email   # создать ssh ключ rsa (альтернатива)

ls -a ~/.ssh                   # убедиться, что ключи созданы
cat ~/.ssh/id_rsa.pub          # вывести публичный ключ
clip < ~/.ssh/id_ed25519.pub   # скопировать ключ в буфер обмена
ssh -T git@github.com          # проверить ssh-соединение с GitHub
```

> 🧠 При первом подключении появится сообщение о подлинности хоста.
> Проверка отпечатка ключа GitHub: [https://docs.github.com/en/authentication/keeping-your-account-and-data-secure/githubs-ssh-key-fingerprints](https://docs.github.com/en/authentication/keeping-your-account-and-data-secure/githubs-ssh-key-fingerprints)

## 🔄 Клонирование репозитория

```bash
git clone git@github.com:yandex-praktikum/git-clone-lesson.git  # клонировать репозиторий

git remote -v   # убедиться, что связь с удалённым репозиторием установлена
```

---

> 💡 Этот конспект можно дополнять командами `branch`, `merge`, `checkout`, `stash`, и другими, когда будешь их изучать.

## 🔄 Жизненный цикл файла в Git

```mermaid
flowchart LR
  A[untracked\n(неотслеживаемый)] -->|git add| B[staged\n(в списке на коммит)\n+ tracked]
  B -->|git commit| C[tracked\n(отслеживаемый)]
  C -->|Изменения| D[modified\n(изменённый)]
  D -->|git add| B
  B -->|Изменения| D
  D -->|Ещё изменения| D
  C -->|Изменения| D
```

Git отслеживает состояние каждого файла в репозитории. Состояния могут меняться в зависимости от действий пользователя:

- **`untracked`** — файл существует, но Git его не отслеживает (новый файл).
- **`staged`** — файл добавлен в список на коммит с помощью `git add`.
- **`tracked`** — файл уже закоммичен или хотя бы один раз был в staging.
- **`modified`** — файл изменён после коммита.

> ⚠️ Важно: если вы уже добавили файл в staging и потом снова его изменили — изменения нужно снова добавить с `git add`, иначе в коммит попадёт неактуальная версия.

---

## 🔑 Что такое хеш коммита (commit hash)

Каждый коммит в Git имеет уникальный **SHA-1 хеш** — это длинная строка, которая выглядит примерно так:

```
e3b0c44298fc1c149afbf4c8996fb92427ae41e4
```

Она:
- используется как идентификатор коммита,
- позволяет ссылаться на коммиты в других командах (`git checkout`, `git revert`, `git reset`),
- вычисляется на основе содержимого, времени, родительского коммита и автора.

---

## 🧭 Что такое HEAD

**`HEAD`** — это ссылка на **текущий коммит**, от которого ты сейчас «живёшь и работаешь». Чаще всего HEAD указывает на последнюю версию текущей ветки:

```bash
git show HEAD          # показать последний коммит
git log                # история коммитов
```

> Если ты создаёшь новый коммит — HEAD сдвигается вперёд.

---

## ✍️ Стиль сообщений к коммитам

### Хороший стиль:
- Кратко, по делу и в **повелительном наклонении**, как будто даёшь команду Git.
- На английском — в профессиональной среде это стандарт (если не указано иное).
- Без точки в конце.

#### Примеры:
```
Add login form validation
Fix typo in README
Refactor task manager logic
Update dependencies
```

> Можно добавить больше контекста через пустую строку и второй абзац:
```bash
git commit -m "Fix bug with null pointer" -m "Caused by missing check in TaskManager"
```