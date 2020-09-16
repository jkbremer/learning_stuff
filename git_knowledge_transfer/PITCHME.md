---?color=linear-gradient(180deg, #1E5C97 75%, black 25%)
# Oh shit, **GIT**
@snap[south span-100]
#### Wissenstransfer
Julia Bremer - Univention GMBH
@snapend

---

### **Agenda**

@snap[east span-50]
@img[shadow](assets/img/ohshitgit.png)
@snapend

@snap[west span-50]
@ol[list-spaces-bullets text-05](true)
1. Kleine Einführung
1. Begrifflichkeiten
1. Zeichen
1. Commits
1. Diff und Show
1. Blaming
1. Branches
1. Merge
1. Merge Konflikte
1. Stash
1. Dinge rückgängig machen - reset
1. Dinge rückgängig machen - checkout
1. Dinge rückgängig machen - rebase
1. Dinge rückgängig machen - Aufgaben
1. Reflog
1. Cherry-pick
1. Allgemeine Aufgaben
1. Git submodule
1. Gute Quellen
@olend
@snapend

---

### Kleine **Einführung**
@snap[east span-20]
@img[](assets/img/git.png)
@snapend

@snap[west span-80]
@ul[list-spaced-bullets text-07]
- Git wurde 2005 von **Linus Torvalds** initiiert.
- Git bedeutet umgangsprachlich **Blödmann**
- *“I’m an egotistical bastard, and I name all my projects after myself. First ‘Linux’, now ‘Git’.”*
- Unterstützt nicht-lineare Entwicklung sehr, branching und merging ist sehr schnell
@snapend

---
@snap[north-west span-80]
### Begrifflichkeiten
@snapend
@snap[south-west span-80]
@ol[list-spaced-bullets text-05]
- **Modified**<div /> Modified bedeutet, dass Änderungen im Working Directory gemacht wurden, die noch nicht gestaged oder committed wurden.
- **Staged**<div /> Staged bedeutet, dass ein File zum commit *vorgemerkt* wurde, aber noch nicht committed wurde
- **Committed**<div /> Committed heißt, dass deine Daten in der Git-Datenbank hinterlegt wurden.
- **origin**<div /> Die URL des remote Repositories von dem geclont wurde.
- **Branch**<div /> Ein Branch ist nur ein Zeiger auf einen Commit und daher ist es sehr schnell ihn zu wechseln
- **HEAD**<div /> Der Commit den man gerade ausgecheckt hat
@olend
@snapend

---
@snap[north-west span-80]
### Zeichen
@snapend
@snap[west span-100]
@ol[list-spaced-bullets text-05]
- **^ (caret)** : `<commit>^` referenziert das **Elter** des Commits, `<commit>^2` das zweite Elter (Vorhanden bei merge-commits)
- **~ (tilde)** : `<commit>~`refernziert auch das **Elter** des Commits, ist also äquivalent zu `<commit>^`. `<commit>~x` referenziert jedoch den x-ten **Vorfahren** von `<commit>`.
- **@** : Ein `@`ist das Kürzel für **HEAD**
- **--** : Ein `--` bedeutet, dass die Nachfolgende Referenz ein **File** und keinen Branch/Commit bezeichnet
@olend
@snapend

---
### Commits
@snap[south-west span-100]
@ul[list-spaced-bullets text-07]
- Jeder commit besteht aus einem **snapshot** deines Repositories zusammen mit den gemachten Änderungen.
- Jeder commit wird im **.git** Ordner gespeichert und ist **immer** wieder aufrufbar. (Außer du löscht deinen .git Ordner...)
- Jeder commit ist ein Hash aus deinem Repo und seinen Änderungen. Jeder Commithash ist **eindeutig** und führt immer zum gleichen Code.
- Git fügt immer nur Informationen seiner Datenbank hinzu. Gelöscht wird nichts.
- Commits können nicht geändert werden. Bei Änderungen wird immer ein neuer Commit erstellt und der Pointer ausgetauscht.
@ulend
@snapend

---?color=linear-gradient(180deg, #1E5C97 100%, black 0%)
### Diff und Show

```bash zoom-10
git diff
git diff --staged
git diff HEAD
git show <commit>
git diff branch1..branch2
$ git diff branch1...branch2
```
@[1](Zeige die **unstaged** Changes)
@[2](Zeige die **staged** Changes)
@[3](Zeige beides)
@[4](Zeige den **`<commit>`**, default ist HEAD)
@[5](Zeige den Unterschied zwischen zwei Branches)
@[6](Zeige den Unterschied zwischen dem HEAD von Branch2 und dem **"common ancestor"** von branch1 und branch2)

---?color=linear-gradient(180deg, #1E5C97 100%, black 0%)
### Blaming

@snap[north-south span-100]
@ul[list-spaced-bullets text-07]
- Command: **`git blame`**
- Git blame braucht man häufig um herauszufinden, wann und warum eine Änderung gemacht wurde.
- Insgesamt speichert git viele Informationen, bei denen es nützlich ist, diese abzurufen.
@ulend
@snapend

```bash zoom-10
git blame <file>
git blame ^<hash> <file>
git log --diff-filter=A -- <file>
git log --diff-filter=D -- <file>
```
@[1](Finde heraus, welcher Commit die letzte Änderung gemacht hat)
@[2](Finde heraus, welcher Commit die letzte Änderung vor Commit `<hash>` gemacht hat)
@[3](Finde heraus, durch welchen Commit `<file>` dem Repo hinzugefügt wurde)
@[4](Dementsprechend: Wer hat das `<file>` gelöscht?)
@snap[south span-100]
@ol[list-spaced-bullets text-06]
1. **Aufgabe**: Findet heraus, wer wann das komische README.md geschrieben hat.
1. **Aufgabe**: Findet heraus wer und wann einen bestimmten ucs-test gelöscht hat. Ich weiß allerdings nicht mehr wie er hieß, irgendwas mit **printer** ..
@olend
@snapend


---?color=linear-gradient(180deg, #1E5C97 100%, black 0%)
### Branches
@snap[north-south span-100]
@ul[list-spaced-bullets text-07]
- Ein Branch ist ein **Pointer** auf einen commit
- Dabei ist der **HEAD** des neuen Branches <br />zunächst der selbe,wie der des Branches <br />auf dem du den Befehl ausgeführt hast
@ulend
@snapend
@snap[east span-20]
@img[](assets/img/workflow.png)
@snapend

@snap[span-80]
```bash zoom-10
git branch
git branch <branchname>
git checkout -b <branchname>
git branch -D <branchname>
git push --delete origin <branchname>
```
@snapend
@[1](Finde heraus auf welchem Branch du bist)
@[2](Kreiere einen neuen Branch auf Basis des aktuellen Branches)
@[3](Kreiere einen neuen Branch und checke ihn gleich aus)
@[4](Lösche einen Branch lokal)
@[5](Lösche einen Branch remote)

---?color=linear-gradient(180deg, #1E5C97 100%, black 0%)

### Merge
@snap[west-south span-100]
@ol[list-spaced-bullets text-06]
- Um Branches zusammenzubringen
- Fast-forward : Der Pointer des Commits wird einfach nach vorne geschoben
- Merge made by the *'recursive'* strategy. (Three-way-merge)
- Wenn kein fast-forward möglich ist, dann wird ein neuer commit (merge commit) erstellt, der zwei Elter hat
- `git pull` ist ein Update der remote Referenzen + merge
- `git merge --abort` Bricht einen merge ab
@snapend
@olend

@snap[west-south span-100]
@ol[list-spaced-bullets text-06]
1. **Aufgabe**: Erstellt einen neuen Branch, der dem Master (hier 4.4-5) folgt, erstellt einen Commit und merged ihn in den Master.
1. **Aufgabe**: Warum steht bei dem ersten von euch *fast-forward* und bei den anderen *`Merge made by recursive strategy`*?
1. **Aufgabe**: Löscht eure gemergeden(?) Branches wieder. Lokal und remote.
@olend
@snapend

---?color=linear-gradient(180deg, #1E5C97 100%, black 0%)

### Merge-Konflikte
@snap[west-south span-100]
@ol[list-spaced-bullets text-07]
- Wenn in zwei Branches ein File unterschiedlich geändert wurde, tritt ein *merge Konflikt* auf.
- In diesem Fall lässt sich mit **git status** anzeigen in welchen Files der Konflikt liegt.
- Um den Konflikt zu beheben muss man die Markierungen, die Git in dieses File eingefügt hat entfernen und **`git add <file>`** und **`git commit --amend`** ausführen
@olend
@snapend

@snap[span-100]
```bash zoom-07
$ git status
On branch master
You have unmerged paths.
(fix conflicts and run "git commit")
Unmerged paths:
(use "git add <file>..." to mark resolution)
both modified:
index.html
```
@snapend
---?color=linear-gradient(180deg, #1E5C97 100%, black 0%)


### Merge-Konflikte

@ol[text-07]
- So ein File sieht dann in etwa so aus:
@olend
@snap[span-100]
```bash zoom-09
<<<<<<< HEAD:index.html
<div id="footer">contact : email.support@github.com</div>
=======
<div id="footer"> please contact us at support@github.com</div>
>>>>>>>
iss53:index.html
```
@snapend

@ol[text-07]
- Eine Mögliche Lösung wäre:
@olend

@snap[span-100]
```bash zoom-09
<div id="footer">
please contact us at email.support@github.com
</div>
```
@snapend
@snap[west-south span-100]
@ol[list-spaced-bullets text-06]
1. **Aufgabe** : Merged den Branch *`jbremer/merge_konfliktA`* in *`jbremer/merge_konfliktB* und behebt den Merge-Konflikt sodass alle Informationen bestehen bleiben.
1. **Aufgabe** : Probiert das Ganze noch mal mit einem merge-tool eurer Wahl. Um dies einzustellen, nutzt dafür **git mergetool --tool-help**
@olend
@snapend

---?color=linear-gradient(180deg, #1E5C97 100%, black 0%)
### Stash

@snap[west-south span-100]
@ol[list-spaced-bullets text-07]
- Bevor man Dinge rückgängig macht noch ein paar Infos. Es gibt einige gefährliche Kommandos, die **uncommittete Änderungen verwerfen**.
- Wenn man diese benutzen will, sollte man noch mal *git commit* oder git *stash* ausführen.
- *git stash* macht einen Snapshot von allen Änderungen im Repo und im Index ohne dass ein *git add* nötig wäre. Danach setzt der Befehl das Working Directory wieder auf HEAD zurück.
- mit *git stash list* lassen sich alle gestashten Snapshots anzeigen
- mit *git stash apply* kann man diese nach einem Reset wieder anwenden
@olend
@snapend

---?color=linear-gradient(180deg, #1E5C97 100%, black 0%)
#### Dinge rückgängig machen - reset

@snap[span-100]
```bash zoom-09
git reset --soft HEAD
git reset HEAD
git reset --hard HEAD (!)
git reset --hard origin/<branchname> (!)
```
@snapend

@[1](Git reset gibt es in drei Modi. *soft*, *mixed* und *hard*)
@[1](Soft tut committete Änderungen in die staging Area)
@[2](Mixed, der default tut committete Änderungen auf unstaged)
@[3](Hard löscht uncommittete die Änderungen)
@[4](Diesen Befehl brauche ich häufig wenn jemand anders geforce-pushed hat.)

@snap[south span-100]
@img[shadow](assets/img/reset.jpg)
@snapend
---?color=linear-gradient(180deg, #1E5C97 100%, black 0%)
#### Dinge rückgängig machen - weiteres
@snap[span-100]
```bash zoom-09
git checkout <commit> (!)
git checkout <commit> -- <filename> (!)
git revert <commit>
git clean -fdx <path> (!)
```
@snapend
@[1](Ändert den HEAD, sodass er auf den Commit zeigt. Wie das bekannte git checkout `<branch>`)
@[2](Checked das File in `<commit>`aus. Deine Änderungen werden verworfen. )
@[3](Erstellt einen **`revert commit`**, der genau das Gegenteil von **`<commit`** tut )
@[4](Löscht **unversionierte** files im Repository.  -x keine Ignorerules benutzen, -f force, -d directories )

---?color=linear-gradient(180deg, #1E5C97 100%, black 0%)
#### Dinge rückgängig machen - rebase

@snapend
@snap[north-south span-100]
@ol[list-spaced-bullets text-07]
- Mithilfe von git commit --amend kann man einen neuen Commit erstellen, der an die Stelle des alten gestellt wird.
- Mithilfe von **git rebase -i** kann man in die Vergangenheit reisen um einen früheren commit als HEAD zu ammenden.
- Man kann auch commits zusammenfügen oder nur die commit message verändern.
@olend
@snapend
@snap[span-100]
```bash zoom-09
git commit --amend
git rebase -i @~x
# Commands:
# p, pick = use commit
# r, reword = use commit, but edit the commit message
# e, edit = use commit, but stop for amending
# s, squash = use commit, but meld into previous commit
# f, fixup = like "squash", but discard this commit's log message
# x, exec = run command (the rest of the line) using shell
# d, drop = remove commit

```
@snapend

@[1](Wie ein kleiner Rebase. Wenn **git add** und **git commit --amend** ausgeführt werden, wird ein neuer Commit erstellt und an Stelle des alten gesetzt.)
@[2](Wenn man frühere commits als HEAD abändern will. )
@[3-10](Optionen beim interaktiven Rebase)

---?image=assets/img/code.jpg&opacity=60&position=left&size=45% 100%

#### Dinge rückgängig machen - Aufgaben
@snap[west-south span-100]
@ol[list-spaced-bullets text-07]
1. **Aufgabe**: Macht einen Commit, und fügt mit *git commit --amend* noch ein weiteres File zu dem Commit hinzu.
1. **Aufgabe**: Macht einen Commit, ändert eine Kleinigkeit, die ihr auch committed. Nun fügt ihr diese mit Fixup wieder zusammen.
1. **Aufgabe**: Findet einen Commit von Florian und ändert die Historie so ab, dass es so aussieht als ob er viele Pep-8 inkompatible Änderungen gemacht hätte.
1. **Aufgabe**: Fügt alle Commits aus Bug #51718 zusammen. Nutzt squash und fixup nach belieben.
@olend
@snapend

---?image=assets/img/code.jpg&opacity=60&position=left&size=45% 100%
#### Git reflog
@snap[west-south span-100]
@ol[list-spaced-bullets text-07]
- Kommando: git reflog
- Mit **git reflog** lassen sich alle Commits referenzieren, die in eurem lokalen Repo bisher gemacht wurden.
- Ihr könnt also mithilfe von **checkout** alle bisher gemachten Änderungen, auch die bei der ihr die Historie verändert habt, wieder rückgängig machen.
- Um den jetzigen Head auf den alten Commit zu resetten: git reset `<commit>`
- Um den HEAD des Branches auf einen anderen commit zu setzen: **`git branch -f <branchname> <commit>`**
@olend
@snapend

@snap[west-south span-100]
@ol[list-spaced-bullets text-07]
1. Aufgabe: Macht eure Zusammenführung von Bug #51718 wieder rückgängig und nutzt dafür **git reflog**
@olend
@snapend


---?image=assets/img/code.jpg&opacity=60&position=left&size=45% 100%

#### Cherry-pick
@snap[west-south span-100]
@ol[list-spaced-bullets text-07]
- **`git cherry-pick`** : Damit kann man commits aus anderen Branches auf den eigenen anwenden.
- **`git cherry-pick A~..B`** : Mehrere Commits cherry-picken A-B inklusive A (daher das **^**).
- ** git cherry-pick -n ** : Cherry-picken ohne einen commit zu erstellen
- ** git cherry-pick -n commit1 commit3 ; git commit ** Mehrere commit cherry-picken und dann in eins comitten.
@olend
---?image=assets/img/code.jpg&opacity=60&position=left&size=45% 100%

#### Allgemeine Aufgaben
@snap[west-south span-100]
@ol[list-spaced-bullets text-07]
1. Mache einen Commit auf dem 4.4-5 Branch und dann zieh ihn auf einen neuen Branch um. 4.4-5 sollte diesen Commit dann nicht enthalten.
1. Mache deine lokalen Änderungen **an einem File** rückgängig. Nicht am Rest des Repositories
1. Der Branch `jbremer/cherry` ist veraltet. Cherry-picked die ersten drei commits, die seit dem fork von jbremer/cherry zu 4.4-5 entstanden sind. Erstellt diesen cherry-pick als einen commit
@olend
@snapend

---?image=assets/img/code.jpg&opacity=60&position=left&size=45% 100%
#### Git submodule
@snap[west-south span-100]
@ol[list-spaced-bullets text-07]
- Manchmal haben git repos git repos
- Ob es welche gibt sieht man an **git submodule status**
- An diese kommt man mit **git submodule init --recursive**
- Beispiel: **ucs-ec2-tools**
- Löschen kann man diese wieder mit **git submodule deinit**
@olend
@snapend
---?image=assets/img/code.jpg&opacity=60&position=left&size=45% 100%
#### Gute Quellen

@snap[west-south span-100]
@ol[list-spaced-bullets text-07]
- **man git** und **man git `command`** (natürlich)
- progit https://git-scm.com/book/de/v2
- **oh shit, git** https://ohshitgit.com/
@olend
@snapend
---?image=assets/img/code.jpg&opacity=60&position=left&size=45% 100%
## **Danke** für eure Aufmerksamkeit
