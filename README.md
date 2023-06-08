# Workflows

![GitHub release (latest SemVer)](https://img.shields.io/github/v/release/pacific-agency/workflows?color=%23aac811&label=%D0%A0%D0%B5%D0%BB%D0%B8%D0%B7)

Репозиторий с переиспользуемыми `workflows`.

## Использование

Для использования необходимо создать обычный `workflow`-файл.

После создания какой-либо `job`, в ней указываем:

```yml
uses: Pacific-Agency/workflows/.github/workflows/<Название workflow>.yml@<Версия workflow>
```

### Пример

```yml
name: CI
on:
  pull_request:
    branches:
      - main
jobs:
  build:
    uses: Pacific-Agency/workflows/.github/workflows/build.yml@v0.1.0

```

## Создание новых `workflow`

Создавать новый `workflow` необходимо в папке `.github/workflows`, вложенные папки не поддерживаются. Перед файлом необходимо указать префикс, если он относится только к части репозиториев, например `frontend-build.yml` или `backend-black.yml`.

В файле необходимо указать:

```yml
name: Название Workflow

on:
  workflow_call:
```

Для того, чтобы задать `inputs` и `secrets`, нужно их также указать в начале файла. Пример:

```yml
on:
  workflow_call:
    inputs:
      version:
        description: "Версия для package.json"
        required: true
        type: string
    secrets:
      GPG_PRIVATE_KEY:
        required: true
        description: "Ключ для подписи коммита"
```

После этого создается `jobs`, в котором всё указывается также, как и в обычном `workflow`.
