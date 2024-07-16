لإنشاء مشروع باستخدام `turtlesim` في ROS، يمكنك اتباع الخطوات التالية:

### 1. إعداد بيئة العمل

1. **إنشاء مجلد العمل**:
   ```sh
   mkdir -p ~/catkin_ws/src
   cd ~/catkin_ws/
   ```

2. **بناء بيئة العمل**:
   ```sh
   catkin_make
   source devel/setup.bash
   ```

### 2. إنشاء حزمة جديدة

1. **الانتقال إلى مجلد `src`**:
   ```sh
   cd ~/catkin_ws/src
   ```

2. **إنشاء حزمة جديدة تسمى `my_turtle`**:
   ```sh
   catkin_create_pkg my_turtle std_msgs rospy roscpp turtlesim
   ```

3. **بناء الحزمة**:
   ```sh
   cd ~/catkin_ws
   catkin_make
   source devel/setup.bash
   ```

### 3. إنشاء ملف إطلاق (launch file)

1. **إنشاء مجلد `launch` داخل الحزمة**:
   ```sh
   mkdir -p ~/catkin_ws/src/my_turtle/launch
   ```

2. **إنشاء ملف `turtlesim.launch`**:
   ```sh
   touch ~/catkin_ws/src/my_turtle/launch/turtlesim.launch
   ```

3. **تحرير ملف `turtlesim.launch` وإضافة المحتوى التالي**:
   ```xml
   <launch>
     <node name="turtlesim" pkg="turtlesim" type="turtlesim_node" output="screen"/>
     <node name="teleop" pkg="turtlesim" type="turtle_teleop_key" output="screen"/>
   </launch>
   ```

### 4. تشغيل المشروع

1. **الانتقال إلى مجلد العمل**:
   ```sh
   cd ~/catkin_ws
   ```

2. **بناء المشروع مجددًا (إذا لم تقم بذلك بالفعل)**:
   ```sh
   catkin_make
   source devel/setup.bash
   ```

3. **تشغيل ملف الإطلاق**:
   ```sh
   roslaunch my_turtle turtlesim.launch
   ```

### 5. التحكم في السلحفاة باستخدام لوحة المفاتيح

- عند تشغيل ملف الإطلاق، سيتم فتح نافذة `turtlesim` ويمكنك التحكم في السلحفاة باستخدام لوحة المفاتيح في نافذة الطرفية.

### برنامج بسيط لتحريك السلحفاة

يمكنك أيضًا كتابة برنامج بسيط لتحريك السلحفاة تلقائيًا:

1. **إنشاء مجلد `scripts` داخل الحزمة**:
   ```sh
   mkdir -p ~/catkin_ws/src/my_turtle/scripts
   ```

2. **إنشاء ملف `move_turtle.py`**:
   ```sh
   touch ~/catkin_ws/src/my_turtle/scripts/move_turtle.py
   chmod +x ~/catkin_ws/src/my_turtle/scripts/move_turtle.py
   ```

3. **تحرير ملف `move_turtle.py` وإضافة المحتوى التالي**:
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

4. **تشغيل البرنامج**:

   افتح نافذة طرفية جديدة وشغل ملف الإطلاق:
   ```sh
   roslaunch my_turtle turtlesim.launch
   ```

   في نافذة طرفية أخرى، شغل البرنامج:
   ```sh
   rosrun my_turtle move_turtle.py
   ```

بهذا، ستكون قد أنشأت مشروع `turtlesim` واختبرت تحريك السلحفاة باستخدام كل من لوحة المفاتيح وبرنامج بسيط. إذا كانت لديك أي استفسارات إضافية، فلا تتردد في طرحها.
