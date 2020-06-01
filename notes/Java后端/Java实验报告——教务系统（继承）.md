## 一、实验目的

使学生进一步了解Java面向对象中继承、封装、抽象、重载的运用。

## 二、实验内容

1、设计教师、学生、课程这三个教务系统中的对象类，包括这些对象的属性和方法。实现学生选课、删除课程、查看课程成绩、教师批准选课及录入成绩。

2、要求用到继承、封装、抽象、重载。

## 三、实验步骤

1抽象类Person的设计

```java
//Person.java

package wsdchong;

public abstract class Person {

   protected String name;

   protected String sex;

   protected int age;

   public final String getName() {

      return name;

   }

   abstract String getInfo();

}
```

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

2学生类的设计：继承自Person类，用两个<课程类>的动态数组保存选课列表和已经选上的课程列表，实现选课、删除选课、查看成绩、查看个人信息等方法。

```java
//Student.java

package wsdchong;



import java.util.ArrayList;



public class Student extends Person {

  

   private String stuno;

   private int grade;

  

   private ArrayList<Course> myCourses = new ArrayList<Course>();  //我的课程

   private ArrayList<Course> mySelectCourses = new ArrayList<Course>();  //我的选课

  

  

   Student(String name, String sex, int age, String stuno, int grade) {

      super();

      this.name = name;

      this.sex = sex;

      this.age = age;

      this.stuno = stuno;

      this.grade = grade;

   }

  

   public void selectCourse(Course c) {     //选课

      if(!myCourses.contains(c) && !mySelectCourses.contains(c))

          mySelectCourses.add(c);

   } 

   public void delateSelectCourse(Course c){    //删除选课

      mySelectCourses.remove(c);

      if (ifApprove(c)) // 如果已中签

      {

          myCourses.remove(c);

          c.removeStudent(this);

          c.getTeacher().removeStudent(this);

      }

   }

   public void addCourse(Course c){   //选课成功，将课程加入我的课程

      myCourses.add(c);

   }

  

   public String getScore(Course c)      //获取学生课程的成绩

   {

      if (myCourses.contains(c))

      { 

          return name+"的"+c.getName()+"成绩为: "+c.searchScore(this);

      }

      else

          return "你的课程列表里没有这门课";

   }

  

   public Boolean ifSelect(Course c) {      //判断学生是否选择某课程

      return mySelectCourses.contains(c);

   }

  

   public Boolean ifApprove(Course c) {     //判断学生是否选择某课程

      return myCourses.contains(c);

   }

  

  

   public String getCourse()    //获取课程列表

   {

      String s = "课程：";

      for(Course c:myCourses)

      {

          s += c.getName() + " ";

      }

      return s;

   }

   public String getScoreList()    //获取成绩单

   {

      String s = "学生 "+ getName() + " 的成绩单如下：\n";

      for(Course c:myCourses)

      {

          s = s+ c.getName() + "   " + c.searchScore(this) + "\n";

      }

      return s;

   }

  

   public String getInfo(){

      return "姓名："+name+"\n性别："+sex+"\n年龄："+age+"\n学号："+stuno+"\n年级："+grade+"\n"+getCourse();

   }    

}
```

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

3、教师类的设计：继承自Person类，用<课程类>的动态数组表示教师所教课程列表，用<学生类>的动态数组表示自己的学生名单，实现设置教师所教课程、同意学生选课、为学生设置成绩等方法。

```java
//Teacher.java

package wsdchong;



import java.util.ArrayList;



public class Teacher extends Person{

  

   private String tno;

   private ArrayList<Course> myCourse = new ArrayList<Course>();   //所授课程列表

   private ArrayList<Student> myStudents = new ArrayList<Student>(); //学生名单

  

   Teacher(String name,String sex, int age, String tno) {

      super();

      this.name = name;

      this.sex = sex;

      this.age = age;

      this.tno = tno;

   }



   void setCourse(Course c) //为老师设置所教课程

   {

      myCourse.add(c) ;

   }



   public void approveSelectCoures (Student s,Course c) {

     

      if (s.ifSelect(c) && myCourse.contains(c))   //如果学生s申请了这门课 且老师教这门课

      {

          s.addCourse(c);    //同意选课，将课程加入到学生的课程表中

          c.addStudent(s);      //将课程加入到课程的学生名单中

          if(!myStudents.contains(s))

             myStudents.add(s);

      }

     

   }

   public boolean removeStudent(Student s)  //移除一名学生

   {

      for(Course c:myCourse)

      {

          if (c.ifContainStudent(s))

          {

             return false;

          }

      }

      myStudents.remove(s);

      return true;

   }

   public void setScore(Student s, float score,Course c) //为一名学生设置成绩

   { 

     

      if(s.ifApprove(c) && myCourse.contains(c))

          c.setScores(s, score);

      else

          System.out.println("学生"+s.getName()+"的课表中没有"+c.getName());

   }

  

   public String getInfo()

   {

      String s =  "姓名："+name+"\n工号："+tno+"\n所授课程：";

      for(Course c : myCourse)     //遍历老师所教课程

      {

          s += c.getName();

          s +=" ";

      }

      return s;

   }

  

   public String getStudentList(Course c)   //获取课程名单

   {

      if(!myCourse.contains(c))

      {

          return "教师"+getName()+"并不教"+c.getName()+"这门课。\n";

      }

     

      String s = "教师"+getName()+"所教的"+c.getName()+"课程学生名单：\n";

     

      for(Student stu: myStudents)

      {

          if (stu.ifApprove(c))

          {

             s = s + stu.getName() +"\n";

          }

      }

      return s;

   }

}
```

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

4设计课程类，用<学生类>的动态数组表示该课程学生名单，用一个<学生类、浮点型>的hashmap来保存课程每名学生的成绩单。实现向课程名单中添加学生、向成绩单中添加一名学生的成绩的接口，实现获取课程成绩表的方法。

```java
//Course.java

package wsdchong;



import java.util.HashMap;

import java.util.ArrayList;



public class Course {

   private String name;

   private String cno;

   private Teacher itsTeacher ;

  

   private ArrayList<Student> studentList = new ArrayList<Student>();    //课程学生名单

   private HashMap<Student, Float> scoreList = new HashMap<Student, Float>();      //课程成绩单

  

  

   Course(String name, String cno) {

      super();

      this.name = name;

      this.cno = cno;

   }

   public String getName()   {return name;}

   public Teacher getTeacher()   {return itsTeacher;}

   public void setTeacher (Teacher t) { //为这门课设置一名教师

      this.itsTeacher = t;

      t.setCourse(this);

   }

   public void addStudent (Student s) {   //课程名单里添加一名学生

      studentList.add(s);

   }

  

   public void setScores (Student s , float score) {  //给学生s设置成绩 

      scoreList.put(s, score);

   } 

   public float searchScore (Student s) { //返回学生s的成绩



      return scoreList.get(s);

   }    

   public void removeStudent(Student s)  //移除学生

   {

      if (s.ifApprove(this))

          studentList.remove(s);

   }

   public boolean ifContainStudent(Student s)

   {

      return studentList.contains(s);

   }

   public String getInfo()     

   {

      return "课程名称:"+name+"课程编号："+cno+"授课教师："+itsTeacher;

   }

  

   public String getStudentList()     //获取学生列表

   {

      String s = "" ;

      for(Student stu : studentList)

      {

          s += stu.getName()+" ";

      }

      return s;

   }

  

   public String getScoreList()    //课程成绩表

   {

      String s = "课程"+this.getName()+"的成绩表\n";

      for(Student stu:scoreList.keySet())

      {

          s += stu.getName()+"  "+scoreList.get(stu)+"\n";

      }

      return s;

   }

}
```

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)



5进行测试，经测试，各功能均可以正常实现。



## 五、实验总结

1、本次实验使我进一步了解了Java中继承、封装、抽象、重载的运用。