لإنشاء مشروع مشابه للمشروع الموجود في المستودع "Manipulate-with-turtlesim-package-in-ROS-noetic"، اتبع الخطوات التالية:

### 1. إعداد بيئة العمل
تأكد من تثبيت ROS Noetic على نظامك. يمكنك اتباع التعليمات في [وثائق ROS](http://wiki.ros.org/noetic/Installation).

### 2. إنشاء مساحة عمل كاتكن
أنشئ مساحة عمل جديدة باستخدام الأوامر التالية:
```sh
mkdir -p ~/catkin_ws/src
cd ~/catkin_ws/
catkin_make
source devel/setup.bash
```

### 3. إنشاء حزمة جديدة
أنشئ حزمة جديدة تسمى `my_turtle`:
```sh
cd ~/catkin_ws/src
catkin_create_pkg my_turtle std_msgs rospy roscpp turtlesim
```

### 4. إنشاء ملف إطلاق
أنشئ ملف `turtlesim.launch` في مجلد `launch` داخل الحزمة `my_turtle`:
```sh
mkdir -p ~/catkin_ws/src/my_turtle/launch
nano ~/catkin_ws/src/my_turtle/launch/turtlesim.launch
```

أضف المحتوى التالي إلى الملف:
```xml
<launch>
  <node name="turtlesim" pkg="turtlesim" type="turtlesim_node" output="screen"/>
  <node name="teleop" pkg="turtlesim" type="turtle_teleop_key" output="screen"/>
</launch>
```

### 5. بناء الحزمة
انتقل إلى مجلد العمل وبنِ الحزمة:
```sh
cd ~/catkin_ws
catkin_make
source devel/setup.bash
```

### 6. تشغيل ملف الإطلاق
شغل ملف الإطلاق لتشغيل TurtleSim:
```sh
roslaunch my_turtle turtlesim.launch
```

### 7. التحكم في السلحفاة
شغل برنامج التحكم في السلحفاة:
```sh
rosrun my_turtle move_turtle.py
```

بهذا تكون قد أنشأت مشروعًا مشابهًا للمشروع الموجود في المستودع المذكور.




بعد إنشاء المشروع وتشغيل ملف الإطلاق، يمكنك البدء في التحكم في السلحفاة وتنفيذ مهام إضافية مشابهة للمستودع الذي أشرت إليه. سأوضح لك كيفية إضافة بعض الميزات الأخرى.

### 8. إنشاء سكربت للتحكم في السلحفاة
يمكنك إنشاء سكربت Python لتحريك السلحفاة تلقائيًا.

#### 8.1 إنشاء ملف `move_turtle.py`
انتقل إلى مجلد `scripts` داخل الحزمة وأنشئ ملف `move_turtle.py`:
```sh
mkdir -p ~/catkin_ws/src/my_turtle/scripts
nano ~/catkin_ws/src/my_turtle/scripts/move_turtle.py
```

أضف المحتوى التالي إلى الملف:
```python
#!/usr/bin/env python3

import rospy
from geometry_msgs.msg import Twist

def move_turtle():
    rospy.init_node('move_turtle', anonymous=True)
    pub = rospy.Publisher('/turtle1/cmd_vel', Twist, queue_size=10)
    rate = rospy.Rate(10)  # 10hz
    
    move_cmd = Twist()
    move_cmd.linear.x = 2.0
    move_cmd.angular.z = 1.0

    while not rospy.is_shutdown():
        pub.publish(move_cmd)
        rate.sleep()

if __name__ == '__main__':
    try:
        move_turtle()
    except rospy.ROSInterruptException:
        pass
```

#### 8.2 تحديث أذونات الملف
تأكد من أن الملف يحتوي على الأذونات الصحيحة للتنفيذ:
```sh
chmod +x ~/catkin_ws/src/my_turtle/scripts/move_turtle.py
```

### 9. تشغيل السكربت
بعد تشغيل `roslaunch my_turtle turtlesim.launch`، افتح نافذة طرفية جديدة وشغل السكربت:
```sh
rosrun my_turtle move_turtle.py
```

### 10. استكشاف العقد والمواضيع باستخدام `rqt_graph`
يمكنك استخدام `rqt_graph` لعرض العقد والمواضيع:
```sh
rosrun rqt_graph rqt_graph
```

بهذه الخطوات، ستكون قد أنشأت مشروعًا متكاملًا يشابه المشروع الموجود في المستودع "Manipulate-with-turtlesim-package-in-ROS-noetic". يمكنك توسيع المشروع بإضافة ميزات جديدة واستكشاف المزيد من إمكانيات ROS وTurtleSim.
