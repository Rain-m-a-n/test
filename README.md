## Тестовое задание 

### Задание 

* Создать 2 WEB сервера с выводом страницы `«Hello Word! \n Server 1»` (аналогично для второго Server 2). 
* Сделать балансировку нагрузки (HA + keepalived), чтобы при обновлении страницы мы попадали на любой из WEB серверов.
* <u>**Будет плюсом использование Docker**</U>
___
1. Создал 2 Docker контейнера с **Nginx**
2. Создал 2 Docker контейнера с **Haproxy**
3. Не смог настроить **Keepalived** в контейнере
___
##### **Результат:**
* Docker контейнеры и адреса:  
  ![result](https://github.com/Rain-m-a-n/test/blob/master/pics/dock1.jpg)   
* Запрос в браузере:  
  ![result](https://github.com/Rain-m-a-n/test/blob/master/pics/dock2.jpg)  
* Обновление страницы:  
  ![result](https://github.com/Rain-m-a-n/test/blob/master/pics/dock3.jpg)  
* Статистика HAProxy:  
  ![result](https://github.com/Rain-m-a-n/test/blob/master/pics/dock4.jpg)  

### Задание 2.2 (усложненное)

* Написать роль на Ansible по развёртыванию стенда из Задание *2.1*. Должен быть описан файл инвентори с серверами.  
  **Роль Nginx** – устанавливает и конфигурирует Nginx на группе хостов `[webservers]`.  
  **Роль HA Proxy** – устанавливает и конфигурирует HA Proxy на группе хостов `[loadbalancers]`.  
  **Роль Keepalived** – устанавливает и конфигурирует Keepalived на группе хостов.   
  **Конфигурационные файлы** - <u>nginx</u>, <u>HA proxy</u>, <u>keepalived</u> оформить, используя шаблоны **Jinja2.**    
___

Плейбук пожно посмотреть перейдя по ссылке [playbook](https://github.com/Rain-m-a-n/test/blob/master/nginx_haproxy.yml)
* Краткое описание шагов:   
![result](https://github.com/Rain-m-a-n/test/blob/master/pics/play.jpg)  
* Результат выполенния <u>playbook:</u>
![result](https://github.com/Rain-m-a-n/test/blob/master/pics/play_res.jpg)  
* Проверка работоспособности:
  * Открываем адрес заданный в настройках keepalived:
  ![result](https://github.com/Rain-m-a-n/test/blob/master/pics/1.jpg)  
  * Обновляем страницу:
  ![result](https://github.com/Rain-m-a-n/test/blob/master/pics/2.jpg)
  * Также открываем страницу статистики:
  ![result](https://github.com/Rain-m-a-n/test/blob/master/pics/3.jpg)  
---
* **Отказоустойчивость**:
  * Система продолжит работать, если отключится сервер **haproxy-02** (так как он выполняет роль дублирующего).
  * Система продолжит работать, если отключится один из web серверов. 
  * Система ${\color{red}перестанет}$ ${\color{red}работать}$, если отключится сервер **haproxy-01** т.к. он выполняет роль мастера. Этот момент можно исправить в конфигурационном файле **keepalived.conf**. Но к сожалению не хватило времени для донастройки. 
  
  
  
  

