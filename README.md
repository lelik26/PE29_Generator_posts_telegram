# Генератор постов и иллюстраций для Telegram
**Этот проект представляет собой инструмент для автоматической генерации постов и иллюстраций для Telegram с использованием OpenAI и библиотеки Telethon**. 
Проект состоит из двух основных частей:

1 . Генерация текстовых постов с помощью OpenAI GPT-4.

2 . Генерация иллюстраций с помощью Stability AI и добавление текста на изображения с использованием библиотеки Pillow.

## Основные функции
### 1. Генерация текстовых постов
Установка библиотеки OpenAI: Проект использует библиотеку OpenAI для генерации текстовых постов на заданные темы.

Генерация постов: Скрипт позволяет генерировать посты на различные темы, такие как "Померанский шпиц", "Уход за шпицом" и другие.

Расширенный скрипт: Включает генерацию заголовков, мета-описаний и SEO-оптимизированного контента.

### 2. Генерация иллюстраций
Stability AI: Используется для генерации изображений на основе текстовых запросов.

Добавление текста на изображения: С помощью библиотеки Pillow на сгенерированные изображения добавляется текст, что делает их подходящими для публикации в Telegram.

Форматирование изображений: Изображения могут быть обрезаны до соотношения 9:16, что идеально подходит для stories в Telegram.

### 3. Интеграция с Telegram
Telethon: Библиотека Telethon используется для автоматической отправки сгенерированных постов и изображений в Telegram.

Асинхронная работа: Скрипт поддерживает асинхронное выполнение, что позволяет отправлять несколько запросов одновременно.

## Установка и использование
### 1. Установка зависимостей:

```
bash

pip install openai pillow telethon requests
```
### 2. Настройка API-ключей:

***Получите API-ключи для OpenAI и Stability AI.***

### 3.Установите ключи в скрипте:



````
python
    os.environ["OPENAI_API_KEY"] = "ваш_api_ключ_openai"
````

### 3. Запуск скрипта:

#### Для генерации постов:



````
python
    python generate_posts.py
````

#### Для генерации и отправки изображений:


````
python
     python generate_images.py
````
### 4. Интеграция с Telegram:

Убедитесь, что у вас есть API ID и API Hash от Telegram.

Запустите скрипт для отправки постов и изображений в Telegram:

```
python

    python send_to_telegram.py
```

Примеры использования
### Генерация поста

```
python

def generate_post(topic):
    prompt_post = f"Напишите подробный пост для блога на тему: {topic}."
    response_post = openai.chat.completions.create(
        model="gpt-4",
        messages=[{"role": "user", "content": prompt_post}],
        max_tokens=50,
        n=1,
        stop=None,
        temperature=0.7,
    )
    post_content = response_post.choices[0].message.content.strip()
    return post_content
```
    
### Генерация изображения

```
python

response = requests.post(
    f"https://api.stability.ai/v2beta/stable-image/generate/core",
    headers={
        "authorization": f"Bearer ваш_api_ключ_stability",
        "accept": "image/*"
    },
    files={"none": ''},
    data={
        "prompt": "Pomeranian small spitz with a beautiful muzzle",
        "output_format": "jpeg",
    },
)
```

### Отправка в Telegram
```
python

async def main():
    async with TelegramClient('session', api_id, api_hash) as client:
        await client.send_file(
            entity='ваш_канал',
            file='./story_rutext2.jpg',
            caption="This simulates a story!",
            ttl_seconds=42
        )
```

## Заключение
Этот проект позволяет автоматизировать процесс создания и публикации контента в Telegram, что может быть полезно для ведения блогов, каналов или просто для развлечения. Используя мощь OpenAI и Stability AI, вы можете создавать уникальные посты и иллюстрации, которые привлекут внимание вашей аудитории.

