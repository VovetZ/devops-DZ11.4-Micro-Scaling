# devops-DZ11.4-Micro-Scaling

 

 

# Домашнее задание к занятию "Микросервисы: масштабирование"

 

Вы работаете в крупной компанию, которая строит систему на основе микросервисной архитектуры.

Вам как DevOps специалисту необходимо выдвинуть предложение по организации инфраструктуры, для разработки и эксплуатации.

 

## Задача 1: Кластеризация

 

Предложите решение для обеспечения развертывания, запуска и управления приложениями.

Решение может состоять из одного или нескольких программных продуктов и должно описывать способы и принципы их взаимодействия.

 

Решение должно соответствовать следующим требованиям:

 

- Поддержка контейнеров;

- Обеспечивать обнаружение сервисов и маршрутизацию запросов;

- Обеспечивать возможность горизонтального масштабирования;

- Обеспечивать возможность автоматического масштабирования;

- Обеспечивать явное разделение ресурсов доступных извне и внутри системы;

- Обеспечивать возможность конфигурировать приложения с помощью переменных среды, в том числе с возможностью безопасного хранения чувствительных данных таких как пароли, ключи доступа, ключи шифрования и т.п.

 

Обоснуйте свой выбор.

 

---

 

# Ответ

 

|Требования|K8s|Docker Swarm|Nomad|Apache Mesos|
|----------|---|------------|-----|------------|
|Поддержка контейнеров|+|+|+|+|
|Обнаружение сервисов и маршрутизацию запросов|+|+|-|+|
|Возможность горизонтального масштабирования|+|+|+|+|
|Возможность автоматического масштабирования|+|-|+|+|
|Разделение ресурсов доступных извне и внутри системы|+|-|+|+|
|Возможность конфигурировать приложения с помощью переменных среды, в том числе с возможностью безопасного хранения чувствительных данных таких как пароли, ключи доступа, ключи шифрования и т.п.|+|+|+|+|


Стандарт для кластеризации микросервисов - Kubernetes. Возможности:

 

- Поддержка контейнеров. Kubernetes поддерживает несколько сред для запуска контейнеров: `Docker`, `containerd`, `CRI-O`, и любая реализация Kubernetes `CRI` (`Container Runtime Interface`).

- Обнаружение сервисов и маршрутизация запросов. Kubernetes обеспечивает функции обнаружения сервисов и маршрутизации по запросу. В частности, система умеет переназначать необходимые для обращения к сервису IP-адрес и доменное имя сервиса различным подам, входящим в его состав. При этом обеспечивается балансировка нагрузки в стиле `Round robin DNS` между подами, чьи метки соответствуют сервису, а также корректная работа в том случае, если один из узлов кластера вышел из строя и размещённые на нём поды автоматически были перемещены на другие узлы

- Горизонтальное масштабирование. С помощью команды `kubectl` можно изменить количество реплик для быстрого масштабирования развертываний на всех узлах кластера

- Автоматическое масштабирование на основе использования ресурсов процессора, памяти и других метрик

- Разделение доступа используя разные механизмы, например, сетевые политики, метки и т.д.

- Конфигурация приложения для безопасного хранения данных с использованием переменных среды (не храня их на файловой системе) или зашифрованных секретов (которые могут быть расшифрованы только получателем)

 

Минус Kubernetes - бОльшая сложность по сравнению с конкурентами.

Из плюсов - самое большое сообщество среди всех оркестраторов, как следствие -  богатый инструментарий, большое число готовых решений.
