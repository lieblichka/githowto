# BASIC COMMANDS - базовые комманды
```
git checkout [filename]		для возврата файла в состояние текущего коммита 
git reset					для отмены индексации модифицированных файлов 
git config --global user.name "Your Name"				 Задать пользователськое имя
git config --global user.email "your_email@whatever.com" Задать пользовательскую почту
```
# ANY COMMITS - несколько коммитов за один пуш 			
```
touch a.html 
touch b.html
git add a.html b.html
git commit -m 'Changes a.html and b.html'

touch c.html
git add c.html
git commit -m 'Changes c.html'

git push
git log -n 5
```
	commit f86dd42108e5568a5d7344917e94ce81a09a3e0c (HEAD -> master, origin/master, origin/HEAD)
	Author: Marjorie Wuckert <mwuckert@intra.42.fr>
	Date:   Sat Oct 14 10:32:51 2023 +0300

	Changes c.html

	commit 3604bcbd7938c9ac67633cd9718da5c8cf9fcc9e
	Author: Marjorie Wuckert <mwuckert@intra.42.fr>
	Date:   Sat Oct 14 10:32:27 2023 +0300

	Changes a.html and b.html

	- Как видно из вывода, используя один пуш и несколько коммитов
	они автоматически разделились 

# GIT WORK WITH MODIFY NOT A COMMIT 
```
@ [let first modify] hello.html 
@ git add hello.html
@ git status 
```	
	On branch master
	Your branch is up to date with 'origin/master'.

	Changes to be committed:
	  (use "git restore --staged <file>..." to unstage)
		modified:   hello.html
```
@ [let second modify ] hello.html
@ git status
```
	Changes to be committed:
	  (use "git restore --staged <file>..." to unstage)
		modified:   hello.html

	Changes not staged for commit:
	  (use "git add <file>..." to update what will be committed)
	  (use "git restore <file>..." to discard changes in working directory)
		modified:   hello.html

	- После второй модификации первое добавленное изменение
	зафиксированно git, а вторая модификация отображается как 
	недобавленное изменение 
```
@ git commit -m 'Add new H2 tag'
```	
	On branch master
	Your branch is ahead of 'origin/master' by 1 commit.
	  (use "git push" to publish your local commits)

	Changes not staged for commit:
	  (use "git add <file>..." to update what will be committed)
	  (use "git restore <file>..." to discard changes in working directory)
		modified:   hello.html

	- После первого коммита, второе изменение так и осталось незафиксированным
```
@ git add .
@ git commit -m 'Add new HEAD tags in hello.html'
@ git push
```

# GIT LOG AND ALL ABOUT HIM
```
git log						# получение списка логов коммита
```
# FORMAT USER OUTPUT 
```
git log --pretty=oneline							# однострочный вывод логов коммита 
git log --pretty=oneline --max-count=2				# 
git log --pretty=oneline --since='5 minutes ago'	# коммиты совершенные 5 минут назад 
git log --pretty=oneline --until='5 minutes ago'	
git log --pretty=oneline --author=<your name>		# поиск коммитов по автору 
git log --pretty=oneline --all
```	
## MOST USED GIT LOG SCRIPT
			
			git log --all --pretty=format:"%h %cd %s (%an)" --since='7 days ago' --author=kovalev.g

				# Просмотра изменений, 
				сделанных за последнюю неделю.


			git log --pretty=format:"%h %ad | %s%d [%an]" --graph --date=short

		# TRANSCRIPT FLAGS

			
			--pretty="..." — определяет формат вывода.
			%h — укороченный хэш коммита
			%d — дополнения коммита («головы» веток или теги)
			%ad — дата коммита
			%s — комментарий
			%an — имя автора
			--graph — отображает дерево коммитов в виде ASCII-графика
			--date=short — сохраняет формат даты коротким и симпатичным


# GIT CONFIG ALIAS

		*В файле ~/.gitconfig  есть возможность добавлять часто используемые
		аргументы*
		
			@ cat ~/.gitconfig 

			[alias]
			  co = checkout
			  ci = commit
			  st = status
			  br = branch
			  hist = log --pretty=format:\"%h %ad | %s%d [%an]\" --graph --date=short
			  type = cat-file -t
			  dump = cat-file -p


		- Чтобы не записывать в файл вручную есть опция 
			
			git config --global alias.[aliasname] [commands]

			... EXAMPLE 
				
				git config --global alias.co checkout
				git config --global alias.ci commit
				git config --global alias.st status
				git config --global alias.br branch
				git config --global alias.hist "log --pretty=format:'%h %ad | %s%d [%an]' --graph --date=short"
				git config --global alias.type 'cat-file -t'
				git config --global alias.dump 'cat-file -p'

				# git config автоматически добавить алиасы в файл и сохранит изменения 

		
# GIT CHECKOUT

	- опция, которая позволяет возвращаться к определенному коммиту

			@ git log --pretty=oneline 
				
				aa9438e9c8cdbf0685c4e59455e920a1c2f0d9cc Modify file: lab.txt [TOP]=GIT LOG COMMANDS
				cb6bf6999a8da56c7667274635a69057710e5c3d modify manual file: lab.txt
				b1dc03eab5b2a58bf7382aafdd01f1cd6d500e3f Add new HEAD tags in hello.html
				8e258c8c85cc1d128cae684a8b372ea71556051a Add new H2 tag in hello.txt
				2f9ce451dd8924bf737a3a202677eb52b9e4d2af renamed lab_03/hello.html hello.html
				ca357b30f928ccb948d11c9eb485d713f568fa32 modify lab_03/hello.html
				09606e1b3075cb0eccbb758a4c4267e357a43507 Modify manual file: lab.txt
				f86dd42108e5568a5d7344917e94ce81a09a3e0c Changes c.html
				3604bcbd7938c9ac67633cd9718da5c8cf9fcc9e Changes a.html and b.html
				ca43fe9d3ec33fe9dc662ae6067e57b25e80b8c4 Remove c.html
				38db27b7dc7862478d4a5aa28a9fddb2f66eda3c Remove a.html and b.html
				e2dfb30da7d88d18dc84f3ae12cb1d10d6be499c Changes for a and b
				af388452419f26319ee71b362d16629418b8a7e3 modify lab_03/hello.html, new lab.txt
				5c5194a84b7e5316b98ddbd44d4a7025a6a5bd23 new file lab03/hello.html
				89aaf908c5479e0091279181c13c84008e6bbc1a Initial commit
			
			@ git checkout ca357b30f928ccb948d11c9eb485d713f568fa32 2
			@ cat lab_03/hello.html

					<h1>Hello World</h1>
					
				- Видно, что файл hello.html вернулся к прежнему состоянию

			@ git checkout master 
			@ cat hello.html  
				<html>
					<head>
					</head>
					<body>
						<h1>Hello, World!</h1>
						<h2>My name is world</>
					</body>
				</html>

			- После возврата к основной ветке, файл hello.html
			принял прежнее состояние 

# GIT TAGS

			
			- Возможность добавлять теги к коммитам
			
				@> git log --pretty=format:"%h %ad | %s%d [%an]" --graph

					* b1dc03e Sat Oct 14 11:04:33 2023 +0300 | Add new HEAD tags in hello.html [Marjorie Wuckert]
					* 8e258c8 Sat Oct 14 11:01:24 2023 +0300 | Add new H2 tag in hello.txt [Marjorie Wuckert]

					- В данном случае интересуют два коммита со старой версией hello.html
					и с более новой 

				@> git checkout b1dc03e 
				@> cat hello.html 
				
					<html>
						<head>
						</head>
						<body>
							<h1>Hello, World!</h1>
							<h2>My name is world</>
						</body>
					</html>

				@> git tag v1	 Создаем тег для текущего коммита
				@> git tag v1^	 И перемещаемся на коммит назад 
				@> cat hello.html 

					<html>
						<body>
							<h1>Hello, World!</h1>
							<h2>My name is world</>
						</body>
					</html>

				@> git tag v1-beta		Присваиваем тег текущему коммиту
				
		- Возвращаемся к предыдущему коммиту 
		
			@> git checkout v1
			@> git log --pretty=format:"%h %ad | %s%d [%an]" --graph
				
				* b1dc03e Sat Oct 14 11:04:33 2023 +0300 | Add new HEAD tags in hello.html (tag: v1)
				* 8e258c8 Sat Oct 14 11:01:24 2023 +0300 | Add new H2 tag in hello.txt (tag: v1-beta) 

				- Теперь у коммитов есть префикс с тегом


		- Для возврата к коммитам с тегами используем
			
			@> git checkout v1
			@> git checkout v1-beta
		



	


