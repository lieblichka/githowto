###### Данное руководство является копией сайта [GITHOWTO](https://githowto.com/) на языке [MARKDOWN](https://gist.github.com/Jekins/2bf2d0638163f1294637) с дополнениями от [LIEBLICHKA](https://github.com/lieblichka/)
---

# 1. Подготовка
Цели
- Быть полностью готовым к работе с Git. 
## 1.1 Настройка имени и адреса электронной почты
Если вы никогда раньше не использовали git, сначала вам нужно указать свое имя и адрес электронной почты. Выполните следующие команды, чтобы сообщить git ваше имя и адрес электронной почты. Если git уже установлен, перейдите к концу строки.
```bash
git config --global user.name «Ваше имя»
git config --global user.email "your_email@whatever.com" 
```
Проверьте результат выполнения предыдущей команды:
```bash
git config --global user.name &&  git config --global user.email
```

```
Your_name
Your_email@whatever.com
```
## 1.2 Варианты установки: окончания строк
Также для пользователей Unix/Mac:
```bash
git config --global core.autocrlf input
git config --global core.safecrlf warn
```

Для пользователей Windows: 
```bash
git config --global core.autocrlf true
git config --global core.safecrlf warn
```
---

# 2. Создание проекта 
Цели
- Узнать, как создать git-репозиторий с нуля.
## 2.1 Создайте надпись «Hello, World!» страница
Начните работу в пустом рабочем каталоге (например, work, если вы загрузили файл на предыдущем шаге) и создайте пустой каталог с именем «hello», затем создайте hello.htmlфайл в нем со следующим содержимым.
```bash
mkdir hello
cd hello
touch hello.hmtl
```
`Hello, World!`
