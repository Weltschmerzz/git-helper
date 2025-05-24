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

