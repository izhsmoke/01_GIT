# Шпаргалка о работе с Git и GitHub
Git - система контроля версий

--

## Регистрация на GitHub
1.

## Создание удаленного репозитория
1. Зайти в профиль GitHub
	>https://github.com/username
	
2. Создаем репозиторий
	- Repositories
	- New 
	- Ввести название
	- 	

## SSH-ключи
1. Генерируем SSH-ключ
	>$ ssh-keygen -t rsa -b 4096 -C "электронная почта, к которой привязан ваш аккаунт на GitHub"
	
2. Копировать содержимое ключа в буфер обмена:
	>$ clip < ~/.ssh/id_rsa.pub
	
3. Привязываем SSH-ключ к GitHub
	> Заходим в аккаунт GitHub -> Settings -> SSH and GPG keys -> New SSH key -> Вводим название и вставляем скопированный в буфер обмена ключ -> Add SSH key
	
4. Проверка ключа
	>$ ssh -T git@github.com
	>
	>Ввести YES
	>
	>Получить в ответ: *Hi %ВАШ_АККАУНТ%! You've successfully authenticated, but GitHub does not provide shell access.*
	
--
	
