Инструкция по копированию репозитория со всеми ветками, тегами и историей из одного репо в другое, на примере Gitlab.

1. Копируем репо с ключом --mirror
git clone --mirror ssh://git@gitlab.example.com:1000/cms/bitrix.git

2. Удаляем текущий origin
git remote rm origin

3. Добавляем новый origin чтобы в него пошел push
git remote add origin git@gitlab.example2.com:sf/cms-bitrix.git

Пушим все со всеми ветками
4. git push origin --all

Главное: в Gitlab нужно создать новый репо, но не инициализировать его, иначе ветка master не синхронизируется и упадет с ошибкой:

! [rejected]        master -> master (fetch first)
error: не удалось отправить некоторые ссылки в «gitlab.example2.com:sf/cms-bitrix.git»
подсказка: Updates were rejected because the remote contains work that you do not
подсказка: have locally. This is usually caused by another repository pushing to
подсказка: the same ref. If you want to integrate the remote changes, use
подсказка: 'git pull' before pushing again.
подсказка: See the 'Note about fast-forwards' in 'git push --help' for details.

Но если вы уже создали новый репозиторий и инициализировали его, то можно разрешить force push в ветку master, для этого нужно:

1. Зайти в настройки проекта в Gitlab: Settings - Repository - Protected branches
2. Включить "Allowed to force push" (по-умолчанию выключено)
3. В п.4 инструкции заменить команду с push на следующую

git push origin --all --force

