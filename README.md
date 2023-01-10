# **Проект «API для Yatube»**
---

## **Описание проекта:**
Социальная сеть "Yatube" , которая дает возможность писать посты , коментировать их , и подписываться на понравившихся авторов.
Основная цель и польза этого проекта - научить меня работать с API , Django , djangorestframework , Python

---

## **Технологии**
Python 3.7.0 ,
Django 3.2.16 ,
Visual Studio Code ,
Postman

---

## **Как развернуть проект на локальной машине:**
Visual Studio Code , терминал bash , директория с проектами (C/Dev/)
- git clone https://github.com/Rishat-Ver/api_final_yatube.git (Клонирую проект с GitHub)
- cd api_final_yatube/ (Переходим в папку нашего проекта)
- python -m venv venv (Установка виртуального окружения)
- source venv/Scripts/activate (Активация виртуального окружения)
- python -m pip install –upgrade pip (Обновил pip)
- pip install -r requirements.txt (Установка зависимостей из файла requirements.txt)
- python manage.py migrate (Сделал миграции)
- python manage.py runserver (Запустил проект в режиме разработке)
### **Дополнительно установил:**
- pip install djoser djangorestframework-simplejwt==4.7.2 (Для работы с JWT в Django установите и подключите две библиотеки Djoser и Simple JWT)
- pip install flake8 (Устоновка flake8)
- pip install isort (Установка isort)

---

## **Задание**
Ваша задача — дописать код и привести его в соответствие с документацией: добавить недостающие модели в приложении posts, создать адреса и представления для обработки запросов в приложении api. Документация — это ваше техническое задание.

Например, в проекте должна быть описана модель Follow, в ней должно быть два поля — user (кто подписан) и following (на кого подписан). Для этой модели в документации уже описан эндпоинт /follow/ и два метода: 

-  GET — возвращает все подписки пользователя, сделавшего запрос. Возможен поиск по подпискам по параметру search
-  POST — подписать пользователя, сделавшего запрос на пользователя, переданного в теле запроса. При попытке подписаться на самого себя, пользователь должен получить информативное сообщение об ошибке. Проверка должна осуществляться на уровне API.

Анонимный пользователь на запросы к этому эндпоинту должен получать ответ с кодом 401 Unauthorized. 

Сейчас ни самой модели Follow, ни обработчиков запросов в коде нет. Надо их написать.

### **Ключевые моменты**
-  Применяйте вьюсеты.
-  Для аутентификации используйте JWT-токены.
-  У неаутентифицированных пользователей доступ к API должен быть только на чтение. Исключение — эндпоинт /follow/: доступ к нему должен предоставляться только аутентифицированным пользователям.
-  Аутентифицированным пользователям разрешено изменение и удаление своего контента; в остальных случаях доступ предоставляется только для чтения.
-  Добавление новых пользователей через API не требуется.

### **Подсказки**
-  Для проверки прав в DRF удобно использовать пермишены. При необходимости пишите и применяйте собственные классы разрешений.
-  При описании вьюсетов для некоторых моделей имеет смысл наследоваться от собственного базового вьюсета. Не пренебрегайте этой возможностью.
-  Работу с JWT-токенами удобно организовать при помощи библиотеки Djoser, но выбор решения за вами.

---

## **Как я делал проект**
<sub>Разверну и дополню этот блок позже</sub>
- Для аутентификации использовал JWT-токены.
- В settings.py зарегестрировал djoser в INSTALLED_APPS
- В settings.py добавил новые настройки в REST_FRAMEWORK и SIMPLE_JWT
- Написал админку и зарегистрировал таблицы
- В api/urls.py зарегистрировал эндпоинты (groups, posts, posts/{id}/comments, follow)
- В yatube_api/urls.py (admin/, api/, redoc/)
- У меня 4 модели (Group, Post, Comment, Follow)
- У меня 4 сериализатора (GroupSerializer, PostSerializer, CommentSerializer, FollowSerializer)
- У меня 4 вьюсета (GroupViewSet, PostViewSet, CommentViewSet, FollowViewSet)
- Написал пермишен IsAuthorOrReadOnly

---

## **Примеры запросов:**
Все необходимые примеры можно получить по ссылке http://127.0.0.1:8000/redoc/
- source venv/Scripts/activate (Активируем виртуалку)
- python manage.py runserver (Запуск проекта)
- переходим по ссылке через браузер http://127.0.0.1:8000/redoc/
### ** Некоторые запросы и ответы на них:**
- **GET** http://127.0.0.1:8000/api/v1/posts/{id}/
<sub>Получить список всех публикаций. При указании параметров limit и offset выдача должна работать с пагинацией.</sub>
```json
{
"id": 0,
"author": "string",
"text": "string",
"pub_date": "2019-08-24T14:15:22Z",
"image": "string",
"group": 0
}
```

- **POST** http://127.0.0.1:8000/api/v1/posts/
<sub>Добавление новой публикации в коллекцию публикаций. Анонимные запросы запрещены.</sub>
*Создаем пост*
```json
{
"text": "string",
"image": "string",
"group": 0
}
*Пост создался*
{
"id": 0,
"author": "string",
"text": "string",
"pub_date": "2019-08-24T14:15:22Z",
"image": "string",
"group": 0
}
```

- **PUT** http://127.0.0.1:8000/api/v1/posts/{id}/
<sub>Обновление публикации по id. Обновить публикацию может только автор публикации. Анонимные запросы запрещены.</sub>
*Обновляем пост*
```json
{
"text": "string",
"image": "string",
"group": 0
}
*Обновленный пост*
{
"id": 0,
"author": "string",
"text": "string",
"pub_date": "2021-01-09T00:03:22Z",
"image": "string",
"group": 0
}
```

- **DELETE** http://127.0.0.1:8000/api/v1/posts/{id}/
<sub>Удаление публикации по id. Удалить публикацию может только автор публикации. Анонимные запросы запрещены.</sub>
*Удаление публикации по id. Удалить публикацию может только автор публикации. Анонимные запросы запрещены.*
```json
{
"detail": "Учетные данные не были предоставлены."
}
```

- **PATCH** http://127.0.0.1:8000/api/v1/posts/{id}/
<sub>Частичное обновление публикации по id. Обновить публикацию может только автор публикации. Анонимные запросы запрещены.</sub>
*Обнвляем только картинку*
```json
{
"text": "string",
"image": "new_string",
"group": 0
}
*Онавленный пост с новой картинкой*
{
"id": 0,
"author": "string",
"text": "new_string",
"pub_date": "2019-08-24T14:15:22Z",
"image": "string",
"group": 0
}
```

---

**~~Автор проекта:~~** Вергасов Ришат https://github.com/Rishat-Ver
