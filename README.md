## Laboratory work II

Данная лабораторная работа посвещена изучению систем контроля версий на примере **Git**.
___
## Homework

### Part I


***1.** Создайте пустой репозиторий на сервисе [github.com](https://github.com/).*

```sh
$ cd ~/Xusk/workspace/projects
$ mkdir lab02
$ cd lab02
$ git init
$ git config --global user.name ${GITHUB_USERNAME}
$ git config --global user.email ${GITHUB_EMAIL}
$ git remote add origin https://github.com/${GITHUB_USERNAME}/lab02.git
$ git pull origin master
$ touch README.md
$ git status
$ git add README.md
$ git commit -m"added README.md"
$ git push origin master
```

***2.** Выполните инструкцию по созданию первого коммита на странице репозитория, созданного на предыдещем шаге.*

Создаём файл `.gitignore`

```sh
$ cat .gitignore  <<EOF
*build*/ 
*install*/
*.swp
.idea/
EOF
```
Загружаем его на GitHub

```sh
$ git add .gitignore
$ git commit -m"created .gitignore"
$ git push origin master
```

***3.** Создайте файл `hello_world.cpp` в локальной копии репозитория (который должен был появиться на шаге 2). Реализуйте программу **Hello world** на языке C++ используя плохой стиль кода. Например, после заголовочных файлов вставьте строку `using namespace std;`.*

```sh
$ cat > sources/hello_world.cpp <<EOF
#include <iostream>
using namespace std;
int main(int argc, char** argv){cout << "Hello world from User-XXI" << endl; return 0;}
EOF
```

***4.** Добавьте этот файл в локальную копию репозитория.*

```sh
$ git add sources/hello_world.cpp
```

***5.** Закоммитьте изменения с *осмысленным* сообщением.*

```sh
$ git commit -m"added hello_world.cpp"
```

***6.** Изменитьте исходный код так, чтобы программа через стандартный поток ввода запрашивалось имя пользователя. А в стандартный поток вывода печаталось сообщение `Hello world from @name`, где `@name` имя пользователя.*

```sh
$ cat > sources/hello_world.cpp <<EOF
#include <iostream>
#include <string>
using namespace std;
int main(int argc, char** argv)
{
string name;
cout << "Input user_name";
cin >> name;
cout << "Hello world from " << name << endl; 
return 0;
}
EOF
```

***7.** Закоммитьте новую версию программы. Почему не надо добавлять файл повторно `git add`?*

```sh
$ git commit sources/hello_world.cpp -m"Changed hello_world.cpp"
```
*Т.к. мы не загрузили файл на GitHub и фактически продолжаем с ним работать, то можно обойтись без повторного использования git add*


***8.** Запуште изменения в удалёный репозиторий.*

```sh
$ git push origin master
```

***9.** Проверьте, что история коммитов доступна в удалёный репозитории.*
___
### Part II

**Note:** *Работать продолжайте с теми же репоззиториями, что и в первой части задания.*

***1.** В локальной копии репозитория создайте локальную ветку `patch1`.*
```bash
$ git checkout -b patch1
```

***2.** Внесите изменения в ветке `patch1` по исправлению кода и избавления от `using namespace std;`.*

```bash
$ cat > sources/hello_world.cpp <<EOF
#include <iostream>
#include <string>

int main(int argc, char** argv)
{
    std::string name;
    std::cout << "Input user_name";
    std::cin >> name;
    std::cout << "Hello world from " << name << std::endl;
    return 0;
}

EOF
```

***3.** **commit**, **push** локальную ветку в удалённый репозиторий.*

```bash
$ git status
$ git add examples
$ git commit -m"Created examples"
$ git add include
$ git commit -m"Created include"
$ git add sources
$ git commit -m"Created sources"
$ git push origin patch1
```
Вывод команды:

<details>

```bash
Username for 'https://github.com': lXuskl
Password for 'https://lXuskl@github.com': 
Перечисление объектов: 7, готово.
Подсчет объектов: 100% (7/7), готово.
При сжатии изменений используется до 12 потоков
Сжатие объектов: 100% (4/4), готово.
Запись объектов: 100% (4/4), 488 байтов | 488.00 КиБ/с, готово.
Всего 4 (изменения 1), повторно использовано 0 (изменения 0)
remote: Resolving deltas: 100% (1/1), completed with 1 local object.
remote: 
remote: Create a pull request for 'patch1' on GitHub by visiting:
remote:      https://github.com/lXuskl/lab02/pull/new/patch1
remote: 
To https://github.com/lXuskl/lab02.git
 * [new branch]      patch1 -> patch1

```
</details>

***4.** Проверьте, что ветка `patch1` доступна в удалёный репозитории.*


***5.** Создайте pull-request `patch1 -> master`.*


***6.** В локальной копии в ветке `patch1` добавьте в исходный код комментарии.*

```bash
$ cat > sources/hello_world.cpp <<EOF
#include <iostream>
#include <string>

int main(int argc, char** argv)
{
    std::string name; // Инициальзируем переменную name типа string
    std::cout << "Input user_name"; // Просим ввести имя пользователя
    std::cin >> name; // Запрашиваем значение переменной name из потока ввода вывода
    std::cout << "Hello world from " << name << std::endl; // Выводим преветствие
    return 0;
}

EOF
```
***7.** **commit**, **push**.*

```bash
$ git status
$ git commit -a -m"Added comments"
$ git push origin patch1
```

***8.** Проверьте, что новые изменения есть в созданном на **шаге 5** pull-request*


***9.** В удалённый репозитории выполните  слияние PR `patch1 -> master` и удалите ветку `patch1` в удаленном репозитории.*


***10.** Локально выполните **pull**.*

```bash
$ git pull origin master
```

Вывод программы

<details>

```bash
remote: Enumerating objects: 1, done.
remote: Counting objects: 100% (1/1), done.
remote: Total 1 (delta 0), reused 0 (delta 0), pack-reused 0
Распаковка объектов: 100% (1/1), 615 байтов | 615.00 КиБ/с, готово.
Из https://github.com/lXuskl/lab02
 * branch            master     -> FETCH_HEAD
   22f2f91..d94ea28  master     -> origin/master
Обновление 9d28bd6..d94ea28
Fast-forward

```

</details>

***11.** С помощью команды **git log** просмотрите историю в локальной версии ветки `master`.*

```bash
$ git log
```
Вывод программы

<details>

```bash
commit d94ea281e5c3ba4798ea4e37ba506ded03e6a8cb (HEAD -> patch1, origin/master)
Merge: 22f2f91 9d28bd6
Author: lXuskl <91723557+lXuskl@users.noreply.github.com>
Date:   Mon Mar 21 23:15:10 2022 +0300

    Merge pull request #1 from lXuskl/patch1
    
    Patch1

commit 9d28bd68a0644820d4d2faebc75220d37e0715c3
Merge: 6cb98c5 4b57726
Author: lXuskl <stalkercomiunity228@gmail.com>
Date:   Mon Mar 21 23:14:14 2022 +0300

    Added comments

commit 6cb98c59bfff061bc44a925373abec0a0471a5bf
Author: lXuskl <stalkercomiunity228@gmail.com>
Date:   Mon Mar 21 23:10:35 2022 +0300

    Added comments

commit 4b577263272d680ba31d668ca372498fe50940d0
Author: lXuskl <91723557+lXuskl@users.noreply.github.com>
Date:   Mon Mar 21 23:09:14 2022 +0300

    Update hello_world.cpp

commit 63bf3709a98d3c3bdf13cf7e4ff9aa4e1432a7a9
Author: lXuskl <91723557+lXuskl@users.noreply.github.com>
Date:   Mon Mar 21 23:03:36 2022 +0300

    Update hello_world.cpp

commit 0efb8f0663b17528bebd3391d70e1aef952c3fbf
Author: lXuskl <stalkercomiunity228@gmail.com>
Date:   Mon Mar 21 22:59:59 2022 +0300

    Added comments

commit ca15ba3be069fe902a7b6e8644cedd1b112c1e35
Author: lXuskl <stalkercomiunity228@gmail.com>
Date:   Mon Mar 21 22:57:24 2022 +0300

    Created examples

commit 22f2f91707eb441802126b66137c97f2a6897e9d (master)
Author: lXuskl <stalkercomiunity228@gmail.com>
Date:   Mon Mar 21 22:55:48 2022 +0300

    Changed hello_world.cpp

commit 87e6e49a7fb5b87c20b1a720a8bc6f10d61a0702
Author: lXuskl <stalkercomiunity228@gmail.com>
Date:   Mon Mar 21 22:53:48 2022 +0300

    added hello_world.cpp

commit e722bef7066119ca4206a81a77362f70c98a1965
Author: lXuskl <91723557+lXuskl@users.noreply.github.com>
Date:   Mon Mar 21 22:45:27 2022 +0300

    Create .gitignore

commit c6706632826763774afc34b9b06c51d0d9640643
Author: lXuskl <stalkercomiunity228@gmail.com>
Date:   Mon Mar 21 22:40:36 2022 +0300

    added sources

commit d02b53a795f65d766f6795910bc1ef5d16b2c58d (origin/main)
Author: lXuskl <91723557+lXuskl@users.noreply.github.com>
Date:   Mon Mar 21 22:19:39 2022 +0300

    Initial commit

commit d94ea281e5c3ba4798ea4e37ba506ded03e6a8cb (HEAD -> patch1, origin/master)
Merge: 22f2f91 9d28bd6
Author: lXuskl <91723557+lXuskl@users.noreply.github.com>
Date:   Mon Mar 21 23:15:10 2022 +0300

    Merge pull request #1 from lXuskl/patch1
    
    Patch1

commit 9d28bd68a0644820d4d2faebc75220d37e0715c3
Merge: 6cb98c5 4b57726
Author: lXuskl <stalkercomiunity228@gmail.com>
Date:   Mon Mar 21 23:14:14 2022 +0300

    Added comments

commit 6cb98c59bfff061bc44a925373abec0a0471a5bf
Author: lXuskl <stalkercomiunity228@gmail.com>
Date:   Mon Mar 21 23:10:35 2022 +0300

    Added comments

commit 4b577263272d680ba31d668ca372498fe50940d0
...skipping...
commit d94ea281e5c3ba4798ea4e37ba506ded03e6a8cb (HEAD -> patch1, origin/master)
Merge: 22f2f91 9d28bd6
Author: lXuskl <91723557+lXuskl@users.noreply.github.com>
Date:   Mon Mar 21 23:15:10 2022 +0300

    Merge pull request #1 from lXuskl/patch1
    
    Patch1

commit 9d28bd68a0644820d4d2faebc75220d37e0715c3
Merge: 6cb98c5 4b57726
Author: lXuskl <stalkercomiunity228@gmail.com>
Date:   Mon Mar 21 23:14:14 2022 +0300

    Added comments

commit 6cb98c59bfff061bc44a925373abec0a0471a5bf
Author: lXuskl <stalkercomiunity228@gmail.com>
Date:   Mon Mar 21 23:10:35 2022 +0300

    Added comments

commit 4b577263272d680ba31d668ca372498fe50940d0
...skipping...

                   SUMMARY OF LESS COMMANDS

      Commands marked with * may be preceded by a number, N.
      Notes in parentheses indicate the behavior if N is given.
      A key preceded by a caret indicates the Ctrl key; thus ^K is ctrl-K.

  h  H                 Display this help.
  q  :q  Q  :Q  ZZ     Exit.
 ---------------------------------------------------------------------------

                           MOVING

  e  ^E  j  ^N  CR  *  Forward  one line   (or N lines).
  y  ^Y  k  ^K  ^P  *  Backward one line   (or N lines).
  f  ^F  ^V  SPACE  *  Forward  one window (or N lines).
  b  ^B  ESC-v      *  Backward one window (or N lines).
  z                 *  Forward  one window (and set window to N).
  w                 *  Backward one window (and set window to N).
  ESC-SPACE         *  Forward  one window, but don't stop at end-of-file.
  d  ^D             *  Forward  one half-window (and set half-window to N).
  u  ^U             *  Backward one half-window (and set half-window to N).
  ESC-)  RightArrow *  Right one half screen width (or N positions).

                   SUMMARY OF LESS COMMANDS

      Commands marked with * may be preceded by a number, N.
      Notes in parentheses indicate the behavior if N is given.
      A key preceded by a caret indicates the Ctrl key; thus ^K is ctrl-K.

  h  H                 Display this help.
  q  :q  Q  :Q  ZZ     Exit.
 ---------------------------------------------------------------------------

                           MOVING

  e  ^E  j  ^N  CR  *  Forward  one line   (or N lines).
  y  ^Y  k  ^K  ^P  *  Backward one line   (or N lines).
  f  ^F  ^V  SPACE  *  Forward  one window (or N lines).
  b  ^B  ESC-v      *  Backward one window (or N lines).
  z                 *  Forward  one window (and set window to N).
  w                 *  Backward one window (and set window to N).
  ESC-SPACE         *  Forward  one window, but don't stop at end-of-file.
  d  ^D             *  Forward  one half-window (and set half-window to N).
  u  ^U             *  Backward one half-window (and set half-window to N).
  ESC-)  RightArrow *  Right one half screen width (or N positions).
  ESC-(  LeftArrow  *  Left  one half screen width (or N positions).
  ESC-}  ^RightArrow   Right to last column displayed.
  ESC-{  ^LeftArrow    Left  to first column.
HELP -- Press RETURN for more, or q when done...skipping...
commit d94ea281e5c3ba4798ea4e37ba506ded03e6a8cb (HEAD -> patch1, origin/master)
Merge: 22f2f91 9d28bd6
Author: lXuskl <91723557+lXuskl@users.noreply.github.com>
Date:   Mon Mar 21 23:15:10 2022 +0300

    Merge pull request #1 from lXuskl/patch1
    
    Patch1

commit 9d28bd68a0644820d4d2faebc75220d37e0715c3
Merge: 6cb98c5 4b57726
Author: lXuskl <stalkercomiunity228@gmail.com>
Date:   Mon Mar 21 23:14:14 2022 +0300

    Added comments

commit 6cb98c59bfff061bc44a925373abec0a0471a5bf
Author: lXuskl <stalkercomiunity228@gmail.com>
Date:   Mon Mar 21 23:10:35 2022 +0300

    Added comments

```

</details>

***12.** Удалите локальную ветку `patch1`.*

```bash
$ git branch -d patch1
Ветка patch1 удалена (была d94ea28).
```
___

