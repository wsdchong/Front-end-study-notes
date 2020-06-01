## 一、实验目的

掌握图形用户界面的设计与实现。

## 二、实验内容

使用图形界面制作一个计算器并实现相应功能。

## 三、实验步骤

![img](https://img-blog.csdnimg.cn/20200505212440113.png)![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

```java
public class firstapp extends Applet implements ActionListener {

    private String[] LEFTKEYS = { "7", "8", "9", "4", "5", "6", "1", "2", "3", "0", "+/-", "." };

    private String[] RIGHTKEYS = { "/", "sqrt", "ln", "*", "sin", "<-", "-", "cos", "CE", "+", "y^x", "=" };

    private Button leftKeys[] = new Button[LEFTKEYS.length];

    private Button rightKeys[] = new Button[RIGHTKEYS.length];

    private TextField resultText = new TextField("0");



    private double resultNum = 0.0;

    private String operator = "=";

    private boolean startInput = true;



    public firstapp() {

        init();

    }

   

    public void init() {

        resultText.setEditable(false);

        resultText.setBackground(Color.WHITE);

        Panel leftPanel = new Panel();// 左边按钮

        leftPanel.setLayout(new GridLayout(4, 3, 3, 3));

        for (int i = 0; i < LEFTKEYS.length; i++) {

            leftKeys[i] = new Button(LEFTKEYS[i]);

            leftPanel.add(leftKeys[i]);

            leftKeys[i].setForeground(Color.RED);

        }

        Panel rightPanel = new Panel();

        rightPanel.setLayout(new GridLayout(4, 3, 3, 3));

        for (int i = 0; i < RIGHTKEYS.length; i++) {

            rightKeys[i] = new Button(RIGHTKEYS[i]);

            rightPanel.add(rightKeys[i]);

            rightKeys[i].setForeground(Color.blue);

        }

        this.setLayout(new BorderLayout());

        this.add(resultText, BorderLayout.NORTH);

        this.add(leftPanel, BorderLayout.WEST);

        this.add(rightPanel, BorderLayout.EAST);



        for (int i = 0; i < LEFTKEYS.length; i++) {

            leftKeys[i].addActionListener(this);

        }

        for (int i = 0; i < RIGHTKEYS.length; i++) {

            rightKeys[i].addActionListener(this);

        }

    }



    public void actionPerformed(ActionEvent e) {

        // TODO 自动生成的方法存根

        String label = e.getActionCommand();

        if (label.equals(RIGHTKEYS[8])) {

            // 处理CE

            resultText.setText("0");

            startInput = true;

        } else if (label.equals(RIGHTKEYS[5])) {

            // 处理退格

            handleBackSpace();

        } else if ("0123456789.".indexOf(label) >= 0) {

            // 处理数字n

            handleNum(label);

        } else {

            // 处理运算符

            handleOperate(label); 

        }

    }



    private void handleBackSpace() {

        String text = resultText.getText();

        int i = text.length();



        text = text.substring(0, i - 1);

        if (text.length() == 0) {

            // 如果文本没有了内容,显示0

            resultText.setText("0");

        } else {

            // 显示新的文本

            resultText.setText(text);

        }

    }



    private void handleNum(String key) {

        if (startInput) {

            if (key.equals(".")) {

                resultText.setText(resultText.getText() + ".");

            } else {

                resultText.setText(key);

            }

        } else if ((key.equals(".")) && (resultText.getText().indexOf(".") < 0)) {



            resultText.setText(resultText.getText() + ".");

        } else if (!key.equals(".")) {

            resultText.setText(resultText.getText() + key);

        }

        startInput = false;

    }



    private void handleOperate(String key) {

        if (key.equals(RIGHTKEYS[1]) || key.equals(RIGHTKEYS[2]) || key.equals(RIGHTKEYS[4]) || key.equals(RIGHTKEYS[7])

                || key.equals(LEFTKEYS[10])) {

            if (key.equals(RIGHTKEYS[1])) { // 处理sqrt

                if (getNumFromText() < 0.0) {

                   resultText.setText("小于0的数不能开方");

                } else {

                   resultNum = Math.sqrt(getNumFromText());

                }

            }



            if (key.equals(RIGHTKEYS[2])) { // 处理ln

                if (getNumFromText() <= 0.0) {

                   resultText.setText("小于等于0的数不能求对数");

                } else {

                   resultNum = Math.log(getNumFromText());

                }

            }

            if (key.equals(RIGHTKEYS[4])) { // 处理sin

                resultNum = Math.sin(getNumFromText());

            }



            if (key.equals(RIGHTKEYS[7])) { // 处理cos

                resultNum = Math.cos(getNumFromText());

            }

            if (key.equals(LEFTKEYS[10])) { // 处理+/-

                resultNum = getNumFromText() * (-1);

            }

            resultText.setText(String.valueOf(resultNum));

            startInput = true;

        }



        else {

            if (operator.equals("/")) {

                // 除

                if (resultText.getText().equals("0")) {

                   resultText.setText("除数不能为零");

                } else {

                   resultNum /= getNumFromText();

                }

            } else if (operator.equals("+")) {

                // 加

                resultNum += getNumFromText();

            } else if (operator.equals("-")) {

                // 减

                resultNum -= getNumFromText();

            } else if (operator.equals("*")) {

                // 乘

                resultNum *= getNumFromText();

            } else if (operator.equals("=")) {

                // 赋值

                resultNum = getNumFromText();

            } else if (operator.equals("y^x")) {

                // pow

                resultNum = Math.pow(resultNum, getNumFromText());

            }

            resultText.setText(String.valueOf(resultNum));

            operator = key;

            startInput = true;

        }

    }



    private double getNumFromText() {

        double textDouble;

        textDouble = Double.valueOf(resultText.getText()).doubleValue();

        return textDouble;

    }



    public static void main(String args[]) {

        firstapp firstapp1 = new firstapp();

        firstapp1.setVisible(true);

    }

}
```

![点击并拖拽以移动](data:image/gif;base64,R0lGODlhAQABAPABAP///wAAACH5BAEKAAAALAAAAAABAAEAAAICRAEAOw==)

## 四、实验总结

本次实验使我学会了如何实现图形用户界面，知道了awt各组件的相关参数、窗口的布局等相关知识。明白了接口的定义及其实现方法，了解了JAVA的事件及处理机制，学会了事件监听者类的使用。现在，我能够写出一些简单的图形用户界面程序了。