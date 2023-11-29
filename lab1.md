## Національний технічний університет України<br>“Київський політехнічний інститут ім. Ігоря Сікорського”

## Факультет прикладної математики<br>Кафедра системного програмування і спеціалізованих комп’ютерних систем

# Лабораторна робота №1<br>"Базова робота з git"

## КВ-11 Петрук Ольга

~

## Хід виконання роботи

### 1. Зклонувати будь-який невеликий проєкт open-source з github

`Клонуємо двічі: повний репозиторій, а також частковий, що міститиме лише один коміт однієї гілки:`

```
$ git clone https://gitlab.com/CalcProgrammer1/OpenRGB.git
Cloning into 'OpenRGB'...
remote: Enumerating objects: 29699, done.
remote: Counting objects: 100% (1577/1577), done.
remote: Compressing objects: 100% (415/415), done.
remote: Total 29699 (delta 1183), reused 1504 (delta 1140), pack-reused 28122
Receiving objects: 100% (29699/29699), 36.18 MiB | 2.07 MiB/s, done.
Resolving deltas: 100% (21979/21979), done.
```

```
$ git clone https://gitlab.com/CalcProgrammer1/OpenRGB --depth=1 --single-branch --branch=qmk_sonix openrgb-shallow
Cloning into 'openrgb-shallow'...
warning: redirecting to https://gitlab.com/CalcProgrammer1/OpenRGB.git/
remote: Enumerating objects: 861, done.
remote: Counting objects: 100% (861/861), done.
remote: Compressing objects: 100% (686/686), done.
remote: Total 861 (delta 242), reused 400 (delta 153), pack-reused 0
Receiving objects: 100% (861/861), 23.50 MiB | 2.05 MiB/s, done.
Resolving deltas: 100% (242/242), done.
```

`Поглянемо на різницю в розмірі баз даних двох клонів:`

```
$ du -sh ./*/.git
38M     ./OpenRGB/.git
24M     ./openrgb-shallow/.git
```

### 2. Зробити не менше трьох локальних комітів

Внесено зміни у існуючий в репозиторії файл `main.cpp`.
Сворено новий файл `1.txt` з будь-яким текстом.

```
$ git status
On branch qmk_sonix
Your branch is up to date with 'origin/qmk_sonix'.

Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git restore <file>..." to discard changes in working directory)
        modified:   main.cpp

Untracked files:
  (use "git add <file>..." to include in what will be committed)
        1.txt

no changes added to commit (use "git add" and/or "git commit -a")
```

```
$ git status -uno
On branch qmk_sonix
Your branch is up to date with 'origin/qmk_sonix'.

Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git restore <file>..." to discard changes in working directory)
        modified:   main.cpp

no changes added to commit (use "git add" and/or "git commit -a")
```

```
$ git commit -am "added changes to main.cpp"
[qmk_sonix 8a720aa] added changes to main.cpp
 1 file changed, 2 insertions(+)
```

```
$ git status
On branch qmk_sonix
Your branch is ahead of 'origin/qmk_sonix' by 1 commit.
  (use "git push" to publish your local commits)

Untracked files:
  (use "git add <file>..." to include in what will be committed)
        1.txt

nothing added to commit but untracked files present (use "git add" to track)
```

```
$ git add 1.txt

$ git status
On branch qmk_sonix
Your branch is ahead of 'origin/qmk_sonix' by 1 commit.
  (use "git push" to publish your local commits)

Changes to be committed:
  (use "git restore --staged <file>..." to unstage)
        new file:   1.txt

$ git commit -m 'created 1.txt'
[qmk_sonix ce1183a] created 1.txt
 1 file changed, 1 insertion(+)
 create mode 100644 1.txt
```

Створено файли `2.txt` та `3.txt`.

```
$ git add .

$ git commit -m 'added 2.txt and 3.txt'
[qmk_sonix 9c7de60] added 2.txt and 3.txt
 2 files changed, 2 insertions(+)
 create mode 100644 2.txt
 create mode 100644 3.txt
```

### 3. Продемонструвати уміння вносити зміни до останнього коміту за допомогою опції --amend.

Створено файл `4.txt`.

```
$ git status
On branch qmk_sonix
Your branch is ahead of 'origin/qmk_sonix' by 3 commits.
  (use "git push" to publish your local commits)

Untracked files:
  (use "git add <file>..." to include in what will be committed)
        4.txt

nothing added to commit but untracked files present (use "git add" to track)

$ git add 4.txt

$ git commit --amend -m "added 2.txt, 3.txt and 4.txt"
[qmk_sonix 2632ba0] added 2.txt, 3.txt and 4.txt
 Date: Wed Nov 29 14:28:10 2023 +0200
 3 files changed, 3 insertions(+)
 create mode 100644 2.txt
 create mode 100644 3.txt
 create mode 100644 4.txt

 $ git status
On branch qmk_sonix
Your branch is ahead of 'origin/qmk_sonix' by 3 commits.
  (use "git push" to publish your local commits)

nothing to commit, working tree clean
```

### 4. Продемонструвати уміння об'єднати кілька останніх комітів в один за допомогою git reset.

```
$ git reset HEAD~2

$ git status
On branch qmk_sonix
Your branch is ahead of 'origin/qmk_sonix' by 1 commit.
  (use "git push" to publish your local commits)

Untracked files:
  (use "git add <file>..." to include in what will be committed)
        1.txt
        2.txt
        3.txt
        4.txt

nothing added to commit but untracked files present (use "git add" to track)

$  git reset HEAD~1
Unstaged changes after reset:
M       main.cpp

$ git status
On branch qmk_sonix
Your branch is up to date with 'origin/qmk_sonix'.

Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git restore <file>..." to discard changes in working directory)
        modified:   main.cpp

Untracked files:
  (use "git add <file>..." to include in what will be committed)
        1.txt
        2.txt
        3.txt
        4.txt

no changes added to commit (use "git add" and/or "git commit -a")
```

```
$ git add .

$ git commit -m 'created 4 txt files'
[qmk_sonix 723c827] created 4 txt files
 5 files changed, 6 insertions(+)
 create mode 100644 1.txt
 create mode 100644 2.txt
 create mode 100644 3.txt
 create mode 100644 4.txt
```

### 5. Видалити файл(и) одним способом на вибір.

```
$ rm 4.txt

$ git status -uno
On branch qmk_sonix
Your branch is ahead of 'origin/qmk_sonix' by 1 commit.
  (use "git push" to publish your local commits)

Changes not staged for commit:
  (use "git add/rm <file>..." to update what will be committed)
  (use "git restore <file>..." to discard changes in working directory)
        deleted:    4.txt

no changes added to commit (use "git add" and/or "git commit -a")

$ git add 4.txt

$ git status -uno
On branch qmk_sonix
Your branch is ahead of 'origin/qmk_sonix' by 1 commit.
  (use "git push" to publish your local commits)

Changes to be committed:
  (use "git restore --staged <file>..." to unstage)
        deleted:    4.txt

Untracked files not listed (use -u option to show untracked files)

$ git commit -m 'deleted 4.txt'
[qmk_sonix c621b18] deleted 4.txt
 1 file changed, 1 deletion(-)
 delete mode 100644 4.txt
```

### 6. Перемістити файл(и) одним способом на вибір.

```
$ mv 1.txt dummy.txt

$  git status -uno
On branch qmk_sonix
Your branch is ahead of 'origin/qmk_sonix' by 2 commits.
  (use "git push" to publish your local commits)

Changes not staged for commit:
  (use "git add/rm <file>..." to update what will be committed)
  (use "git restore <file>..." to discard changes in working directory)
        deleted:    1.txt

no changes added to commit (use "git add" and/or "git commit -a")

$ git add dummy.txt

$  git status -uno
On branch qmk_sonix
Your branch is ahead of 'origin/qmk_sonix' by 2 commits.
  (use "git push" to publish your local commits)

Changes to be committed:
  (use "git restore --staged <file>..." to unstage)
        new file:   dummy.txt

Changes not staged for commit:
  (use "git add/rm <file>..." to update what will be committed)
  (use "git restore <file>..." to discard changes in working directory)
        deleted:    1.txt

Untracked files not listed (use -u option to show untracked files)

$ git add 1.txt

$  git status -uno
On branch qmk_sonix
Your branch is ahead of 'origin/qmk_sonix' by 2 commits.
  (use "git push" to publish your local commits)

Changes to be committed:
  (use "git restore --staged <file>..." to unstage)
        renamed:    1.txt -> dummy.txt

Untracked files not listed (use -u option to show untracked files)

$ git commit -m 'rename 1.txt to dummy.txt'
[qmk_sonix c9dc1d7] rename 1.txt to dummy.txt
 Date: Wed Nov 29 15:26:58 2023 +0200
 1 file changed, 0 insertions(+), 0 deletions(-)
 rename 1.txt => dummy.txt (100%)
```

### 7. Гілкування

1. Створити три гілки, принаймні з одним унікальним комітом кожна
2. Показати уміння переключатися між гілками

```
$ git branch
* qmk_sonix

$ git branch -a
* qmk_sonix
  remotes/origin/qmk_sonix

$  git branch my-branch-1

$ git checkout -b my-branch-2
Switched to a new branch 'my-branch-2'

$ git checkout -b my-branch-3
Switched to a new branch 'my-branch-3'

$ git branch
  my-branch-1
  my-branch-2
* my-branch-3
  qmk_sonix

$ echo "my-branch-3" > 3.txt

$ git add 3.txt

$ git commit -m "changed 3.txt file"
[my-branch-3 a51782a] changed 3.txt file
 1 file changed, 1 insertion(+), 1 deletion(-)

$ git checkout my-branch-2
Switched to branch 'my-branch-2'

$ echo "my-branch-2" > 2.txt

$ git add 2.txt

$ git commit -m "changed 2.txt file"
[my-branch-2 a1f5543] changed 2.txt file
 1 file changed, 1 insertion(+), 1 deletion(-)

 $ git checkout my-branch-1
Switched to branch 'my-branch-1'

$ echo "my-branch-1" > 1.txt

$ git add 1.txt

$ git commit -m "changed 1.txt file"
[my-branch-1 547101b] changed 1.txt file
 1 file changed, 1 insertion(+)
 create mode 100644 1.txt
```

### 8. Продемонструвати уміння знайти в історії комітів набір комітів, в яких була зміна по конкретному шаблону в конкретному файлі.

```
$ git log

$ git log -G 'View device information' README.md
commit 942df264324e96903524ffcbee46ee23988db582
Author: Adam Honse <calcprogrammer1@gmail.com>
Date:   Mon Jun 29 14:20:48 2020 -0500

    Update Readme

$ git diff 942df264324e96903524ffcbee46ee23988db582~..942df264324e96903524ffcbee46ee23988db582 README.md
diff --git a/README.md b/README.md
index 62ccbd45..fde84ba5 100644
--- a/README.md
+++ b/README.md
@@ -1,7 +1,17 @@
 ## ![OpenRGB](https://gitlab.com/CalcProgrammer1/OpenRGB/-/wikis/uploads/5b7e633ac9f63b00c8a4c72686206c3f/OpenRGB.png) (formerly OpenAuraSDK)

 One of the biggest complaints about RGB is the software ecosystem surrounding it.  Every manufacturer has their own app, their own brand, their own style.  If
you want to mix and match devices, you end up with a ton of conflicting, functionally identical apps competing for your background resources.  On top of that, these apps are proprietary and Windows-only.  Some even require online accounts.  What if there was a way to control all of your RGB devices from a single app, on both Windows and Linux, without any nonsense?  That is what OpenRGB sets out to achieve.  One app to rule them all.
-OpenRGB is still in its early stages and already supports quite a few products.  I'm always on the lookout for good deals on more popular RGB devices to add support for.
+
+## Features
+
+* Set colors and select effect modes for a wide variety of RGB hardware
+* Save and load profiles
+* Control lighting from third party software using the OpenRGB SDK
+* Command line interface
+* Connect multiple instances of OpenRGB to synchronize lighting across multiple PCs
+* Can operate standalone or in a client/headless server configuration
+* View device information
+* No official/manufacturer software required

$ git show 942df264324e96903524ffcbee46ee23988db582 README.md
commit 942df264324e96903524ffcbee46ee23988db582
Author: Adam Honse <calcprogrammer1@gmail.com>
Date:   Mon Jun 29 14:20:48 2020 -0500

    Update Readme

diff --git a/README.md b/README.md
index 62ccbd45..fde84ba5 100644
--- a/README.md
+++ b/README.md
@@ -1,7 +1,17 @@
 ## ![OpenRGB](https://gitlab.com/CalcProgrammer1/OpenRGB/-/wikis/uploads/5b7e633ac9f63b00c8a4c72686206c3f/OpenRGB.png) (formerly OpenAuraSDK)

 One of the biggest complaints about RGB is the software ecosystem surrounding it.  Every manufacturer has their own app, their own brand, their own style.  If
you want to mix and match devices, you end up with a ton of conflicting, functionally identical apps competing for your background resources.  On top of that, these apps are proprietary and Windows-only.  Some even require online accounts.  What if there was a way to control all of your RGB devices from a single app, on both Windows and Linux, without any nonsense?  That is what OpenRGB sets out to achieve.  One app to rule them all.
-OpenRGB is still in its early stages and already supports quite a few products.  I'm always on the lookout for good deals on more popular RGB devices to add support for.
+
+## Features
+
+* Set colors and select effect modes for a wide variety of RGB hardware
+* Save and load profiles
+* Control lighting from third party software using the OpenRGB SDK
+* Command line interface
+* Connect multiple instances of OpenRGB to synchronize lighting across multiple PCs
+* Can operate standalone or in a client/headless server configuration
+* View device information
+* No official/manufacturer software required
```
