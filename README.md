## Laboratory work II

<a href="https://yandex.ru/efir/?stream_id=vMPJl0nEKr_0"><img src="https://raw.githubusercontent.com/tp-labs/lab02/master/preview.png" width="640"/></a>

Данная лабораторная работа посвещена изучению систем контроля версий на примере **Git**.

```bash
$ open https://git-scm.com
```

## Tasks

- [x] 1. Создать публичный репозиторий с названием **lab02** и с лиценцией **MIT**
- [x] 2. Сгенирировать токен для доступа к сервису **GitHub** с правами **repo**
- [x] 3. Ознакомиться со ссылками учебного материала
- [x] 4. Выполнить инструкцию учебного материала
- [x] 5. Составить отчет и отправить ссылку личным сообщением в **Slack**

## Tutorial

```sh
$ export GITHUB_USERNAME=ilvivl #define value GITHUB_USERNAME
$ export GITHUB_EMAIL=vinogradov.iv@phystech.edu #define value GITHUB_EMAIL
$ export GITHUB_TOKEN=****72cf8cdf1c17eb04436711713832c******* #define value GITHUB_TOKEN
$ alias edit=subl #make an alias for the standard editor
```

```sh
$ cd ${GITHUB_USERNAME}/workspace
$ source scripts/activate #read and execute commands
```

```sh
$ mkdir ~/.config
$ cat > ~/.config/hub <<EOF
github.com:
- user: ${GITHUB_USERNAME}
  oauth_token: ${GITHUB_TOKEN}
  protocol: https
EOF
$ git config --global hub.protocol https #change global configuration communication protocol for https, tell the command to read from only that location 
```

```sh
$ mkdir projects/lab02 && cd projects/lab02
$ git init # create an empty Git repository or reinitialize an existing one
Initialized empty Git repository in /home/ilya/Documents/acro/ilvivl/workspace/projects/lab02/.git/
$ git config --global user.name ${GITHUB_USERNAME}
$ git config --global user.email ${GITHUB_EMAIL}
# check your git global settings
$ git config -e --global
[hub]
        protocol = https
[user]
        name = ilvivl
        email = vinogradov.iv@phystech.edu
$ git remote add origin https://github.com/${GITHUB_USERNAME}/lab02.git #adds a remote repository
$ git pull origin master #fetch from and integrate with another repository or a local branch
From https://github.com/ilvivl/lab02
 * branch            master     -> FETCH_HEAD
 * [new branch]      master     -> origin/master
$ touch README.md #change file timestamps
$ git status #show the working tree status
On branch master
nothing to commit, working tree clean
$ git add README.md #add file contents to the index
$ git commit -m"added README.md" #record changes to the repository
On branch master
Untracked files:
	ter

nothing added to commit but untracked files present
$ git push origin master #update remote refs along with associated objects
Username for 'https://github.com': ilvivl
Password for 'https://ilvivl@github.com': 
Everything up-to-date
```

Добавить на сервисе **GitHub** в репозитории **lab02** файл **.gitignore**
со следующем содержимом:

```sh
*build*/
*install*/
*.swp
.idea/
```

```sh
$ git pull origin master
From https://github.com/ilvivl/lab02
 * branch            master     -> FETCH_HEAD
Already up to date.
ilya@ilya-laptop:~/D
$ git log
commit af8687b21746c774d987f07e8d89e3c9a3f821c2 (HEAD -> master, origin/master)
Author: rusdevops <rusdevops@gmail.com>
Date:   Fri Apr 10 14:14:56 2020 +0300

    Update README.md

commit 4162a0f6677e33bf76de5a06cad3385f35ccde43
Author: rusdevops <rusdevops@gmail.com>
Date:   Fri Apr 10 14:14:39 2020 +0300

    Update README.md

commit 7542e7739792b8fcd0dbdfed0e45eb6d7a36c5f8
Author: rusdevops <rusdevops@gmail.com>
Date:   Fri Apr 10 13:46:51 2020 +0300

    Update README.md

commit 2a8a860ea41d9c2c7016cd97d7be44dbd7e2bee0
Author: rusdevops <rusdevops@gmail.com>
Date:   Fri Apr 10 13:27:26 2020 +0300
```

```sh
$ mkdir sources
$ mkdir include
$ mkdir examples
$ cat > sources/print.cpp <<EOF
#include <print.hpp>

void print(const std::string& text, std::ostream& out)
{
  out << text;
}

void print(const std::string& text, std::ofstream& out)
{
  out << text;
}
EOF
```

```sh
$ cat > include/print.hpp <<EOF
#include <fstream>
#include <iostream>
#include <string>

void print(const std::string& text, std::ofstream& out);
void print(const std::string& text, std::ostream& out = std::cout);
EOF
```

```sh
$ cat > examples/example1.cpp <<EOF
#include <print.hpp>

int main(int argc, char** argv)
{
  print("hello");
}
EOF
```

```sh
$ cat > examples/example2.cpp <<EOF
#include <print.hpp>

#include <fstream>

int main(int argc, char** argv)
{
  std::ofstream file("log.txt");
  print(std::string("hello"), file);
}
EOF
```

```sh
$ edit README.md
```

```sh
$ git status
On branch master
Untracked files:
  (use "git add <file>..." to include in what will be committed)

	examples/
	include/
	sources/
	ter

nothing added to commit but untracked files present (use "git add" to track)
$ git add .
$ git commit -m"added sources"
[master 1533de7] added sources
 5 files changed, 268 insertions(+)
 create mode 100644 examples/example1.cpp
 create mode 100644 examples/example2.cpp
 create mode 100644 include/print.hpp
 create mode 100644 sources/print.cpp
 create mode 100644 ter
$ git push origin master
Username for 'https://github.com': ilvivl
Password for 'https://ilvivl@github.com': 
Enumerating objects: 11, done.
Counting objects: 100% (11/11), done.
Delta compression using up to 4 threads
Compressing objects: 100% (8/8), done.
Writing objects: 100% (10/10), 4.50 KiB | 768.00 KiB/s, done.
Total 10 (delta 0), reused 0 (delta 0)
To https://github.com/ilvivl/lab02.git
   af8687b..1533de7  master -> master

```

## Report

```sh
$ cd ~/workspace/
$ export LAB_NUMBER=02
$ git clone https://github.com/tp-labs/lab${LAB_NUMBER}.git tasks/lab${LAB_NUMBER}
Cloning into 'tasks/lab02'...
remote: Enumerating objects: 93, done.
remote: Total 93 (delta 0), reused 0 (delta 0), pack-reused 93
Unpacking objects: 100% (93/93), done.
$ mkdir reports/lab${LAB_NUMBER}
$ cp tasks/lab${LAB_NUMBER}/README.md reports/lab${LAB_NUMBER}/REPORT.md
$ cd reports/lab${LAB_NUMBER}
$ edit REPORT.md
$ gist REPORT.md
```

## Homework

### Part I

1. Создайте пустой репозиторий на сервисе github.com (или gitlab.com, или bitbucket.com).
2. Выполните инструкцию по созданию первого коммита на странице репозитория, созданного на предыдещем шаге.
3. Создайте файл `hello_world.cpp` в локальной копии репозитория (который должен был появиться на шаге 2). Реализуйте программу **Hello world** на языке C++ используя плохой стиль кода. Например, после заголовочных файлов вставьте строку `using namespace std;`.
4. Добавьте этот файл в локальную копию репозитория.
5. Закоммитьте изменения с *осмысленным* сообщением.
6. Изменитьте исходный код так, чтобы программа через стандартный поток ввода запрашивалось имя пользователя. А в стандартный поток вывода печаталось сообщение `Hello world from @name`, где `@name` имя пользователя.
7. Закоммитьте новую версию программы. Почему не надо добавлять файл повторно `git add`?
8. Запуште изменения в удалёный репозиторий.
9. Проверьте, что история коммитов доступна в удалёный репозитории.

### Part II

**Note:** *Работать продолжайте с теми же репоззиториями, что и в первой части задания.*
1. В локальной копии репозитория создайте локальную ветку `patch1`.
2. Внесите изменения в ветке `patch1` по исправлению кода и избавления от `using namespace std;`.
3. **commit**, **push** локальную ветку в удалённый репозиторий.
4. Проверьте, что ветка `patch1` доступна в удалёный репозитории.
5. Создайте pull-request `patch1 -> master`.
6. В локальной копии в ветке `patch1` добавьте в исходный код комментарии.
7. **commit**, **push**.
8. Проверьте, что новые изменения есть в созданном на **шаге 5** pull-request
9. В удалённый репозитории выполните  слияние PR `patch1 -> master` и удалите ветку `patch1` в удаленном репозитории.
10. Локально выполните **pull**.
11. С помощью команды **git log** просмотрите историю в локальной версии ветки `master`.
12. Удалите локальную ветку `patch1`.

### Part III

**Note:** *Работать продолжайте с теми же репоззиториями, что и в первой части задания.*
1. Создайте новую локальную ветку `patch2`.
2. Измените *code style* с помощью утилиты [**clang-format**](http://clang.llvm.org/docs/ClangFormat.html). Например, используя опцию `-style=Mozilla`.
3. **commit**, **push**, создайте pull-request `patch2 -> master`.
4. В ветке **master** в удаленном репозитории измените комментарии, например, расставьте знаки препинания, переведите комментарии на другой язык.
5. Убедитесь, что в pull-request появились *конфликтны*.
6. Для этого локально выполните **pull** + **rebase** (точную последовательность команд, следует узнать самостоятельно). **Исправьте конфликты**.
7. Сделайте *force push* в ветку `patch2`
8. Убедитель, что в pull-request пропали конфликтны. 
9. Вмержите pull-request `patch2 -> master`.

## Links

- [hub](https://hub.github.com/)
- [GitHub](https://github.com)
- [Bitbucket](https://bitbucket.org)
- [Gitlab](https://about.gitlab.com)
- [LearnGitBranching](http://learngitbranching.js.org/)

```
Copyright (c) 2015-2020 The ISC Authors
```
