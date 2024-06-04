# IC50_prediction

### Постановка задачи

Необходимо предсказать значение **IC50** - концентрация полумаксимального ингибирования, — показатель эффективности лиганда при ингибирующем биохимическом или биологическом взаимодействии. Этот показатель обычно используется в качестве индикатора активности вещества-антагониста в фармакологических исследованиях. 


### Материалы

**Исследование данных**, построение графиков распределения, графиков предполагаемых зависимостей в данных [research.ipynb](research.ipynb)


**Основное решение**: [baseline.ipynb](baseline.ipynb)
* Предобработка данных
* Удаление выбросов
* Добавление признаков-дескрипторов
* Эксперимент с расширешением датасета с использованием стандартного отклонения таргета и предсказанием с учётом погрешности на это отклонение
* Добавление эмбеддингов и признаков MOLVEC
* Попытка свести задачу регрессии к классификации и метрики классификации
* Использование бустингов (catboost, XGboost, LightGBM)
* Реализация архитектуры DeepIC50 на torch, https://github.com/labnams/DeepIC50
* Проба KAN


**Эксперименты с получением эмбеддингов и использование их для предсказаний**: [ic50_1.ipynb](ic50_1.ipynb)
* LLAMA
* MolTransformerEmbeddings
* RegNet (MLP)
* WineNet (MLP)
* Сведение задачи к классификации
* Padelpy descriptors (использование максимального количества дескрипторов ~2500)
* KAN


**CHEMBert**: [Untitled3.ipynb](Untitled3.ipynb)


**Ещё некоторые эксперименты**: [ic50_3.ipynb](ic50_3.ipynb)


### Результаты, выводы

1) Использование бустингов - более оптимально, чем нейросетевых архитектур
2) **Best R2 score** = 0.23
3) Расширешение датасета с использованием стандартного отклонения таргета (target, target + std, target - std) только запутало модель, R2 упал в два раза
4) Предсказание с учётом на погрешность в 2 * std показало **Accuracy 76%**, а с учётом на погрешность в std показало **Accuracy 50%**. Если взять модель регрессии с более высоким показателем R2 (например, у наших коллег), думаем, точность попадания будет близка к 1.


### Участники

Анисимова Надежда, Ульянова Мария, Мальцев Никита