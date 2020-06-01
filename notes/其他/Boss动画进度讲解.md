# Boss动画进度讲解

已执行工作包括两个部分：设置动画，设置脚本

## 一、设置动画

主要是两部分工作：

一是给动画片段进行了简单的状态设置

1连线

2设置bool参数

3添加参数

![img](file:///C:/Users/ADMINI~1/AppData/Local/Temp/msohtmlclip1/01/clip_image002.png)

 



二是把只执行一次的动画的loop time关闭。使其不能循环播放

![img](file:///C:/Users/ADMINI~1/AppData/Local/Temp/msohtmlclip1/01/clip_image004.png)

 



## 二、添加脚本

using System.Collections;

using System.Collections.Generic;

using UnityEngine;

//按照执行次数分类：持续动作：站立idle、跑步run、眩晕stun

//         执行一次动作：技能1，2，3；受击hit；进入in；死亡dead。

//实现60S的boss动画；首先通过进入状态进入站立状态；

//          然后每5s按顺序释放技能1，2，3；技能空挡期，boss左右跑动来躲避攻击；

//交互部分：在60S中，每次受到攻击，打断boss当前动作，进入一次受击状态，然后重新攻击；

//     攻击三次后进入眩晕状态，然后重新攻击。

//     当boss血量消失，直接进入死亡状态，游戏结束

//实现思路：用循环语句循环15S的动作，if时间为0执行技能一，然后回正常状态，然后跑；技能2，3同理

//     if受到攻击进入受击状态，然后后置时间5s；眩晕同理

//遇到的问题：执行一次的攻击，进入状态后不能结束后退出状态，还需再次执行，才能退出

public class flash : MonoBehaviour

{

  public Animator ani;

  // Use this for initialization

  void Start()

  {

​    //ani.GetComponent<Animator>();

  }

 

  // Update is called once per frame

  void Update()

  {

​    if (Input.GetKey(KeyCode.A))

​    {

​      ani.SetBool("Skill1", true);

​    }

​    if (Input.GetKey(KeyCode.B))

​    {

​      ani.SetBool("Skill1", false);

​    }

​    if (Input.GetKey(KeyCode.Q))

​    {

​      ani.SetBool("Hit", true);

​    }

  }

}

 

 