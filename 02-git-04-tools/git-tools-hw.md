# Домашнее задание к занятию «Инструменты Git»

### Цель задания

В результате выполнения задания вы:

* научитесь работать с утилитами Git;
* потренируетесь решать типовые задачи, возникающие при работе в команде. 

### Инструкция к заданию

1. Склонируйте [репозиторий](https://github.com/hashicorp/terraform) с исходным кодом Terraform.
2. Создайте файл для ответов на задания в своём репозитории, после выполнения прикрепите ссылку на .md-файл с ответами в личном кабинете.
3. Любые вопросы по решению задач задавайте в чате учебной группы.

------

## Задание

В клонированном репозитории:

1. Найдите полный хеш и комментарий коммита, хеш которого начинается на `aefea`.
2. Ответьте на вопросы.

* Какому тегу соответствует коммит `85024d3`?
* Сколько родителей у коммита `b8d720`? Напишите их хеши.
* Перечислите хеши и комментарии всех коммитов, которые были сделаны между тегами  v0.12.23 и v0.12.24.
* Найдите коммит, в котором была создана функция `func providerSource`, её определение в коде выглядит так: `func providerSource(...)` (вместо троеточия перечислены аргументы).
* Найдите все коммиты, в которых была изменена функция `globalPluginDirs`.
* Кто автор функции `synchronizedWriters`? 

*В качестве решения ответьте на вопросы и опишите, как были получены эти ответы.*

---

### Решение.

1. 
Полный хэш: aefead2207ef7e2aa5dc81a34aedf0cad4c32545
Комментарий: Update CHANGELOG.md
```bash
git log aefea
```
```bash
commit aefead2207ef7e2aa5dc81a34aedf0cad4c32545
Author: Alisdair McDiarmid <alisdair@users.noreply.github.com>
Date:   Thu Jun 18 10:29:58 2020 -0400

    Update CHANGELOG.md

commit c12ad38c5dd4c3f4fc7a350a44cdfe4c9f52830d
Merge: ea24faa9ac 163c943e9b
Author: Alisdair McDiarmid <alisdair@users.noreply.github.com>
Date:   Thu Jun 18 10:21:31 2020 -0400
```

2. 
- 
```bash 
git log 85024d3
```
```bash 
commit 85024d3100126de36331c6982bfaac02cdab9e76 (tag: v0.12.23)
Author: tf-release-bot <terraform@hashicorp.com>
Date:   Thu Mar 5 20:56:10 2020 +0000

    v0.12.23
```
Коммит "85024d3" соответствует тэгу: "v0.12.23"
- у коммита "b8d720" 2 родителей: 56cd7859e0 9ea88f22fc
```bash
git log b8d720 --pretty=%p --graph
*   56cd7859e0 9ea88f22fc
...
```
- Хеши и комментарии всех коммитов, которые были сделаны между тегами  v0.12.23 и v0.12.24:
```bash
git log v0.12.23..v0.12.24 --oneline
```
```
33ff1c03bb (tag: v0.12.24) v0.12.24
b14b74c493 [Website] vmc provider links
3f235065b9 Update CHANGELOG.md
6ae64e247b registry: Fix panic when server is unreachable
5c619ca1ba website: Remove links to the getting started guide's old location
06275647e2 Update CHANGELOG.md
d5f9411f51 command: Fix bug when using terraform login on Windows
4b6d06cc5d Update CHANGELOG.md
dd01a35078 Update CHANGELOG.md
225466bc3e Cleanup after v0.12.23 release
```

- Функция providerSource была создана в коммите: 8c928e83589d90a031f811fae52a81be7153e82f
```bash
 git grep -p --heading "func providerSource(" 
```
```
provider_source.go
import (
func providerSource(configs []*cliconfig.ProviderInstallation, services *disco.Disco) (getproviders.Source, tfdiags.Diagnostics) {
```
```bash
git log -S providerSource -- provider_source.go
```
```
commit 5af1e6234ab6da412fb8637393c5a17a1b293663
Author: Martin Atkins <mart@degeneration.co.uk>
Date:   Tue Apr 21 16:28:59 2020 -0700

    main: Honor explicit provider_installation CLI config when present
    
    If the CLI configuration contains a provider_installation block then we'll
    use the source configuration it describes instead of the implied one we'd
    build otherwise.

commit 8c928e83589d90a031f811fae52a81be7153e82f
Author: Martin Atkins <mart@degeneration.co.uk>
Date:   Thu Apr 2 18:04:39 2020 -0700

    main: Consult local directories as potential mirrors of providers
```
-  Все коммиты, в которых была изменена функция `globalPluginDirs`:

```bash
git log -S globalPluginDirs --oneline
```
```bash
7c4aeac5f3 stacks: load credentials from config file on startup (#35952)
65c4ba7363 Remove terraform binary
125eb51dc4 Remove accidentally-committed binary
22c121df86 Bump compatibility version to 1.3.0 for terraform core release (#30988)
7c7e5d8f0a Don't show data while input if sensitive
35a058fb3d main: configure credentials from the CLI config file
c0b1761096 prevent log output during init
8364383c35 Push plugin discovery down into command package
```

-  Автор функции `synchronizedWriters`: Martin Atkins
```bash
git log -S synchronizedWriters --pretty="%h %an %ad"
```
```bash
bdfea50cc8 James Bardin Mon Nov 30 18:02:04 2020 -0500
fd4f7eb0b9 James Bardin Wed Oct 21 13:06:23 2020 -0400
5ac311e2a9 Martin Atkins Wed May 3 16:25:41 2017 -0700
```


### Правила приёма домашнего задания

В личном кабинете отправлена ссылка на .md-файл в вашем репозитории.

### Критерии оценки

Зачёт:

* выполнены все задания;
* ответы даны в развёрнутой форме;
* приложены соответствующие скриншоты и файлы проекта;
* в выполненных заданиях нет противоречий и нарушения логики.

На доработку:

* задание выполнено частично или не выполнено вообще;
* в логике выполнения заданий есть противоречия и существенные недостатки.