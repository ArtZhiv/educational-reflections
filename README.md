# educational-reflections

[![Release](https://img.shields.io/github/release/golang-standards/project-layout.svg?style=flat-square)](https://github.com/ArtZhiv/educational-reflections)

![Go](https://img.shields.io/badge/go-%2300ADD8.svg?style=for-the-badge&logo=go&logoColor=white)
![YAML](https://img.shields.io/badge/yaml-%23ffffff.svg?style=for-the-badge&logo=yaml&logoColor=151515)
![PowerShell](https://img.shields.io/badge/PowerShell-%235391FE.svg?style=for-the-badge&logo=powershell&logoColor=white)
![Shell Script](https://img.shields.io/badge/shell_script-%23121011.svg?style=for-the-badge&logo=gnu-bash&logoColor=white)
![Rust](https://img.shields.io/badge/rust-%23000000.svg?style=for-the-badge&logo=rust&logoColor=white)

![Neovim](https://img.shields.io/badge/NeoVim-%2357A143.svg?&style=for-the-badge&logo=neovim&logoColor=white)
![Obsidian](https://img.shields.io/badge/Obsidian-%23483699.svg?style=for-the-badge&logo=obsidian&logoColor=white)
![Visual Studio Code](https://img.shields.io/badge/Visual%20Studio%20Code-0078d7.svg?style=for-the-badge&logo=visual-studio-code&logoColor=white)

![openSUSE](https://img.shields.io/badge/openSUSE-%2364B345?style=for-the-badge&logo=openSUSE&logoColor=white)
![Windows](https://img.shields.io/badge/Windows-0078D6?style=for-the-badge&logo=windows&logoColor=white)

## Project Layout

```bash
.
├── /api                 # Спецификации OpenAPI/Swagger, JSON schema файлы, файлы определения протоколов.
├── /assets              # Другие ресурсы, необходимые для использования вашего репозитория (изображения, логотипы и т.д.)
├── /build               # Сборка и непрерывная интеграция (Continuous Integration, CI). Поместите файлы конфигурации и скрипты облака (AMI), контейнера (Docker), пакетов (deb, rpm, pkg) в директорию /build/package. Поместите ваши файлы конфигурации CI (travis, circle, drone) и скрипты в директорию /build/ci.
│   └── /ci
│   └── /package
├── /cmd                 # Основные приложения для текущего проекта. Имя директории для каждого приложения должно совпадать с именем исполняемого файла, который вы хотите собрать (например, /cmd/myapp).
├── /configs             # Шаблоны файлов конфигураций и файлы настроек по-умолчанию.
├── /deployments         # Шаблоны и файлы конфигураций разворачивания IaaS, PaaS, системной и контейнерной оркестрации (docker-compose, kubernetes/helm, mesos, terraform, bosh).
├── /docs                # Проектная и пользовательская документация (в моём случае моя личная wiki). Создаётся в Obsidian.
│   └── /assets
├── /init                # Файлы конфигураций для инициализации системы (systemd, upstart, sysv) и менеджеров процессов (runit, supervisord).
├── /internal            # Внутренний код приложения и библиотек. Это код, который не должен использоваться в других приложениях и библиотеках. Вы можете добавить дополнительное структурирование, чтобы разделить открытую и закрытую части вашего внутреннего кода. Такой подход не является необходимым, особенно для маленьких проектов, но позволяет сразу визуально оценить применение кода. Код самого приложения может находиться в директории /internal/app (например, /internal/app/myapp), а код, который это приложение использует - в директории /internal/pkg (например, /internal/pkg/myprivlib).
├── README.md
└── /scripts             # Скрипты для выполнения различных операций сборки, установки, анализа и т.п. операций.
```
