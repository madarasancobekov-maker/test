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


## Толық видео-практика: #11–#15

Бұл сабақтар Git/GitHub-тың өзімен жұмыс істеуді үйретеді; кодтағы шағын HTML өзгерістер Git әрекеттерін көрсетуге ғана арналған.

### #11 — Git Graph

VS Code-та `mhutchie.git-graph` кеңейтімі орнатылған. Оны Source Control ішіндегі **Graph** бөлімінен немесе статус жолағындағы **Git Graph** батырмасынан ашуға болады. Графикте коммиттер, ағымдағы тармақ және `origin`-дегі тармақ көрінеді. Коммитті таңдап, оның diff-ін қараңыз.

### #12 — alias

Видеода қысқартулар user-level `.gitconfig` файлына жазылады. Осы жобада сол командаларды репозиторийге ғана әсер ететін жергілікті баптаумен сақтадым:

```bash
git config --local alias.s "status --short"
git config --local alias.l "log --oneline --graph --decorate --all"
git config --local alias.g "log --graph --abbrev-commit --decorate --all --oneline"
git config --local alias.br branch
git config --local alias.co checkout
```

Тексерілген командалар: `git s`, `git l`, `git g`, `git br`. Видеодағыдай барлық жобаларға ортақ ету үшін осы командалардағы `--local` орнына `--global` қолданылады.

### #13 — өзгерістерді кері қайтару

Тәжірибе жеке уақытша worktree-де жасалды; жобадағы сіздің `index.html` өзгерісіңіз сақталды.

```bash
# Жұмыс қалтасындағы сақталмаған өзгерісті тастау
git checkout -- index.html

# Staging-тен файлды шығару, одан соң жұмыс өзгерісін тастау
git reset index.html
git checkout -- index.html

# Соңғы коммитті және файл өзгерісін толық жою
git reset --hard HEAD~1

# Соңғы коммитті алып тастап, staged өзгерістерді қалдыру
git reset --soft HEAD~1
git reset index.html
git checkout -- index.html
```

Git Graph/VS Code ішінде баламасы: **Undo Last Commit**, staged файлды **Unstage**, кейін өзгерісті **Discard** ету. Ескі коммитті графтан таңдап, **Checkout** ету detached HEAD күйіне әкеледі; тармаққа қайта оралу үшін `git checkout main` сияқты тармақ атауын қолданыңыз. `--hard` ағымдағы жұмыс өзгерістерін жояды, сондықтан орындалмас бұрын `git status` тексеріледі.

### #14 — тармақ құру және тарих айырмасын көру

Уақытша бөлек worktree-де `tutorial-main` және `develop` тармақтарын құрып, әрқайсысына шағын HTML коммитін жасадым. Git Graph және `git log --graph` олардың бір бастапқы коммиттен тарағанын көрсетті. Кейін мысал коммиттерін кері қайтарып, уақытша тармақты жойдым. Бұл HTML мысалдары негізгі `main` және `practice-branches` тармақтарына қосылған жоқ.

```bash
git branch
git branch -v
git branch develop
git checkout develop
# index.html файлына мысал өзгеріс енгізіп:
git add index.html
git commit -m "New"
git checkout main
# main тармағында басқа өзгеріс енгізіп, коммит жасаңыз
git add index.html
git commit -m "New"
git log --oneline --graph --decorate --all
```

### #15 — тармақ атауын өзгерту, hash бойынша ауысу, жариялау және жою

Уақытша тармақта атауын өзгерту, `git checkout -b develop` арқылы тармақ құрып оған бірден ауысу, commit hash бойынша detached HEAD күйіне өту, `git checkout tutorial-main` арқылы тармаққа қайту, feature коммиттерін reset ету және уақытша тармақты жою әрекеттерін орындадым.

```bash
git branch -m master-demo
git branch -m tutorial-main
git checkout -b develop
git checkout <commit-hash>
git checkout tutorial-main
git push -u origin develop
git push origin --delete develop
git branch -D develop
```

`practice-branches` тармағын сіз GitHub-қа жібердіңіз; ол `origin/practice-branches` тармағымен тең. Оны уақытша `develop` тармағының орнына жойған жоқпын. Жаңа уақытша тармақты GitHub-қа жариялап, одан кейін жою қадамдарын осы командалар көрсетеді. Қазіргі ортада GitHub тіркелгі деректері қолжетімсіз болғандықтан, осы қадамдарды серверде орындаған жоқпын.
