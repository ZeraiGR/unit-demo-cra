ДЗ "Инфраструктура"

1. Установлен прекоммит хук, чтобы бить по рукам за коммиты, которые не соответствуют формату conventional commits
1. В ci пайплайне также присутствует проверка на conventional commits
1. При создании любого пулл реквеста запускается ci .github/workflows/pr-ci.yaml, который переиспользует базовые таски (сборка, тесты, линтеры)
1. Так как стоит триггер на types synchronize (pr-ci.yaml 5 строчка), то проверка запускаются автоматом на каждый коммит в PR (на последний, если было несколько)
1. Результат проверки виден на странице PR а также настроено ограничение на мерж, если проверки не прошли.
1. При пуше в ветку master также запускается ci .github/workflows/push-to-master-ci.yaml, т.к до нашего пулл реквеста ветка master могла обновиться
1. При пуше релизного тега запускается release ci  .github/workflows/release-ci.yaml
1. Все необходимые задачи в рамках резизного флоу выполняются успешно. 

### Как запушить релизный тег

```
git add .
git commit -m 'fix: something'
```

Посмотреть версию последнего текущего релиза, прибавить 1 и записать ниже вместо звёздочки.

```
git tag -a v* -m 'v*'
git push origin v*
```

### Использованные фичи

1. Reusing workflows: https://docs.github.com/en/actions/using-workflows/reusing-workflows#creating-a-reusable-workflow
1. Defining outputs for jobs: https://docs.github.com/en/actions/using-jobs/defining-outputs-for-jobs
1. auto-changelog - для генерации changlog: https://github.com/cookpete/auto-changelog
1. commitlint - для проверки коммитов: https://commitlint.js.org/
1. actions/upload-artifact@v3 и actions/download-artifact@v3 - для работы с артефактами: https://github.com/actions/upload-artifact and https://github.com/actions/download-artifact
1. github cli - для создания релиза: https://cli.github.com/
1. peter-evans/close-issue@v3 - для закрытия issue: https://github.com/peter-evans/close-issue
1. JasonEtco/create-an-issue@v2 - для создания issue на базе шаблона: https://github.com/JasonEtco/create-an-issue
1. JamesIves/github-pages-deploy-action@v4 - для деплоя приложения: https://github.com/JamesIves/github-pages-deploy-action



В этом репозитории находится пример приложения с тестами:

- [e2e тесты](e2e/example.spec.ts)
- [unit тесты](src/example.test.tsx)

Для запуска примеров необходимо установить [NodeJS](https://nodejs.org/en/download/) 16 или выше.

Как запустить:

```sh
# установить зависимости
npm ci

# запустить приложение
npm start
```

Как запустить e2e тесты:

```sh
# скачать браузеры
npx playwright install

# запустить тесты
npm run e2e
```

Как запустить модульные тесты:

```sh
npm test
```
