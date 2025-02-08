# LAB1_Установка Docker на Oracle Linux
1. Начал с установки пакета <b>wget</b>, используя команду ```sudo yum install wget```, данный пакет даёт возможность загружать файлы из интернета
   
   ![image](https://github.com/user-attachments/assets/81ffa714-132f-4ade-89b9-d72be8018ce7)
   
3. Следом установил пакет <b>curl</b> ```sudo yum install curl```,данный пакет даёт возможность отправлять HTTP/HTTPS запросы
   
   ![image](https://github.com/user-attachments/assets/d89019b2-3053-4320-b829-f730576085a5)
   
4. Копирую репозиторий докера, для того чтобы его потом установить, используя <b>wget</b> используя тег <b>-P</b> для чтения <br>```sudo wget -P /etc/yum.repos.d/ https://download.docker.com/linux/centos/docker-ce.repo```

   ![image](https://github.com/user-attachments/assets/34eb77ad-9b3d-42e6-93e8-d96f9e72dce9) 
   
6. C помощью пакета <b>yum</b> устанавливаем докер из копированного репозитория выше <br>```sudo yum install docker-ce docker-ce-cli containerd.io```
   
   ![image](https://github.com/user-attachments/assets/245c96d4-816b-479b-bad7-d0914e037cc0)
   ![image](https://github.com/user-attachments/assets/7ec33469-db1f-4f1f-87f7-0c336141fca6)

   
8. Запускаем докер используя команду ```sudo systemctl enable docker --now``` эта команда добавляет doker в список служб, которые запустятся при запуске ОС
   
   ![image](https://github.com/user-attachments/assets/a416064c-9e96-41c6-a73f-e7820770ad1b) 


