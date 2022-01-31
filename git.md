## Как склеить коммиты

1. В идеале вы комиитили повторные коммиты так  


1. Узнаем сколько коммитов надо склеить  
`git cherry -v master | wc -l`

1. Переписываем истьорию на число коммитов из предыдущей команды  
`git rebase -i HEAD~5`
или
`git rebase -i master`
В интерактивном режиме самый верхний коммит должен быть pick, fixup   
Он самый ранний и к нему буду приклеиватся остальные.

1. Так как история изменилась на сервер пушим с форсом  
`git push --force`

## Как поднять свою ветку
1. в репе larapress-client https://git.fabricmedia.ru/larapress/larapress-client
`git checkout -b newBranchName`
`git push`
2. тоже самое в репе проекта  https://git.fabricmedia.ru/MX/lptpl_nevnov_2017
`git checkout master`
`git checkout -b newBranchName`
`git push`
3. запустить пайплайн dev_deploy
4. примаппить свою рабочую директорию в ide к удаленной папке
5. пересобрать фронт
```bash
ssh 82.202.197.18
cd /home/dev/nevnov.ru/template/newBranchName/current
npm i && gulp v2
```
6. Ветка доступна по адресу newBranchName.dev.nevnov.ru

## Обновление ветки
1. делаю в этой ветке  
`git fetch origin master`, 
1. перезапускаю сборку фронта
`npm i && gulp gulp v2`
1. в gitlab запускаю пайплайн dev_deploy


## Игнорируем изменения прав файлов (chmod)
git config core.fileMode false
Используем флаг --global чтобы настройка применялась для всех репозиториев(использует ~/.gitconfig вместо .git/config)

git config --global core.fileMode false
## error: The following untracked working tree files would be overwritten by merge
git fetch --all
git reset --hard origin/master
