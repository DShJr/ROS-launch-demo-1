# ROS-launch-demo-1
This repository contains the files for the first assignment, which involves setting up and running a simple ROS demo node.
Этот репозиторий содержит файлы для первого задания, которое включает в себя настройку и запуск простой демонстрационной ноды ROS.

Что было сделано, по шагам:

1) Создал отдельную папку под файлы: .sh и .launch.
Создал их, с добавлением кода.

1.1.
start-ros.sh
#!/bin/bash
# Этот скрипт будет запускать .launch файл: demo_publisher.launch
link="/home/name/directoty1/directory2/ros-launch-demo-1"
source /opt/ros/noetic/setup.bash
roslaunch "$link/demo_publisher.launch"

далее..
сохранив и закрыв файл .sh
присвоил право на исполнение этому файлу
chmod +x start-ros.sh

1.2.
demo_publisher.launch
<launch>
<node name="demo_publisher" pkg="rostopic" type="rostopic" args="pub -r 10 /demo_topic std_msgs/String 'data: Hello, ROS!" />
</launch>
Этот .launch файл: 
описывает, какой ROS-узел или программу нужно запустить.

name="demo_publisher"
это имя узла, который будет выводиться в списке узлов.

2)
Создал файл ros-demo_work-1.service , по адресу:
/etc/systemd/system/ ,
с добавлением в него следующего кода:

[Unit]
Description=ROS Demo Node
Service
After=network.target

[Service]
Type=simple
ExecStart=/bin/bash /home/name/directory1/directory2/ros-launch-demo-1/start-ros.sh

[Install]
WantedBy=multi-user.target

закрыв этот файл..

3)
Открыл другую консоль,
В этой консоли ввёл по очереди следующие команды:

3.1.
sudo systemctl daemon-reload
Сообщаю системе о новом сервисном файле.

3.2.
sudo systemctl enable ros-demo_work-1.service
Включаю автозапуск сервиса, при загрузке системы.

3.3.
sudo systemctl start ros-demo_work-1.service
Запускаю сервис, для проверки.

3.4.
systemctl status ros-demo_work-1.service
Проверяем статус сервиса.

В консоле появилось много разной информации, среди неё:
Loaded: loaded
Active: active (running)

3.5.
sudo reboot
Перезагружаю компьютер, чтобы убедиться, что всё работает.

3.6.
Компьютер заработал.
Открываю консоль.
Ввожу команду:
rosnode list

Появился список:
/demo_publisher/
/rosout

Всё работает :)
далее..

3.7.
Ввожу команду
rostopic echo /demo_topic

В итоге, запускается бесконечный список из:
data: Hello, ROS!

___
Скриншоты прилагаю.
