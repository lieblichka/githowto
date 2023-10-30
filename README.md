###### Данное руководство является копией сайта [GITHOWTO](https://githowto.com/) на языке [MARKDOWN](https://gist.github.com/Jekins/2bf2d0638163f1294637) с дополнениями от [LIEBLICHKA](https://github.com/lieblichka/)
---

# Подготовка
Цели
- Быть полностью готовым к работе с Git. 
## Настройка имени и адреса электронной почты
Если вы никогда раньше не использовали git, сначала вам нужно указать свое имя и адрес электронной почты. Выполните следующие команды, чтобы сообщить git ваше имя и адрес электронной почты. Если git уже установлен, перейдите к концу строки.

```shell
git config --global user.name «Ваше имя»
git config --global user.email "your_email@whatever.com" 
```

## Варианты установки: окончания строк
Также для пользователей Unix/Mac:
```shell
git config --global core.autocrlf input
git config --global core.safecrlf warn
```

