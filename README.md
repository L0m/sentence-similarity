# sentence-similarity

Особенности реализации:

1. После загрузки большого текста страница с предложениями очень сильно тормозила на стороне API.
   API не поддерживает пагинацию потому было добавлено ограничение на выдачу всего 100 предложений на каждый текст.
   Это настраивается в config.py -> sentence_limit 
   
2. HTTPValidationError на прямую не используется, как я понял это соответствует формату ошибки FastAPI.
   Я не понял как предполагалось их реализовать, потому обработки ошибок сейчас прямой нет.

3. Загрузка и индексация предложений сейчас производится прямо в момент добавления документа.
   Это стоит выносить в отдельный поток, но я не стал усложнять и делать это в рамках текущего задания, 
   тем более что нет поддержки API (сколько проиндексировано и т.д.).

4. Используется Postgresql для хранения текста и предложений и elasticsearch для поиска по вектору.
   Предложения переводятся в вектор при помощи Google Universal Sentence Encoder.
