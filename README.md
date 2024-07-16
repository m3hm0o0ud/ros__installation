### 1. إعداد هيكلية الحزمة وملفات الإطلاق

#### 1.1 التحقق من هيكلية الحزمة
تأكد من أن الحزمة `my_turtle` موجودة وتحتوي على الملفات والمجلدات التالية:
```sh
~/catkin_ws/src/my_turtle/
├── CMakeLists.txt
├── include
├── launch
│   └── turtlesim.launch
├── package.xml
├── scripts
│   └── move_turtle.py
└── src
```

#### 1.2 محتويات `turtlesim.launch`
تأكد من أن ملف `turtlesim.launch` يحتوي على التالي:
```xml
<launch>
  <node name="turtlesim" pkg="turtlesim" type="turtlesim_node" output="screen"/>
  <node name="teleop" pkg="turtlesim" type="turtle_teleop_key" output="screen"/>
</launch>
```

#### 1.3 محتويات `move_turtle.py`
تأكد من أن ملف `move_turtle.py` يحتوي على الكود التالي:
```python
#!/usr/bin/env python

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

#### 1.4 الأذونات لملف `move_turtle.py`
تأكد من أن الملف يحتوي على الأذونات الصحيحة للتنفيذ:
```sh
chmod +x ~/catkin_ws/src/my_turtle/scripts/move_turtle.py
```

### 2. بناء بيئة العمل

1. **الانتقال إلى مجلد العمل**:
   ```sh
   cd ~/catkin_ws
   ```

2. **تنظيف بيئة العمل**:
   ```sh
   catkin_make clean
   ```

3. **بناء بيئة العمل**:
   ```sh
   catkin_make
   ```

4. **مصدر بيئة العمل**:
   ```sh
   source devel/setup.bash
   ```

### 3. تشغيل ملف الإطلاق

حاول تشغيل ملف الإطلاق:
```sh
roslaunch my_turtle turtlesim.launch
```

### 4. تشغيل البرنامج لتحريك السلحفاة

حاول تشغيل البرنامج:
```sh
rosrun my_turtle move_turtle.py
```

### إذا استمرت المشكلة

إذا واجهت أي مشاكل، تحقق من رسائل الخطأ في الطرفية. إذا لم يتم حل المشكلة، يرجى مشاركة تفاصيل إضافية حول رسالة الخطأ حتى أتمكن من تقديم المزيد من المساعدة.

إذا كل شيء صحيح، يجب أن تعمل السلحفاة الآن وتتحرك تلقائيًا بناءً على البرنامج الذي كتبناه في `move_turtle.py`. إذا كانت لديك أي استفسارات إضافية، فلا تتردد في طرحها.



لنفترض أنك قد أكملت جميع الخطوات بشكل صحيح وأن الهيكلية الموجودة لديك صحيحة، دعنا نتأكد من تشغيل البرنامج بشكل صحيح من داخل المجلد `scripts`. يجب التأكد من أن جميع الأوامر تُنفذ من بيئة العمل المناسبة بعد بناء الحزمة.

### 1. إعداد بيئة العمل

أولاً، تأكد من أنك قمت بإنشاء جميع الملفات بشكل صحيح وأعطيتها الأذونات اللازمة.

### 2. بناء بيئة العمل

تأكد من أنك قمت بتنظيف وبناء بيئة العمل:
```sh
cd ~/catkin_ws
catkin_make clean
catkin_make
source devel/setup.bash
```

### 3. تشغيل ملف الإطلاق

حاول تشغيل ملف الإطلاق لتشغيل `turtlesim`:
```sh
roslaunch my_turtle turtlesim.launch
```

### 4. تشغيل البرنامج لتحريك السلحفاة

الآن، تأكد من أنك داخل مجلد `scripts` ثم قم بتشغيل البرنامج:
```sh
cd ~/catkin_ws/src/my_turtle/scripts
rosrun my_turtle move_turtle.py
```

### ملاحظة مهمة

إذا كنت تواجه مشاكل في التعرف على الحزمة، قد تحتاج إلى التأكد من أن ROS يعرف عن الحزمة الخاصة بك عن طريق تحديث المتغيرات البيئية واستخدام الأوامر الصحيحة.

### التأكد من إعدادات البيئة

تأكد من أنك قد قمت بمصدر بيئة العمل بشكل صحيح:
```sh
source /opt/ros/noetic/setup.bash
source ~/catkin_ws/devel/setup.bash
```

إذا كنت لا تزال تواجه مشكلة في تشغيل البرنامج، تأكد من عدم وجود أي أخطاء في التسمية أو في مسارات الملفات.

### إذا استمرت المشكلة

إذا لم يتم حل المشكلة بعد تنفيذ هذه الخطوات، شارك تفاصيل إضافية حول رسالة الخطأ حتى أتمكن من تقديم المزيد من المساعدة.
