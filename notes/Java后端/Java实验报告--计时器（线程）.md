## 一、实验目的

了解Java线程的使用方法

## 二、实验内容

1、使用多线程制作一计时器，要求实现文本框输入一个时间（分），计时结束后提示。

2、系统通过点击按钮可实现启动计时、暂停、结束计时、复位等功能。

## 三、实验步骤

借助windowBulider制作窗体界面，使用两个Date获取系统时间，通过两次时间相减来计算计时器经过了多长时间。

```java
package test;



import java.awt.BorderLayout;

import java.awt.Button;

import java.awt.Font;

import java.awt.Frame;

import java.awt.Label;

import java.awt.TextField;

import java.awt.event.ActionEvent;

import java.awt.event.ActionListener;

import java.awt.event.WindowAdapter;

import java.awt.event.WindowEvent;

import java.util.Date;



public class thirdapp extends Frame {

    private TextField tf = new TextField(30);

    private TextField m = new TextField(2);

    private TextField s = new TextField(2);

    private TextField ms = new TextField(2);

    private boolean start = false;

    private boolean pause = false;

    private int mSecond = 0;

    private int second = 0;

    private int min = 0;   

    private int time ;

    private float diff = 0;        //时间差

    private float part = 0;        //如要暂停时使用

    private Date d1;

    private Date d2;

    private Button bt_start = new Button("\u5F00\u59CB");

    MyThread mt = new MyThread();

   

    thirdapp(){

        super("计时器");

        setSize(300, 240);

        setVisible(true);

        setLayout(null);

       

        m.setFont(new Font("Dialog", Font.PLAIN, 35));

        m.setBounds(40, 50, 50, 35);

        m.setEditable(false);

        add(m);

       

        Label label = new Label(":");

        label.setAlignment(Label.CENTER);

        label.setFont(new Font("Dialog", Font.PLAIN, 35));

        label.setBounds(90, 50, 25, 35);

        add(label);

       

        s.setFont(new Font("Dialog", Font.PLAIN, 35));

        s.setBounds(115, 50, 50, 35);

        s.setEditable(false);

        add(s);

       

        Label label_1 = new Label(":");

        label_1.setAlignment(Label.CENTER);

        label_1.setFont(new Font("Dialog", Font.PLAIN, 35));

        label_1.setBounds(165, 50, 25, 35);

        add(label_1);

       

       

        ms.setFont(new Font("Dialog", Font.PLAIN, 35));

        ms.setBounds(190, 50, 50, 35);

        ms.setEditable(false);

        add(ms);

       



        bt_start.setBounds(187, 120, 65, 35);

        add(bt_start);

        bt_start.addActionListener(ActionStart);

       

        tf.setFont(new Font("Dialog", Font.PLAIN, 34));

        tf.setBounds(115, 120, 65, 35);

        add(tf);

       

        Label label_2 = new Label("\u8BF7\u8F93\u5165\u65F6\u957F");

        label_2.setBounds(30, 125, 77, 25);

        add(label_2);

       

        Button bt_pause = new Button("\u6682\u505C");

        bt_pause.setBounds(15, 180, 60, 35);

        add(bt_pause);

        bt_pause.addActionListener(ActionPause);

       

        Button bt_reset = new Button("\u590D\u4F4D");

        bt_reset.setBounds(147, 180, 60, 35);

        add(bt_reset);

        bt_reset.addActionListener(ActionReset);

       

        Button bt_stop = new Button("\u7ED3\u675F");

        bt_stop.setBounds(212, 180, 60, 35);

        add(bt_stop);

        bt_stop.addActionListener(ActionStop);

       

        Button bt_continue = new Button("\u7EE7\u7EED");

        bt_continue.setBounds(81, 180, 60, 35);

        add(bt_continue);

        bt_continue.addActionListener(ActionContinue);

       

        addWindowListener(winclose);

        mt.start();

       

    }

   

    WindowAdapter winclose = new WindowAdapter() {

        public void windowClosing(WindowEvent e) {

            System.exit(0);

        }

    };

   

    ActionListener ActionStart = new ActionListener() {

       

        @Override

        public void actionPerformed(ActionEvent e) {

            // TODO 自动生成的方法存根

            start = true;



            d1 = new Date();

            time = Integer.parseInt(tf.getText());

            tf.setEditable(false);

            bt_start.setEnabled(false);

           

        }

    };

    ActionListener ActionPause = new ActionListener() {

       

        @Override

        public void actionPerformed(ActionEvent e) {

            // TODO 自动生成的方法存根

            pause = true;             

            part = diff;

           

        }

    };

    ActionListener ActionContinue = new ActionListener() {

       

        @Override

        public void actionPerformed(ActionEvent e) {

            // TODO 自动生成的方法存根

            d1 = new Date();

           

            pause = false;            

           

        }

    };



    ActionListener ActionStop = new ActionListener() {

       

        @Override

        public void actionPerformed(ActionEvent e) {

            // TODO 自动生成的方法存根

            start = false;            

            bt_start.setEnabled(true);

        }

    };

   

    ActionListener ActionReset = new ActionListener() {

       

        @Override

        public void actionPerformed(ActionEvent e) {

            // TODO 自动生成的方法存根

            start = false;

            pause = false;

            tf.setText("");

            tf.setEditable(true);

            m.setText("");

            s.setText("");

            ms.setText("");

            min = 0;

            second = 0;

            mSecond = 0;

            diff = 0;

            part = 0;

            bt_start.setEnabled(true);        

        }

    };

   

    class MyThread extends Thread{   

        public void run() {

            while(true)

            {

                validate();

                if(start && !pause)

                {

                   d2 = new Date();

                   diff = d2.getTime() - d1.getTime() + part;

                   mSecond = (int)diff%1000/10;

                   second =(int) (diff/1000)%60;

                   min=(int)diff/1000/60;

                   m.setText(min+"");

                   s.setText(second+"");

                   ms.setText(mSecond+"");

                  

                   try{

                       Thread.sleep(5);

                   }

                   catch(Exception e){

                   }

                  

                   if((second+min*60)==time)

                   {

                       pause = true;

                       Frame fr = new Frame("时间到");

                      

                       fr.setSize(100,100);

                       Label finish = new Label("时间到");

                       fr.add(finish, BorderLayout.CENTER);

                       fr.addWindowListener(winclose);

                       fr.setVisible(true);

                   }  

                }

            }

        }

    }

   

    public static void main(String[] args) {

            thirdapp mt = new thirdapp(); 

    }

}
```

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

## 四、实验总结

本次实验使我了解了Java的多线程机制，学会了如何创建并运行一个线程，运用多线程，可以进行一些更复杂的项目了。