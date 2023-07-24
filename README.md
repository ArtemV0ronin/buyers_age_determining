# Определение возраста покупателей
Ноутбук проекта находится в файле [buyers_age_determining.ipynb](https://github.com/ArtemV0ronin/buyers_age_determining/blob/main/buyers_age_determining.ipynb)  
Альтернативная [ссылка](https://colab.research.google.com/drive/10tJBwQCCBJ6S1Wsp2cQJ3VWd1zQLViYz#offline=true&sandboxMode=true) на Google Collab.


## Задача проекта
Сетевой супермаркет «Хлеб-Соль» внедряет систему компьютерного зрения для обработки фотографий покупателей. Фотофиксация в прикассовой зоне поможет определять возраст клиентов, чтобы:
- Анализировать покупки и предлагать товары, которые могут заинтересовать покупателей этой возрастной группы;
- Контролировать добросовестность кассиров при продаже алкоголя.

Необходимо построить модель, которая по фотографии определит приблизительный возраст человека.


## Описание данных
В нашем распоряжении набор фотографий людей с указанием возраста. 
Данные взяты с сайта <a href = "https://chalearnlap.cvc.uab.cat/dataset/26/description/">ChaLearn Looking at People</a>.

Данные состоят из двух папок - одна папка со всеми изображениями `/final_files` и CSV-файл `labels.csv` с двумя колонками: *file_name* и *real_age*. 


## Используемый стек
![Static Badge](https://img.shields.io/badge/tensorflow-red)
![Static Badge](https://img.shields.io/badge/keras-red)
![Static Badge](https://img.shields.io/badge/ResNet50-red)
![Static Badge](https://img.shields.io/badge/ImageDataGenerator-red)
![Static Badge](https://img.shields.io/badge/Adam-red)
![Static Badge](https://img.shields.io/badge/pandas-red)
![Static Badge](https://img.shields.io/badge/numpy-red)
![Static Badge](https://img.shields.io/badge/matplotlib-red)
![Static Badge](https://img.shields.io/badge/seaborn-red)

---
## Итоги проекта
В ходе выполнения проекта была построена модель, определяющая по фотографии приблизительный возраст человека. 

Модель построена на основе архитектуры свёрточной нейросети ResNet50, предобученная на датасете ImageNet:

- два последних слоя модели заморожены, а вместо них добавлены новые:
    - первый слой GlobalAveragePooling2D — пулинг с окном во весь тензор, чтобы получить пиксель с большим количеством каналов
    - второй слой Dense — полносвязный слой с одним нейроном и Relu активацией для задачи регрессии
- модель обучена на 10 эпохах
- дополнительных преобразований изображений не проводилось

На тестовой выборке метрика **MAE** модели равна **6.0981**.

Для улучшения качества модели, судя по распределению целевого признака, отличным решением будет дополнить выборку фотографиями людей старше 41 года.
