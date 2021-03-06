# tf3rd
Third lab SMOMI

1. На первом этапе нам предстояло обучить самодельную сеть VGG16. Почти постоянно наам не хватало ресурсов, чтобы обучить ее хорошо. И зачастую потери у нас уходили в нан, в то время как точность держалась на довольно низких показателях. Ниже можно результаты одной из вариаций такой сети. В файле train.py лежит код с этой сетью VGG16.

Параметры для 1-ой попытки: 
    ```BATCH_SIZE = 4 *** lr=0.000000001 ```
    
![Image alt](https://github.com/deeChyz/tf3rd/blob/master/1st(b).jpg)

Я получил неудовлетворительные результаты. На грифике можно увидеть, что график не становится асимптотой. И через несколько попыток, по итогу уменьшив Learning Rate, я пришел к таким следующим результатам:
    

Итоговые параметры:
    ```BATCH_SIZE = 8 *** lr=0.0000002 ```

![Image alt](https://github.com/deeChyz/tf3rd/blob/master/1st.jpg)

Ссылка на коммит по первому этапу -- https://github.com/deeChyz/tf3rd/commit/970754563efbf50d823cac6d163d368963a79f90


2. На втором же этапе мы проводили обучение классификатора на предобученной на imagenet сети VGG16. В сети были заморожены сверточные слои.
Параметры:
    ```BATCH_SIZE = 8 *** lr=0.00000007 ```    

![Image alt](https://github.com/deeChyz/tf3rd/blob/master/2nd.jpg)

Параметры:
    ```BATCH_SIZE = 8 *** lr=0.0000001 ```    

![Image alt](https://github.com/deeChyz/tf3rd/blob/master/noSmoothing/2nd(b).jpg)

Параметры:
    ```BATCH_SIZE = 8 *** lr=0.000001 ```    

![Image alt](https://github.com/deeChyz/tf3rd/blob/master/noSmoothing/2nd(c).jpg)


Ссылка на коммит по второму этапу -- https://github.com/deeChyz/tf3rd/commit/9c8a8364f6cb424e7e0bc24981727acdeac8a4b7


3. На третьем этапе мы разморозили сверточные слои и использовали весовые коэффициенты из предыдущей попытки.


Моя первая попытка не увенчалась успехом. Мало эпох и некорректные параметры (```BATCH_SIZE = 4 *** lr=0.000000001 ```) дали такой результат:

![Image alt](https://github.com/deeChyz/tf3rd/blob/master/3rd(c).jpg)


Во второй попытке я попровал изменить параметры и сделать больше эпох. Параметры: ```BATCH_SIZE = 8 *** lr=0.00000000002 ```

![Image alt](https://github.com/deeChyz/tf3rd/blob/master/3rd(d).jpg)

Для того learning rate'a эпох оказалось много и сеть успела переобучиться уже после 40 эпохи.


На третий раз я пришел к тому, что надо увеличить learning rate и кол-во эпох в определенном соотношение, чтобы сеть неначала переобучаться на определенном этапе. С параметрами ```BATCH_SIZE = 8 *** lr=0.000000000022 ``` у меня получились следующие графики:

![Image alt](https://github.com/deeChyz/tf3rd/blob/master/3rd(a).jpg)

Без сглаживания: 

![Image alt](https://github.com/deeChyz/tf3rd/blob/master/noSmoothing/3rd(a).jpg)

К сожалению, я опять неправильно выставил параметры и получил переобученную сеть.


И в итоговой попытке я попровал в два раза уменшить learning rate, оставит при этом окло 80 эпох, и вот, что из этого вышло: 
    

![Image alt](https://github.com/deeChyz/tf3rd/blob/master/3rd(b).jpg)

Без сглаживания: 

![Image alt](https://github.com/deeChyz/tf3rd/blob/master/noSmoothing/3rd(b).jpg)

Итоговые параметры: ```BATCH_SIZE = 8 *** lr=0.000000000011 ```

Ссылка на коммит по третьему этапу -- https://github.com/deeChyz/tf3rd/commit/91ab36f655f7361ac2804bb7e922ebee513d016d
