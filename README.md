# ros__installation

## Installing ROS Noetic
### المتطلبات الأساسية
قبل بدء عملية التثبيت، تأكد من تحديث نظام التشغيل الخاص بك وتثبيت الحزم الضرورية.

### الخطوات
1. إضافة المصادر والمفاتيح:
    قم بإضافة مفاتيح التحقق والمصادر اللازمة لتثبيت ROS Noetic.
   
bash
    sudo apt update
    sudo apt install curl
    curl -s https://raw.githubusercontent.com/ros/rosdistro/master/ros.asc | sudo apt-key add -
    sudo sh -c 'echo "deb http://packages.ros.org/ros/ubuntu $(lsb_release -sc) main" > /etc/apt/sources.list.d/ros-latest.list'
    sudo apt update
    sudo apt install ros-noetic-desktop-full
    

2. إعداد البيئة:
    قم بإضافة إعدادات البيئة لـ ROS Noetic إلى ملف ~/.bashrc لتحميلها تلقائيًا عند بدء جلسة جديدة.
   
bash
    echo "source /opt/ros/noetic/setup.bash" >> ~/.bashrc
    source ~/.bashrc
    

## Installing ROS2 Foxy
### المتطلبات الأساسية
تأكد من تحديث نظام التشغيل الخاص بك وتثبيت الحزم الضرورية.

### الخطوات
1. إضافة المصادر والمفاتيح:
    قم بإضافة مفاتيح التحقق والمصادر اللازمة لتثبيت ROS2 Foxy.
   
bash
    sudo apt update
    sudo apt install curl gnupg2 lsb-release
    curl -sSL https://raw.githubusercontent.com/ros/rosdistro/master/ros.asc | sudo apt-key add -
    sudo sh -c 'echo "deb http://packages.ros.org/ros2/ubuntu $(lsb_release -cs) main" > /etc/apt/sources.list.d/ros2-latest.list'
    sudo apt update
    sudo apt install ros-foxy-desktop
    

2. إعداد البيئة:
    قم بإضافة إعدادات البيئة لـ ROS2 Foxy إلى ملف ~/.bashrc لتحميلها تلقائيًا عند بدء جلسة جديدة.
   
bash
    echo "source /opt/ros/foxy/setup.bash" >> ~/.bashrc
    source ~/.bashrc
    

باتباع هذه الخطوات، يمكنك إعداد بيئة عملك لتطوير وتشغيل تطبيقات ROS. إذا واجهت أي مشاكل أو كانت لديك أسئلة، يرجى الرجوع إلى الوثائق الرسمية لـ [ROS Noetic](http://wiki.ros.org/noetic) و [ROS2 Foxy](https://docs.ros.org/en/foxy/index.html).
