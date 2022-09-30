## Как склеить коммиты

1. Узнаем сколько коммитов надо склеить 
`git cherry -v master | wc -l`
1. Переписываем историю на число коммитов из предыдущей команды
`git rebase -i HEAD~5` или `git rebase -i master`. В интерактивном режиме самый верхний коммит должен быть `pick`.  Он самый ранний и к нему буду приклеиватся остальные.
1. Так как история изменилась на сервер пушим с форсом 
`git push --force`

## Просим git игнорировать изменения прав файлов (chmod)
`git config core.fileMode false`
То же самое с флагом `--global` чтобы настройка применялась для всех репозиториев (использует ~/.gitconfig вместо .git/config)

## error: The following untracked working tree files would be overwritten by merge
Remote файлы несовпадают с локальными. Перепишем в пользу удаленных
```bash
git fetch --all
git reset --hard origin/master
```

## Переименовать удалённую ветку
Предположим, что у вас есть ветка oldname. Вы запушили (push) ее на удаленный репозиторий. Теперь вы хотите переименовать ее, чтобы она называлась newname.
1. Переключиться на ветку, которую вы хотите переименовать.
1. Переименовать локальную ветку командой: 
`bash git branch -m oldname newname`
1.  Удалить удаленную (remote) ветку (oldname), которую вы хотите переименовать:
`git push origin :oldname`
1. Загрузить (push) переименованную ветку newname в удаленный репозиторий:
`git push origin -u newname`


## Склонировать в текущаю папку не создавая имя репозитория
`git clone https://github.com/napastyuk/md.git .`