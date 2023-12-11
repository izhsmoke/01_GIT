# Заметки о работе с Bash, Git и GitHub
Git - система контроля версий

---

## Работа с командной строкой (BASH)
1. Текущий рабочий каталог

```
pwd
```

3. Содержимое текущего каталога

```
ls
```
    
4. Создание каталога
   
```
mkdir %НАЗВАНИЕ_КАТАЛОГА%
```

5. Копировать
   
```
cp file.txt %ПУТЬ%
```

6. Переместить
   
```
mv file.txt %ПУТЬ%
```

7. Удалить:
|   Данные      |   Команда        |
|     ---       |     ---          |
|    Файл       |> rm file.txt     |
|Пустая папка   |> rmdir /empty_DIR|
|Папка с файлами|> rm -r /DIR      |

## Регистрация на GitHub
1. Перейти на главную страницу GitHub
> https://github.com/
	
2. Проходим регистрацию

## Создание удаленного репозитория

1. Зайти в профиль GitHub
   
>https://github.com/username
	
2. Создаем удаленный репозиторий

```mermaid
graph LR
Repositories --> New --> id3["Ввести название"] --> id4["Выбрать тип приватности"] --> OK
```	

## SSH-ключи
1. Генерируем SSH-ключ

```
ssh-keygen -t rsa -b 4096 -C "электронная почта, к которой привязан ваш аккаунт на GitHub"
```
	
3. Копировать содержимое ключа в буфер обмена:

```
clip < ~/.ssh/id_rsa.pub
```
	
4. Привязываем SSH-ключ к GitHub

> Заходим в аккаунт GitHub -> Settings -> SSH and GPG keys -> New SSH key -> Вводим название и вставляем скопированный в буфер обмена ключ -> Add SSH key
	
6. Проверка ключа
```
ssh -T git@github.com
```
>Ввести <b>YES</b>
>
>Получить в ответ: *Hi %ВАШ_АККАУНТ%! You've successfully authenticated, but GitHub does not provide shell access.*
	
## Связываем локальный и удалённый репозитории
1. Открыть папку проекта
	
```
cd /папка_проекта
```
    
2. Инициализировать проект

```
git init
``` 
   
3. Добавить файл
```
git add README.md
```

4. Создать коммит

```
git commit -m "first commit"
```

5. Создать ветку
   
```
git branch -M main
```
    
6. Привязать локальный репозиторий к удалённому
   
```
git remote add origin https://github.com/%ИМЯ_АККАУНТА%/%ИМЯ_ПРОЕКТА%.git
```
	
8. Отправить изменения на удаленный репозиторий

```
git push -u origin master
```

---

## О ХЕШах
*Хеш — идентификатор коммита*

- Git преобразует информацию о коммитах с помощью алгоритма SHA-1 и для каждого из них рассчитывает уникальный идентификатор — хеш.
- Хеш — основной идентификатор коммита и позволяет узнать его автора, дату и содержимое закоммиченных файлов.
- Все хеши, а также таблицу соответствий хеш → информация о коммите Git хранит в папке ```.git```

1. Вывод истории коммитов

```
git log
```

*Вывод будет содержать:* **хеш, автора, дату и сообщение**

2. Вывод сокращенного лога

```
git log --oneline
```

3. Файл **HEAD**
- В папке .git есть служебный файл HEAD. Он указывает на самый свежий коммит.
- Вместо хеша последнего коммита можно написать слово ```HEAD```.

---

## Статусы ```untracked```/```tracked```, ```staged``` и ```modified```

- Статусом untracked помечается файл, о существовании которого Git знает, но не следит за изменениями в нём. Этот статус — противоположность tracked, в который попадают все файлы, отслеживаемые Git.
- Файл переходит в статус staged после выполнения git add.
- Статус modified означает, что файл был изменён.
- Большинство файлов в проектах «шагает» по следующему циклу:
 
```mermaid
graph LR;
  id1["изменён"]-->id2["добавлен в список на коммит"]
  id2-->id3["закоммичен"]
  id3-->id4["изменён"]
  id4-->id1
```

- Команда ```git status``` показывает, что происходит с файлом: например, он добавлен в список «на коммит» или ещё вообще не отслеживается, или изменён.
- ```git status``` показывает явно следующие состояния файлов: ```untracked```, ```staged``` и ```modified```.
- ```git status``` подсказывает, какие команды можно выполнить, чтобы поменять состояние файла.

- Сообщение коммита должно быть информативным, быть в одном стиле

## Как сделать mermaid-схему

```mermaid
graph LR;
  untracked -- "git add" --> staged
  staged    -- "git commit -m '%%СООБЩЕНИЕ%%'" --> id2["tracked/comitted"]

%% стрелка без текста для примера: 
  A --> B --> C;
```

## Исправление последнего коммита
--amend рассчитан на работу с последним коммитом (HEAD).
- Дополнить коммит новыми файлами можно с помощью

```
git commit --amend --no-edit
```

- Благодаря опции ```--no-edit``` сообщение к коммиту останется таким, каким и было.
- Изменить сообщение к коммиту позволяет команда 

## Откат на ранюю версию
Чтобы вернуть состояние репозитория к более раннему. Для этого используют команду:
```
git reset --hard <hash>
```

![опция --restore](https://pictures.s3.yandex.net/resources/M2_T6_1686651127.png)

```
git commit --amend -m "Обновлённое сообщение коммита"
```

- Чтобы «откатит» изменения в файле до последней сохранённой (в коммите или в staging) версии

```
git restore <file>
```

- Чтобы перевести файл из staged обратно в modified или untracked

```
git restore --staged <file>
```
  
- Чтобы «откатит» историю до коммита с хешем <hash>. **Более поздние коммиты потеряются!**

```
git reset --hard <commit hash>
```

## Что изменилось? (```git diff```)
- Чтобы сравнить последнюю закоммиченную версию файла с той, что находится в состоянии modifie

```
git diff
```

- Для просмотра изменения в staged-файлах относительно последних закоммиченных версий

```
git diff --staged
```

---

## .gitignore

- Git игнорирует файлы, находящиеся в файл ```.gitignore```
- Чтобы увидеть игнорируемые файлы ввести команду

```
git status --ignored
```

- Файл .gitignore — это обычный файл в репозитории. Его нужно коммитеть
