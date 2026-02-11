# Netology_K8S_2.1 (Моисеенко А.Н.)
## Задание 1: Volume: обмен данными между контейнерами в поде
### Задача
Создать Deployment приложения, состоящего из двух контейнеров, обменивающихся данными.

### Шаги выполнения
- Создать Deployment приложения, состоящего из контейнеров busybox и multitool.
- Настроить busybox на запись данных каждые 5 секунд в некий файл в общей директории.
- Обеспечить возможность чтения файла контейнером multitool.
### Скриншоты:
- описание пода с контейнерами (kubectl describe pods data-exchange)
<img width="854" height="857" alt="image" src="https://github.com/user-attachments/assets/c77bfc78-bec6-41c3-9001-d744f71866e4" />
<img width="1191" height="707" alt="image" src="https://github.com/user-attachments/assets/c91683c1-cf3e-4086-b351-05ec01d739b8" />

- вывод команды чтения файла (tail -f <имя общего файла>)
<img width="809" height="288" alt="image" src="https://github.com/user-attachments/assets/5af610d2-f810-41eb-81f7-dadc5aa65d85" />

### Манифесты:
- [containers-data-exchange.yaml](https://github.com/joyspride812/Netology_K8S_2.1/blob/main/containers-data-exchange.yaml)
## Задание 2. PV, PVC
### Задача
- Создать Deployment приложения, использующего локальный PV, созданный вручную.

### Шаги выполнения
- Создать Deployment приложения, состоящего из контейнеров busybox и multitool, использующего созданный ранее PVC
- Создать PV и PVC для подключения папки на локальной ноде, которая будет использована в поде.
<img width="652" height="330" alt="image" src="https://github.com/user-attachments/assets/ed072cf0-2696-4cb8-92ce-ed2026937a92" />
<img width="606" height="239" alt="image" src="https://github.com/user-attachments/assets/3e8933fc-9c78-425a-b8d7-6976ab3e09e0" />


- Продемонстрировать, что контейнер multitool может читать данные из файла в смонтированной директории, в который busybox записывает данные каждые час.
<img width="856" height="70" alt="image" src="https://github.com/user-attachments/assets/499c97d3-d085-4c9b-9da9-e7019b189026" />

- Удалить Deployment и PVC. Продемонстрировать, что после этого произошло с PV. Пояснить, почему. (Используйте команду kubectl describe pv).
<img width="724" height="395" alt="image" src="https://github.com/user-attachments/assets/7e7750ed-310d-4f7e-968f-2b74a407a3c5" />

Статус PV изменился на Released. Данные не удалились, так как Reclaim Policy имеет значение Retain.
- Продемонстрировать, что файл сохранился на локальном диске ноды. Удалить PV. Продемонстрировать, что произошло с файлом после удаления PV. Пояснить, почему.
<img width="558" height="134" alt="image" src="https://github.com/user-attachments/assets/d1341965-ad53-44e6-9d33-556700e42c57" />

Удаление PV в Kubernetes — это только удаление объекта из состояния кластера. Локальное хранилище не управляется Kubernetes, поэтому файловая система на ноде не затрагивается.
### Манифесты:
- [pv-pvc.yml](https://github.com/joyspride812/Netology_K8S_2.1/blob/main/pv-pvc.yml)

## Задание 3: StorageClass
### Задача: Создать Deployment приложения, использующего PVC, созданный на основе StorageClass.
### Шаги выполнения
- Создать Deployment приложения, состоящего из контейнеров busybox и multitool, использующего созданный ранее PVC.
- Создать SC и PVC для подключения папки на локальной ноде, которая будет использована в поде.  
Так StorageClass в данном задании использует provisioner: kubernetes.io/no-provisioner динамически PV создаваться не будет и перед созданием SC необходимо создаьт PV.

 
 <img width="591" height="42" alt="image" src="https://github.com/user-attachments/assets/9d918b41-a855-47e6-8ec9-66299b527669" />  

Создание SC, PVC и Deployments.  

<img width="579" height="67" alt="image" src="https://github.com/user-attachments/assets/d62acee8-29c0-48bd-b2b2-c775224c1c40" />  
  
- Продемонстрировать, что контейнер multitool может читать данные из файла в смонтированной директории, в который busybox записывает данные каждые 5 секунд.  

   
 <img width="817" height="210" alt="image" src="https://github.com/user-attachments/assets/4ae10823-b969-4d8f-8872-8d651e18a3f8" />
### Манифесты:
- [sc.yaml](https://github.com/joyspride812/Netology_K8S_2.1/blob/main/sc.yaml)
- [pv.yaml](https://github.com/joyspride812/Netology_K8S_2.1/blob/main/pv.yaml)
 



