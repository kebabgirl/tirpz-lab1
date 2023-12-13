## Національний технічний університет України<br>“Київський політехнічний інститут ім. Ігоря Сікорського”

## Факультет прикладної математики<br>Кафедра системного програмування і спеціалізованих комп’ютерних систем

# Лабораторна робота №2<br>""Розширена робота з git"

## КВ-11 Петрук Ольга

~

## Хід виконання роботи

### 1. Зклонуємо репозиторій для ЛР2 використавши локальний репозиторій від ЛР1 в якості "віддаленого".

`Клонуємо двічі: повний репозиторій, а також частковий, що міститиме лише один коміт однієї гілки:`

```
$ git clone file:///D:/Education/3.1/tirpz/lab1/uuid
Cloning into 'uuid'...
remote: Enumerating objects: 2727, done.
remote: Counting objects: 100% (2727/2727), done.
remote: Compressing objects: 100% (1148/1148), done.
Receiving objects: 100% (2727/2727), 2.80 MiB | 36.27 MiB/s, done.
remote: Total 2727 (delta 1513), reused 2708 (delta 1505), pack-reused 0Resolving deltas:  13% (197/1513)
Resolving deltas: 100% (1513/1513), done.
```

```
$ git branch -a
* lab1-branch
  remotes/origin/HEAD -> origin/lab1-branch
  remotes/origin/lab1-branch
  remotes/origin/main
```

### 2. Робота з ремоутами.

#### 1. Додємо новий ремоут використавши URI на інтернет-джерело репозиторію.

```
$ git remote -v
origin  file:///D:/Education/3.1/tirpz/lab1/uuid (fetch)
origin  file:///D:/Education/3.1/tirpz/lab1/uuid (push)
```

```
$ git remote add upstream https://github.com/uuidjs/uuid.git
```

```
$ git remote -v
origin  file:///D:/Education/3.1/tirpz/lab1/uuid (fetch)
origin  file:///D:/Education/3.1/tirpz/lab1/uuid (push)
upstream        https://github.com/uuidjs/uuid.git (fetch)
upstream        https://github.com/uuidjs/uuid.git (push)
```

#### 2. Покажемо список віддалених гілок, так щоби було видно гілки з різних ремоутів.

```
$ git fetch upstream
remote: Enumerating objects: 99, done.
remote: Counting objects: 100% (83/83), done.
remote: Compressing objects: 100% (27/27), done.

Unpacking objects: 100% (99/99), 21.18 KiB | 10.00 KiB/s, done.
From https://github.com/uuidjs/uuid
 * [new branch]      lu-max             -> upstream/lu-max
 * [new branch]      main               -> upstream/main
 * [new branch]      node-uuid          -> upstream/node-uuid
 * [new branch]      release-please     -> upstream/release-please
 * [new branch]      revert_677         -> upstream/revert_677
 * [new branch]      rfc4122bis         -> upstream/rfc4122bis
 * [new branch]      typescript-typings -> upstream/typescript-typings
```

```
$ git branch -a
* lab1-branch
  remotes/origin/HEAD -> origin/lab1-branch
  remotes/origin/lab1-branch
  remotes/origin/main
  remotes/upstream/lu-max
  remotes/upstream/main
  remotes/upstream/node-uuid
  remotes/upstream/release-please
  remotes/upstream/revert_677
  remotes/upstream/rfc4122bis
```

#### 3. Створюємо нову гілку lab2-branch та додаємо в нього кілька комітів.

```
$ git checkout -b lab2-branch
Switched to a new branch 'lab2-branch'
```

Створено файл 1.txt.

```
$ git add .

$ git commit -m 'add 1.txt'
[lab2-branch f1df2ab] add 1.txt
 1 file changed, 1 insertion(+)
 create mode 100644 1.txt
```

Створено файли 2.txt, 3.txt.

```
$ git add .

$ git commit -m 'add 2.txt and 3.txt'
[lab2-branch f400996] add 2.txt and 3.txt
 2 files changed, 2 insertions(+)
 create mode 100644 2.txt
 create mode 100644 3.txt
```

Змінено файл 1.txt.

```
$ git add .

$ git commit -m 'edit 1.txt'
[lab2-branch 0452382] edit 1.txt
 1 file changed, 1 insertion(+), 1 deletion(-)
```

#### 4. Пушнемо гілку lab2-branch на ремоут, створений з ЛР1 без зв'язування локальної гілки з віддаленою.

```
$ git push
fatal: The current branch lab2-branch has no upstream branch.
To push the current branch and set the remote as upstream, use

    git push --set-upstream origin lab2-branch

To have this happen automatically for branches without a tracking
upstream, see 'push.autoSetupRemote' in 'git help config'.
```

```
$ git push origin lab2-branch
Enumerating objects: 11, done.
Counting objects: 100% (11/11), done.
Delta compression using up to 8 threads
Compressing objects: 100% (6/6), done.
Writing objects: 100% (10/10), 743 bytes | 743.00 KiB/s, done.
Total 10 (delta 3), reused 0 (delta 0), pack-reused 0
To file:///D:/Education/3.1/tirpz/lab1/uuid
 * [new branch]      lab2-branch -> lab2-branch
```

#### 5. Додамо до гілки ще коміт.

Змінено файл 2.txt.

```
$ git status
On branch lab2-branch
Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git restore <file>..." to discard changes in working directory)
        modified:   2.txt

no changes added to commit (use "git add" and/or "git commit -a")

$ git add .

$ git commit -m 'edit 2.txt'
[lab2-branch ae190c1] edit 2.txt
 1 file changed, 1 insertion(+), 1 deletion(-)
```

#### 6. Пушнемо зміни гілки на ремоут, створений з ЛР1, цього разу зв'язавши гілки.

```
$ git push -u origin lab2-branch
Enumerating objects: 5, done.
Counting objects: 100% (5/5), done.
Delta compression using up to 8 threads
Compressing objects: 100% (2/2), done.
Writing objects: 100% (3/3), 262 bytes | 262.00 KiB/s, done.
Total 3 (delta 1), reused 0 (delta 0), pack-reused 0
To file:///D:/Education/3.1/tirpz/lab1/uuid
   0452382..ae190c1  lab2-branch -> lab2-branch
branch 'lab2-branch' set up to track 'origin/lab2-branch'.
```

#### 7. Додамо до гілки ще коміт.

Додано файл 4.txt.

```
$ git status
On branch lab2-branch
Your branch is up to date with 'origin/lab2-branch'.

Untracked files:
  (use "git add <file>..." to include in what will be committed)
        4.txt

nothing added to commit but untracked files present (use "git add" to track)

$ git add .

$ git commit -m 'add 4.txt'
[lab2-branch 53f70a6] add 4.txt
 1 file changed, 1 insertion(+)
 create mode 100644 4.txt
```

#### 8. Переконаємося в тому, що після зв'язування гілок тепер можна пушити просто через git push.

```
$ git push
Enumerating objects: 4, done.
Counting objects: 100% (4/4), done.
Delta compression using up to 8 threads
Compressing objects: 100% (2/2), done.
Writing objects: 100% (3/3), 269 bytes | 269.00 KiB/s, done.
Total 3 (delta 1), reused 0 (delta 0), pack-reused 0
To file:///D:/Education/3.1/tirpz/lab1/uuid
   ae190c1..53f70a6  lab2-branch -> lab2-branch
```

#### 9. Перевіримо в репозиторії ЛР1, що після пушу тут з'явилася нова локальна гілка (яку ми власне пушнули).

Перейдено у репозиторій ЛР1.

```
$ git branch -a
* lab1-branch
  lab2-branch
  main
  remotes/origin/HEAD -> origin/main
  remotes/origin/lu-max
  remotes/origin/main
  remotes/origin/node-uuid
  remotes/origin/release-please
  remotes/origin/revert_677
  remotes/origin/rfc4122bis
```

### 3. Змерджимо гілку, що була створена при виконанні ЛР1, в поточну гілку lab2-branch.

```
$ git branch -a
  lab1-branch
* lab2-branch
  remotes/origin/HEAD -> origin/lab1-branch
  remotes/origin/lab1-branch
  remotes/origin/lab2-branch
  remotes/origin/main
  remotes/upstream/lu-max
  remotes/upstream/main
  remotes/upstream/node-uuid
  remotes/upstream/release-please

$ git merge origin/lab1-branch
Already up to date.

$ git log --pretty=oneline --graph
* 53f70a6b5145b5374b9d3ee57d0970e8b6848fac (HEAD -> lab2-branch, origin/lab2-branch) add 4.txt
* ae190c13ef3b1783051fa8965ed0040d667beeaa edit 2.txt
* 045238260e308d35c7d7626bf06d01ec98ee4285 edit 1.txt
* f4009960944fdf0fe4a74e0dd388fbcd00b0f2aa add 2.txt and 3.txt
* f1df2ab767fcb5c3057cc3b2c2f1e353492facb2 add 1.txt
* 2dc859f82d56d0df172d2f72c735ac743259dec9 (origin/lab1-branch, origin/HEAD) edit 1.js
* 0662142ed15f1cd1051eed1c72646506cd894e01 add 2.js and 3.js
* defae57f44ff074770094cc3b1dbc727715a1be6 add 1.js
* bc46e198ab06311a9d82d3c9c6222062dd27f760 (upstream/main, origin/main) chore: expand Prettier glob to all files (#701)
* e267b9073df1d0ce119ee53c0487fe76acb2be37 fix: revert "perf: remove superfluous call to toLowerCase (#677)" (#738)
```

### 4. Перенесення комітів.

#### 1. Створюємо ще одну гілку від master-a lab2-branch-2, додаємо в неї три коміти.

```
$ git checkout --track origin/main
Switched to a new branch 'main'
branch 'main' set up to track 'origin/main'.

$ git checkout -b lab2-branch-2
Switched to a new branch 'lab2-branch-2'
```

Створено файл AAA.txt.

```
$ git status
On branch lab2-branch-2
Untracked files:
  (use "git add <file>..." to include in what will be committed)
        AAA.txt

nothing added to commit but untracked files present (use "git add" to track)

$ git add .

$ git commit -m 'add AAA'
[lab2-branch-2 4228f3a] add AAA
 1 file changed, 1 insertion(+)
 create mode 100644 AAA.txt
```

Створено файл BBB.txt.

```
$ git status
On branch lab2-branch-2
Untracked files:
  (use "git add <file>..." to include in what will be committed)
        BBB.txt

nothing added to commit but untracked files present (use "git add" to track)

$ git add .

$ git commit -m 'add BBB.txt'
[lab2-branch-2 860b4d8] add BBB.txt
 1 file changed, 1 insertion(+)
 create mode 100644 BBB.txt
```

Створено файл CCC.txt.

```
$ git status
On branch lab2-branch-2
Untracked files:
  (use "git add <file>..." to include in what will be committed)
        CCC.txt

nothing added to commit but untracked files present (use "git add" to track)

$ git add .

$ git commit -m 'add CCC.txt'
[lab2-branch-2 f59cc56] add CCC.txt
 1 file changed, 1 insertion(+)
 create mode 100644 CCC.txt
```

#### 2. Переносимо з гілки lab2-branch-2 середній з трьох нових комітів в гілку lab2-branch.

```
$ git log -n 3
commit f59cc56d1b2f86f90ebb2c7e7337123f36c24eda (HEAD -> lab2-branch-2)
Author: kebabgirl <olapetruk2003@gmail.com>
Date:   Wed Dec 13 12:33:54 2023 +0200

    add CCC.txt

commit 860b4d835a2598f293bf26f247252c2a30825343
Author: kebabgirl <olapetruk2003@gmail.com>
Date:   Wed Dec 13 12:32:59 2023 +0200

    add BBB.txt

commit 4228f3a5493e2b26fa3a275854b3cce9b3ac7643
Author: kebabgirl <olapetruk2003@gmail.com>
Date:   Wed Dec 13 12:31:50 2023 +0200

    add AAA


$ git checkout lab2-branch
Switched to branch 'lab2-branch'
Your branch is up to date with 'origin/lab2-branch'.

$ git cherry-pick 860b4d835a2598f293bf26f247252c2a308253431
fatal: bad revision '860b4d835a2598f293bf26f247252c2a308253431'

$  git log --pretty=oneline --graph -n 10 --branches
* f59cc56d1b2f86f90ebb2c7e7337123f36c24eda (lab2-branch-2) add CCC.txt
* 860b4d835a2598f293bf26f247252c2a30825343 add BBB.txt
* 4228f3a5493e2b26fa3a275854b3cce9b3ac7643 add AAA
| * 53f70a6b5145b5374b9d3ee57d0970e8b6848fac (HEAD -> lab2-branch, origin/lab2-branch) add 4.txt
| * ae190c13ef3b1783051fa8965ed0040d667beeaa edit 2.txt
| * 045238260e308d35c7d7626bf06d01ec98ee4285 edit 1.txt
| * f4009960944fdf0fe4a74e0dd388fbcd00b0f2aa add 2.txt and 3.txt
```

### 5. Визначити останнього спільного предка між двома будь-якими гілками.

```
$ git merge-base origin/lab2-branch origin/lab1-branch
2dc859f82d56d0df172d2f72c735ac743259dec9
```

### 6. Робота з ничкою.

#### 1. Зробимо трохи unstaged змін.

```
$ git status
On branch lab2-branch
Your branch is up to date with 'origin/lab2-branch'.

Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git restore <file>..." to discard changes in working directory)
        modified:   1.txt
        modified:   2.txt

no changes added to commit (use "git add" and/or "git commit -a")
```

#### 2. Збережемо до нички.

```
$ git stash
Saved working directory and index state WIP on lab2-branch: 53f70a6 add 4.txt

$ git status
On branch lab2-branch
Your branch is up to date with 'origin/lab2-branch'.

nothing to commit, working tree clean

$ git stash list
stash@{0}: WIP on lab2-branch: 53f70a6 add 4.txt
```

#### 3. Зробимо ще трохи unstaged змін.

```
$ git status
On branch lab2-branch
Your branch is up to date with 'origin/lab2-branch'.

Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git restore <file>..." to discard changes in working directory)
        modified:   3.txt
        modified:   4.txt

no changes added to commit (use "git add" and/or "git commit -a")
```

#### 4. Збережемо до нички.

```
$ git stash
Saved working directory and index state WIP on lab2-branch: 53f70a6 add 4.txt

$ git stash list
stash@{0}: WIP on lab2-branch: 53f70a6 add 4.txt
stash@{1}: WIP on lab2-branch: 53f70a6 add 4.txt
```

#### 5. Дістанемо з нички перші збережені зміни, ті що збереглися на кроці (6.2).

```
$ git stash apply stash@{0}
On branch lab2-branch
Your branch is up to date with 'origin/lab2-branch'.

Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git restore <file>..." to discard changes in working directory)
        modified:   3.txt
        modified:   4.txt

no changes added to commit (use "git add" and/or "git commit -a")
```

### 7. Робота з файлом .gitignore.

#### 1. Створюємо кілька файлів з якимось унікальним розширенням.

Створено файли 11.kvfpm, 12.kvfpm та 123.fpm.

```
$ git status
On branch lab2-branch
Your branch is up to date with 'origin/lab2-branch'.

Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git restore <file>..." to discard changes in working directory)
        modified:   3.txt
        modified:   4.txt

Untracked files:
  (use "git add <file>..." to include in what will be committed)
        11.kvfpm
        12.kvfpm
        123.fpm

no changes added to commit (use "git add" and/or "git commit -a")
```

#### 2. Додаємо шаблон для цих файлів в ігнор та перевіряємо статус -- файли повинні зникнути.

```
$ git status
On branch lab2-branch
Your branch is up to date with 'origin/lab2-branch'.

Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git restore <file>..." to discard changes in working directory)
        modified:   .gitignore
        modified:   3.txt
        modified:   4.txt

Untracked files:
  (use "git add <file>..." to include in what will be committed)
        123.fpm

no changes added to commit (use "git add" and/or "git commit -a")
```

#### 3. Перевіряємо статус включно з ігнором.

```
$ git status --ignored
On branch lab2-branch
Your branch is up to date with 'origin/lab2-branch'.

Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git restore <file>..." to discard changes in working directory)
        modified:   .gitignore
        modified:   3.txt
        modified:   4.txt

Untracked files:
  (use "git add <file>..." to include in what will be committed)
        123.fpm

Ignored files:
  (use "git add -f <file>..." to include in what will be committed)
        11.kvfpm
        12.kvfpm

no changes added to commit (use "git add" and/or "git commit -a")
```

#### 4. Чистимо всі untracked файли з репозиторію, включно з ігнорованими.

```
$ git clean -fdx
Removing 11.kvfpm
Removing 12.kvfpm
Removing 123.fpm
```

### 8. Робота з reflog.

#### 1. Переглядаємо лог станів гілок.

```
$ git log --pretty=oneline --graph -n 15
* 53f70a6b5145b5374b9d3ee57d0970e8b6848fac (HEAD -> lab2-branch, origin/lab2-branch) add 4.txt
* ae190c13ef3b1783051fa8965ed0040d667beeaa edit 2.txt
* 045238260e308d35c7d7626bf06d01ec98ee4285 edit 1.txt
* f4009960944fdf0fe4a74e0dd388fbcd00b0f2aa add 2.txt and 3.txt
* f1df2ab767fcb5c3057cc3b2c2f1e353492facb2 add 1.txt
* 2dc859f82d56d0df172d2f72c735ac743259dec9 (origin/lab1-branch, origin/HEAD) edit 1.js
* 0662142ed15f1cd1051eed1c72646506cd894e01 add 2.js and 3.js
* defae57f44ff074770094cc3b1dbc727715a1be6 add 1.js
* bc46e198ab06311a9d82d3c9c6222062dd27f760 (upstream/main, origin/main, main) chore: expand Prettier glob to all files (#701)
* e267b9073df1d0ce119ee53c0487fe76acb2be37 fix: revert "perf: remove superfluous call to toLowerCase (#677)" (#738)
* ca1d39d58a6308d5311bcb356a931aa818ec0ded chore(release): 9.0.1
* fc5d64346a8a93324b7f8f87bdc6b96164f35ba0 chore: add node@12 back to CI, update readme (#733)
* 462128b660e477c8878a991073547c01ffaf76e6 ci: update node versions for cI (#732)
* 4de23a6030e65ac72b3b015680f08e7e292681ed test: remove missing getRandomValues test (#709)
* 6eef540aa3407b15e1e7573f45ff17098e9343ea chore: adapt bundlewatch config to new main branch name (#705)

$ git branch -D lab2-branch

$ git push -d origin lab2-branch

$ git reflog
bc46e19 (HEAD -> main, upstream/main, origin/main) HEAD@{0}: checkout: moving from lab2-branch to main
6ecfeec HEAD@{1}: commit: edit 3.txt and 4.txt
53f70a6 HEAD@{2}: reset: moving to HEAD
53f70a6 HEAD@{3}: reset: moving to HEAD
53f70a6 HEAD@{4}: checkout: moving from lab2-branch-2 to lab2-branch
f59cc56 (lab2-branch-2) HEAD@{5}: checkout: moving from lab2-branch to lab2-branch-2
53f70a6 HEAD@{6}: checkout: moving from lab2-branch-2 to lab2-branch
f59cc56 (lab2-branch-2) HEAD@{7}: checkout: moving from lab2-branch to lab2-branch-2
53f70a6 HEAD@{8}: checkout: moving from lab2-branch-2 to lab2-branch
f59cc56 (lab2-branch-2) HEAD@{9}: checkout: moving from lab2-branch to lab2-branch-2
:...skipping...
bc46e19 (HEAD -> main, upstream/main, origin/main) HEAD@{0}: checkout: moving from lab2-branch to main
6ecfeec HEAD@{1}: commit: edit 3.txt and 4.txt
53f70a6 HEAD@{2}: reset: moving to HEAD
53f70a6 HEAD@{3}: reset: moving to HEAD
53f70a6 HEAD@{4}: checkout: moving from lab2-branch-2 to lab2-branch
f59cc56 (lab2-branch-2) HEAD@{5}: checkout: moving from lab2-branch to lab2-branch-2
53f70a6 HEAD@{6}: checkout: moving from lab2-branch-2 to lab2-branch
f59cc56 (lab2-branch-2) HEAD@{7}: checkout: moving from lab2-branch to lab2-branch-2
53f70a6 HEAD@{8}: checkout: moving from lab2-branch-2 to lab2-branch
f59cc56 (lab2-branch-2) HEAD@{9}: checkout: moving from lab2-branch to lab2-branch-2
53f70a6 HEAD@{10}: checkout: moving from lab2-branch-2 to lab2-branch
f59cc56 (lab2-branch-2) HEAD@{11}: commit: add CCC.txt
860b4d8 HEAD@{12}: commit: add BBB.txt
4228f3a HEAD@{13}: commit: add AAA
bc46e19 (HEAD -> main, upstream/main, origin/main) HEAD@{14}: checkout: moving from main to lab2-branch-2
bc46e19 (HEAD -> main, upstream/main, origin/main) HEAD@{15}: checkout: moving from lab2-branch to main
53f70a6 HEAD@{16}: checkout: moving from 2dc859f82d56d0df172d2f72c735ac743259dec9 to lab2-branch
2dc859f (origin/lab1-branch, origin/HEAD) HEAD@{17}: checkout: moving from bc46e198ab06311a9d82d3c9c6222062dd27f760 to origin/lab1-branch
bc46e19 (HEAD -> main, upstream/main, origin/main) HEAD@{18}: checkout: moving from lab2-branch to origin/main
53f70a6 HEAD@{19}: commit: add 4.txt
ae190c1 HEAD@{20}: commit: edit 2.txt
0452382 HEAD@{21}: commit: edit 1.txt
f400996 HEAD@{22}: commit: add 2.txt and 3.txt
f1df2ab HEAD@{23}: commit: add 1.txt
2dc859f (origin/lab1-branch, origin/HEAD) HEAD@{24}: checkout: moving from lab1-branch to lab2-branch
2dc859f (origin/lab1-branch, origin/HEAD) HEAD@{25}: clone: from file:///D:/Education/3.1/tirpz/lab1/uuid
```

#### 2. Створюємо нову гілку на будь-який стан зі списку та переключаємося на цю гілку.

```
$ git branch lab2-resurrected 6ecfeec

$ git checkout lab2-resurrected
Switched to branch 'lab2-resurrected'

$ git log --pretty=oneline --graph -n 15
* 6ecfeecca94e0aa52e60d1f8cc3ef4650f64750c (HEAD -> lab2-resurrected) edit 3.txt and 4.txt
* 53f70a6b5145b5374b9d3ee57d0970e8b6848fac add 4.txt
* ae190c13ef3b1783051fa8965ed0040d667beeaa edit 2.txt
* 045238260e308d35c7d7626bf06d01ec98ee4285 edit 1.txt
* f4009960944fdf0fe4a74e0dd388fbcd00b0f2aa add 2.txt and 3.txt
* f1df2ab767fcb5c3057cc3b2c2f1e353492facb2 add 1.txt
* 2dc859f82d56d0df172d2f72c735ac743259dec9 (origin/lab1-branch, origin/HEAD) edit 1.js
* 0662142ed15f1cd1051eed1c72646506cd894e01 add 2.js and 3.js
* defae57f44ff074770094cc3b1dbc727715a1be6 add 1.js
* bc46e198ab06311a9d82d3c9c6222062dd27f760 (upstream/main, origin/main, main) chore: expand Prettier glob to all files (#701)
* e267b9073df1d0ce119ee53c0487fe76acb2be37 fix: revert "perf: remove superfluous call to toLowerCase (#677)" (#738)
* ca1d39d58a6308d5311bcb356a931aa818ec0ded chore(release): 9.0.1
* fc5d64346a8a93324b7f8f87bdc6b96164f35ba0 chore: add node@12 back to CI, update readme (#733)
* 462128b660e477c8878a991073547c01ffaf76e6 ci: update node versions for cI (#732)
* 4de23a6030e65ac72b3b015680f08e7e292681ed test: remove missing getRandomValues test (#709)
```
