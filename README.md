## Тестовое задание 

### Задание 1.1
*	Установить VirtualBox (или VMware workstation player), разобраться как  создать виртуальную машину и создать новую vm на базе дистрибутива  Centos  (Centos это параллельная open source ветка rhel).
* Подключиться к созданной vm по ssh через любой клиент.
* Установить Python на созданной vm.
* В домашней директорий пользователя создать папку task; реализовать собственное key-values хранилище на Python. Данные будут сохраняться в файле storage.data
___
**Результат:**
* Virtual Box установлен для задачи 2.1 
* Подключение к VM по SSH работает.
* Python на VM установлен.
* По Python - было 2 ознакомительных занятия, самостоятельно выполнить задание не представляется возможным. 
* В сети нашёл код, но он не совсем корректно работает.
* Ссылка на [код](https://github.com/Rain-m-a-n/test/DB.py)

### Задание 1.2 (усложненное)
Написать сервис API на Python к key-values хранилищу из задания 1.

### Задание 2.1

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
  ![result](https://github.com/Rain-m-a-n/test/blob/master/picsdock1.jpg)   
* Запрос в браузере:  
  ![result](https://github.com/Rain-m-a-n/test/blob/master/picsdock2.jpg)  
* Обновление страницы:  
  ![result](https://github.com/Rain-m-a-n/test/blob/master/picsdock3.jpg)  
* Статистика HAProxy:  
  ![result](https://github.com/Rain-m-a-n/test/blob/master/picsdock4.jpg)  


### Задание 2.2 (усложненное)

* Написать роль на Ansible по развёртыванию стенда из Задание *2.1*. Должен быть описан файл инвентори с серверами. 
  **Роль Nginx** – устанавливает и конфигурирует Nginx на группе хостов `[webservers]`.
  **Роль HA Proxy** – устанавливает и конфигурирует HA Proxy на группе хостов `[loadbalancers]`.
  **Роль Keepalived** – устанавливает и конфигурирует Keepalived на группе хостов. 
  **Конфигурационные файлы** - <u>nginx</u>, <u>HA proxy</u>, <u>keepalived</u> оформить, используя шаблоны **Jinja2.**  
___

Плейбук пожно посмотреть перейдя по ссылке [playbook](https://github.com/Rain-m-a-n/test/nginx_haproxy.yml)
* Краткое описание шагов:   
![result](https://github.com/Rain-m-a-n/test/blob/master/picsplay.jpg)  
* Результат выполенния <u>playbook:</u>
![result](https://github.com/Rain-m-a-n/test/blob/master/picsplay_res.jpg)  
* Проверка работоспособности:
  * Открываем адрес заданный в настройках keepalived:
  ![result](https://github.com/Rain-m-a-n/test/blob/master/pics1.jpg)  
  * Обновляем страницу:
  ![result](https://github.com/Rain-m-a-n/test/blob/master/pics2.jpg)
  * Также открываем страницу статистики:
  ![result](https://github.com/Rain-m-a-n/test/blob/master/pics3.jpg)  

* **Отказоустойчивость**:
  * Система продолжит работать, если отключится сервер **haproxy-02** (так как он выполняет роль дублирующего).
  * Система продолжит работать, если отключится один из web серверов. 
  * Система ${\color{red}перестанет}$ ${\color{red}работать}$, если отключится сервер **haproxy-01** т.к. он выполняет роль мастера. Этот момент можно исправить в конфигурационном файле **keepalived.conf**. Но к сожалению не хватило времени для донастройки. 
