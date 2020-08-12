# MIL_test_noise

# Clothes Detection

## Dataset

Во-первых был подобран датасет: Common Voice (https://commonvoice.mozilla.org/ru/datasets). Объёмный, свежий, с хорошей разметкой - идеально для нашей задачи.

## +Noise

Действуем по плану:

![noise_pipeline](https://user-images.githubusercontent.com/32402386/89902314-f8bc2280-dbee-11ea-9c04-8702dd819430.png)

Some manipulations выбрано просто прибавление рандомного тензора (https://github.com/AlberetOZ/MIL_test_noise/blob/master/Noise_my_dataset.ipynb).

## Solution

По известной статье (https://arxiv.org/pdf/1609.07132.pdf) и важному результату для задачи Denoising:

![image](https://user-images.githubusercontent.com/32402386/89903179-00c89200-dbf0-11ea-839a-0a936b9bf7e2.png)

Мы будем использовать CNN, для выбора архитектуры:

![image](https://user-images.githubusercontent.com/32402386/89905079-5c941a80-dbf2-11ea-9499-2ba8965bf083.png)

Skip connections показывают отличный результат. Была выбрана CR-CED(Skip) по принципу большей точности с 16 слоями, т.к. R-CED(Skip) с 20 слоями имеет уже в 3 раза больше параметров, хотя не сильно увеличивает точность, а время на обучение у нас ограничено, особенно без сервера.

Обучать будем фреймворком tensorflow => преобразуем датасет в tfrecords формат, метрика выбрана MSE.

Полученные веса (checkpoints) лежат в https://drive.google.com/file/d/19S_St8aHIM9YEBOsbDVM8-UsFRKg7amr/view?usp=sharing

## Result

На тестовом датасете rmse: 0.3816

Мы получили неплохую демо версию (Примеры работы можно найти в ). В перспективе этот проект можно оптимизировать (тем более если ) По времени было затрачено ~25 часов. 

# That's all
