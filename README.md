## Laboratory work IX

Данная лабораторная работа посвещена изучению процесса создания артефактов на примере **Github Release**

```sh
$ open https://help.github.com/articles/creating-releases/
```

## Tasks

- [ok] 1. Создать публичный репозиторий с названием **lab09** на сервисе **GitHub**
- [ok] 2. Ознакомиться со ссылками учебного материала
- [ok] 3. Получить токен для доступа к репозиториям сервиса **GitHub**
- [ok] 4. Выполнить инструкцию учебного материала
- [ok] 5. Составить отчет и отправить ссылку личным сообщением в **Slack**

## Tutorial

```sh
$ export GITHUB_TOKEN=<полученный_токен>         #присваиваем сгенирированный токен в переменную GITHUB_TOKEN
$ export GITHUB_USERNAME=<имя_пользователя>     #присваиваем имя пользователя GitHub в переменную GITHUB_USERNAME
$ export PACKAGE_MANAGER=<пакетный менеджер>   #указываем используемый пакетный менеджер
$ export GPG_PACKAGE_NAME=<gpg2|gpg>          #указываем, в какой утилите будет создаваться ключ
```

```sh
# for *-nix system
$ $PACKAGE_MANAGER install xclip                     #скачиваем утилиту xclip
Updating Homebrew...
==> Auto-updated Homebrew!
....................................
$ alias gsed=sed                                    #заменяем команду sed на gsed
$ alias pbcopy='xclip -selection clipboard'        #заменяем команду pbcopy на xclip -selection clipboard
$ alias pbpaste='xclip -selection clipboard -o'   #заменяем команду pbpaste на xclip -selection clipboard -o
```

```sh
$ cd ${GITHUB_USERNAME}/workspace                #спускаемся в workspace
$ pushd .                                       #добавляем в стек текущий каталог
$ source scripts/activate                      #выполняем скрипт
$ go get github.com/aktau/github-release      #скачивание и установка пакета Go, для работы с релизами Github
go: downloading github.com/aktau/github-release v0.10.0
go: downloading github.com/dustin/go-humanize v1.0.0
go: downloading github.com/voxelbrain/goptions v0.0.0-20180630082107-58cddc247ea2
go: downloading github.com/github-release/github-release v0.10.0
go: downloading github.com/tomnomnom/linkheader v0.0.0-20180905144013-02ca5825eb80
go: downloading github.com/kevinburke/rest v0.0.0-20210506044642-5611499aa33c
```

```sh
$ git clone https://github.com/${GITHUB_USERNAME}/lab08 projects/lab09   #клонируем репозиторий из lab08 в директорию projects/lab09
$ cd projects/lab09                                                     #переходим директорию projects/lab09
$ git remote remove origin                                            #удаляем старую ссылку репозитория
$ git remote add origin https://github.com/${GITHUB_USERNAME}/lab09  #добавляем ссылку репозитория в управление репозиториями
```

```sh
$ gsed -i -e 's/lab08/lab09/g' README.md                #поменяем в README.md все строки lab08 на lab09
```

```sh
$ $PACKAGE_MANAGER install ${GPG_PACKAGE_NAME}         #устанавливаем программу GPG для шифрования информации и создания электронных цифровых подписей
==> Downloading https://ghcr.io/v2/homebrew/core/gmp/manifests/6.2.1
######################################################################## 100.0%
==> Downloading ................................................................
$ gpg --list-secret-keys --keyid-format LONG           #проверяем на наличие ранее созданных ключей
gpg: создан каталог '/Users/user/.gnupg'
gpg: создан щит с ключами '/Users/user/.gnupg/pubring.kbx'
gpg: /Users/user/.gnupg/trustdb.gpg: создана таблица доверия
$ gpg --full-generate-key                                 #гененрируем ключ
gpg (GnuPG) 2.3.1; Copyright (C) 2021 Free Software Foundation, Inc.
This is free software: you are free to change and redistribute it.
There is NO WARRANTY, to the extent permitted by law.

Выберите тип ключа:
   (1) RSA and RSA
   (2) DSA and Elgamal
   (3) DSA (sign only)
   (4) RSA (sign only)
   (9) ECC (sign and encrypt) *default*
  (10) ECC (только для подписи)
  (14) Existing key from card
Ваш выбор? 1
длина ключей RSA может быть от 1024 до 4096.
Какой размер ключа Вам необходим? (3072) 1025
Запрошенный размер ключа - 1025 бит
округлен до 1056 бит
Выберите срок действия ключа.
         0 = не ограничен
      <n>  = срок действия ключа - n дней
      <n>w = срок действия ключа - n недель
      <n>m = срок действия ключа - n месяцев
      <n>y = срок действия ключа - n лет
Срок действия ключа? (0) 5
Ключ действителен до четверг,  3 июня 2021 г. 21:17:41 MSK
Все верно? (y/N) y 
GnuPG должен составить идентификатор пользователя для идентификации ключа.
Ваше полное имя: Ivan
Имя не должно быть короче 5 символов   #Обидно
Ваше полное имя: Vanusha
Адрес электронной почты: melihovivan936@gmail.com
Примечание: for tutorial
Вы выбрали следующий идентификатор пользователя:
    "Vanusha (for tutorial) <melihovivan936@gmail.com>"

Сменить (N)Имя, (C)Примечание, (E)Адрес; (O)Принять/(Q)Выход? O
Необходимо получить много случайных чисел. Желательно, чтобы Вы
в процессе генерации выполняли какие-то другие действия (печать
на клавиатуре, движения мыши, обращения к дискам); это даст генератору
случайных чисел больше возможностей получить достаточное количество энтропии.

gpg: ключ #NUMBERKEY# помечен как абсолютно доверенный
gpg: создан каталог '/Users/user/.gnupg/openpgp-revocs.d'
gpg: сертификат отзыва записан в '/Users/user/.gnupg/openpgp-revocs.d/#KEY DIRECTORY#.rev'.
открытый и секретный ключи созданы и подписаны.

pub   rsa1056 2021-05-29 [SC] [   годен до: 2021-06-03]
      #KEY DIRECTORY#
uid                      Vanusha (for tutorial) <melihovivan936@gmail.com>
sub   rsa1056 2021-05-29 [E] [   годен до: 2021-06-03]


$ gpg --list-secret-keys --keyid-format LONG     #выводим в консоль сгенерированный ключ
gpg: проверка таблицы доверия
gpg: marginals needed: 3  completes needed: 1  trust model: pgp
gpg: глубина: 0  достоверных:   1  подписанных:   0  доверие: 0-, 0q, 0n, 0m, 0f, 1u
gpg: срок следующей проверки таблицы доверия 2021-06-03
/Users/user/.gnupg/pubring.kbx
------------------------------
sec   rsa1056/#NUMBERKEY# 2021-05-29 [SC] [   годен до: 2021-06-03]
      #KEY DIRECTORY#
uid               [  абсолютно ] Vanusha (for tutorial) <melihovivan936@gmail.com>
ssb   rsa1056/#2NUMBERKEY2# 2021-05-29 [E] [   годен до: 2021-06-03]

$ GPG_KEY_ID=$(gpg --list-secret-keys --keyid-format LONG | grep ssb | tail -1 | awk '{print $2}' | awk -F'/' '{print $2}') # cоздаем переменной окружения с сохраненным в ней публичным ключом
$ GPG_SEC_KEY_ID=$(gpg --list-secret-keys --keyid-format LONG | grep sec | tail -1 | awk '{print $2}' | awk -F'/' '{print $2}') #cоздаем переменной окружения с сохраненным в ней секретным ключом
$ gpg --armor --export ${GPG_KEY_ID} | pbcopy  #выводим ключ в ASCII
Error: Can't open display: (null)
$ pbpaste                                    #копируем ключ в буфер
Error: Can't open display: (null)
$ open https://github.com/settings/keys         #открываем Github ключ
$ git config user.signingkey ${GPG_SEC_KEY_ID} #добавляем секретный ключ в Github
$ git config gpg.program gpg
```

```sh
# Настраиваем скрипт для добавления сообщения к тегу
$ test -r ~/.bash_profile && echo 'export GPG_TTY=$(tty)' >> ~/.bash_profile
$ echo 'export GPG_TTY=$(tty)' >> ~/.profile
```

```sh
$ cmake -H. -B_build -DCPACK_GENERATOR="TGZ"    #генерируем пакет с раширением .tar.gz
$ cmake --build _build --target package        #запускаем сборку package
```

```sh
$ travis login --auto         #авторизируемся на travis
$ travis enable              #делаем проект доступным
```

```sh
$ git tag -s v0.1.0.0                   #создаем тега с сообщением с информацией
$ git tag -v v0.1.0.0                  #верифицируем тег
$ git show v0.1.0.0                   #посмотрим изменения
$ git push origin master --tags      #отправляем измения на Github
```

```sh
$ github-release --version              #узнаем версию
$ github-release info -u ${GITHUB_USERNAME} -r lab09
$ github-release release \              #создаем релиза
    --user ${GITHUB_USERNAME} \
    --repo lab09 \
    --tag v0.1.0.0 \
    --name "libprint" \
    --description "my first release"
```

```sh
#Добавим артефакт с указанием ОС и архитектуры, на которых происходила компиляция библиотеки
$ export PACKAGE_OS=`uname -s` PACKAGE_ARCH=`uname -m`        #
$ export PACKAGE_FILENAME=print-${PACKAGE_OS}-${PACKAGE_ARCH}.tar.gz       #
$ github-release upload \       #
    --user ${GITHUB_USERNAME} \
    --repo lab09 \
    --tag v0.1.0.0 \
    --name "${PACKAGE_FILENAME}" \
    --file _build/*.tar.gz
```

```sh
$ github-release info -u ${GITHUB_USERNAME} -r lab09 
$ wget https://github.com/${GITHUB_USERNAME}/lab09/releases/download/v0.1.0.0/${PACKAGE_FILENAME}  #скачаем артефакт
$ tar -ztf ${PACKAGE_FILENAME}                                                                    #выводим на экран содержимого архива
```

## Report

```sh
$ popd                                                                           #удаляем из стека текущий каталог
$ export LAB_NUMBER=09                                                          #присваиваем 09 в переменную LAB_NUMBER
$ git clone https://github.com/tp-labs/lab${LAB_NUMBER} tasks/lab${LAB_NUMBER} #клонируем из ссылки в директорию (в нашем случае-tasks/lab09)
$ mkdir reports/lab${LAB_NUMBER}                                              #создаем в директории reports папку (в нашем случае- lab09) 
$ cp tasks/lab${LAB_NUMBER}/README.md reports/lab${LAB_NUMBER}/REPORT.md     #копируем из одной директории в другую
$ cd reports/lab${LAB_NUMBER}                                               #спускаемся в директорию (в наше случае- lab09)
$ edit REPORT.md                                                           #редактируем REPORT.md
$ gistup -m "lab${LAB_NUMBER}"
```

## Links

- [Create Release](https://help.github.com/articles/creating-releases/)
- [Get GitHub Token](https://help.github.com/articles/creating-a-personal-access-token-for-the-command-line/)
- [Signing Commits](https://help.github.com/articles/signing-commits-with-gpg/)
- [Go Setup](http://www.golangbootcamp.com/book/get_setup)
- [github-release](https://github.com/aktau/github-release)

```
Copyright (c) 2015-2021 The ISC Authors
```

