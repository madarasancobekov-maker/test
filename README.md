# Git және GitHub: 11–15-сабақтарға практика

Бұл жоба VS Code-та Git-пен жұмыс істеуді жаттықтыруға арналған. Командаларды VS Code ішіндегі **Terminal → New Terminal** терезесінде, осы жоба ашық тұрғанда орындаңыз.

## Бастапқы тексеріс

```bash
git status
git log --oneline --decorate --graph --all
```

`git status` жұмыс қалтасы мен staging аймағындағы өзгерістерді көрсетеді. `git log` коммиттер тарихын көрсетеді.

## 11-сабақ — Git Graph

VS Code-та Extensions бөлімін ашып, **Git Graph** кеңейтімін іздеңіз. Орнатылған соң командалар палитрасынан `Git Graph: View Git Graph` ашыңыз. Графикте коммиттер, тармақтар және олардың байланысы көрінеді.

Қосымша тексеру:

```bash
git log --oneline --decorate --graph --all
```

## 12-сабақ — Git alias командалары

Қысқа командаларды тек осы репозиторийге орнатыңыз:

```bash
git config --local alias.st status
git config --local alias.ci commit
git config --local alias.co checkout
git config --local alias.br branch
git config --local alias.lg "log --oneline --decorate --graph --all"
```

Тексеру:

```bash
git st
git br
git lg
```

`--local` баптауы тек осы жобаға әсер етеді. Aliases `.git/config` файлында сақталады және коммитке қосылмайды.

## 13-сабақ — өзгерістерді қайтару

Алдымен файлға уақытша мәтін қосып, сақтаңыз. Қайтармас бұрын өзгерісті тексеріңіз:

```bash
git diff
```

Жұмыс қалтасындағы файл өзгерісін соңғы коммиттегі күйіне қайтару:

```bash
git restore index.html
```

Staging аймағына қосылған өзгерісті алдымен одан шығару:

```bash
git restore --staged index.html
```

Одан кейін ғана жұмыс қалтасындағы өзгерісті қайтарыңыз. Ал бұрын жасалған коммитті тарихты қайта жазбай кері айналдыру үшін:

```bash
git revert <коммит-хэші>
```

`git restore` жергілікті сақталмаған өзгерісті өшіруі мүмкін. Алдымен `git diff` арқылы тексеріңіз; қажет файлға жасалған өзгерістерді ғана қайтарыңыз.

## 14-сабақ — тармақ құру және ауысу

Жаңа тәжірибелік тармақ құрып, оған ауысыңыз:

```bash
git switch -c practice-branches
```

Ескі Git нұсқаларында баламасы:

```bash
git checkout -b practice-branches
```

Қазіргі тармақты және қолда бар тармақтарды көру:

```bash
git branch
```

`index.html` файлына шағын өзгеріс енгізіп, оны коммитке сақтаңыз:

```bash
git add index.html
git commit -m "Add branch practice change"
```

## 15-сабақ — тармақтарды басқару және GitHub-пен синхрондау

Тармақтар арасында ауысу:

```bash
git switch main
git switch practice-branches
```

Тармақты қайта атау:

```bash
git branch -m practice-branches practice-branches-renamed
```

Қашықтағы репозиторийге тармақты жариялау қажет болса:

```bash
git push -u origin practice-branches-renamed
```

Жергілікті тармақты жою тек ол керек болмай қалған кезде орындалады:

```bash
git branch -d practice-branches-renamed
```

GitHub-тағы тармақты жою бөлек әрекет және қашықтағы репозиторийді өзгертеді. Бұл оқу жобасында оны қажет болмаса орындамаңыз.

## Практика соңындағы тексеріс

```bash
git status
git lg
```

Өзгерістерді GitHub-қа жібермес бұрын қай тармақта тұрғаныңызды және коммиттерді тексеріңіз.

