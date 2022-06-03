Отчет 8 Лаба:
Export GITHUB_USERNAME=DmitryZB
$Создаем переменную с логином git
git submodule update --init
$Инициализируем использованные сабмодули
Git remote remove origin && git remote add origin https://github.com/%{GITHUB_USERNAME}/lab08
$Удаляем и добавляем новый origin для нового репозитория
Cat >> Dockerfile <<EOF 
...
EOF
$Записываем текст в Docker-file
Docker build -t logger .
$Создаем среду с названием logger, ищем Docker-file в текущей директории
Docker images
$Смотрим информацию о средах
mkdir logs
Docker run -it -v "$(pwd)/logs/:home/logs/" logger
$Запускаем среду logger в указанном по пути каталоге
Docker inspect logger
$Выводит код среды logger
Cat logs/log.txt
$Выводим содержание файла log, записанного logger-ом
$Создаем .yml файл в GitHub actions
Git add .
$Добавляем все файлы в текущей директории
Git commit -m"commit"
Git push origin main
$Коммитим и пушим файлы в репозиторий

Содержание gitact.yml:

name: CMake

on:
  push:
    branches: [ main ]

jobs:
  build:
    # The CMake configure and build commands are platform agnostic and should work equally well on Windows or Mac.
    # You can convert this to a matrix build if you need cross-platform coverage.
    # See: https://docs.github.com/en/free-pro-team@latest/actions/learn-github-actions/managing-complex-workflows#using-a-build-matrix
    runs-on: ubuntu-latest

    steps:
    - uses: actions/checkout@v3

    - name: Install Docker
      run: sudo snap install docker
$Команда устанавливает docker
      
    - name: Run Docker
      run: sudo docker build -t logger .
$Команда билдит docker с именем (-t) - logger 


