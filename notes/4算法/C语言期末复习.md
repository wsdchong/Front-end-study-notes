# C语言期末复习

选择题（10）

## 第一章：C语言

1C语言本身没有输入输出语句，由库函数scanf完成；main函数位置随意；一行可以写多条语句；单行注释、多行注释

## 第二章：算法

1结构化程序的三种基本结构：顺序、分支、循环；goto可能破坏程序清晰结构，不提倡；算法的时间复杂度指算法早执行过程中的运算次数；空间复杂度是用的存储空间；

2设计程序是，先确定数据结构、然后确定算法，在编码上机调试，最后整理文档。（分析、设计、编码、测试、排错等）

## 第三章：顺序结构

1存储空间char<short<int<long<float<double；进制；字符常量由由单引号引的一个字符，转义字符’\’也是字符常量；实型参与运算就自动转换为double型。

2标识符只能由字母、数字、下划线三种字符组成，第一个字符不能是数字。

3计算顺序

4putchar（）是用于输出字符的库函数

## 第四章：分支结构

1if()的应用

## 第五章：循环结构

1for（）的应用

## 第六章：数组

1数组的下标只能是整数类型数据；[]中的必须是确定值，不能是变量；整数数组不能整体赋值。字符串默认的结束标准——字符‘\0’

2gets()函数的参数只能是一个字符串；

 

## 第七章：函数

1形参只能是变量，不能是常量或表达式，但实参可以；函数的返回类型由函数类型决定；

 

## 第八章：指针

1由于通过地址能够找到所需的变量单元，因此将地址比作指针；

 

## 第九章：结构体

1struct是结构体类型的关键字；结构体类型；结构体成员名

 

## 第十章：I/O

Fopen函数打开数据文件。返回值是指针

 

编程题（算法+数据结构）

 

### 判断是不是素数

算法：只能被一和自己整除的数。用双循环结构，一个循环用来输入数（从3开始）、一个用来除数（从2开始）。如果取余为零就break，如果最终只能自己除自己，就输出。

```
  for(n=3;n<20;n++)

  {

   for(i=2;i<n;i++)//注意双循环的循环

​       if(n%i==0)

​       break;

​       if(i==n){

​          printf("%4d",n);

​       }

  }

 
```

### 数字分离

算法：用取余分离个位数，用整除去掉个位数；

```
    scanf("%d",&i);

​    while(i!=0){

​       printf("%4d",i%10);

​       i=i/10;

​       k++;

​    }
```

 

### 排序

算法：用冒泡排序，将相邻两数比较，大数换后面。

```
    for(i=0;i<N;i++){

​     scanf("%d",&a[i]);}          //输入

​    for(i=0;i<N-1;i++){

​       for(j=0;j<N-i-1;j++){

​           if(a[j]>a[j+1]){

​           t=a[j];

​           a[j]=a[j+1];

​           a[j+1]=t;

​           }

​       }

​    }                   //排序

​    for(i=0;i<N;i++)

​    printf("%5d",a[i]);            //排序       
```

 

### 以特殊字符终止输入

算法：当输入字符等于特殊字符后break

```
    while(1){

​       c=getchar();

​       if(c=='#')

​       break;

​       i++;

​    }
```

 

### 删除指定字符

算法：产生一个新数组，如果原数组中不等于指定字符是字符放到新数组中

```
    gets(str1);                 //获得字符串

​    c=getchar();                //获得删除字符

​    while (str1[i]!='\0'){             //执行到终止

​       if(str1[i]!=c){

​           str2[j]=str1[i];

​           j++;

​       }

​       i++;

​    }

​    str2[j]='\0';                //用终止符终止
```

 

### 比较字符串大小

算法：逐个比较，知道字符不等或只有一个字符串；

```
    gets(s1);                //输入字符串

​    gets(s2);

​    while(s1[i]!='\0'&&s2[i]!='\0'){       //比对

​       if(s1[i]!=s2[i]) break;

​       else i++;

​    }

​    k=s1[i]-s2[i];

​    if(k>0) printf("s1>s2\n");          //比较

​    else if(k<0) printf("s1<s2\n");

​    else printf("s1=s2\n");

 

 
```

### 指针应用

算法：用函数count计算最高成绩、最低成绩和平均成绩；并用参数返回。

```
int main(){

​    int i,N;

​    int score[30],max,min;

​    float ave;

​    void count (int a[],int n,int *pmax,int *pmin,float *ave);

​    scanf("%d",&N);

​    for(i=0;i<N;i++) scanf("%d",&score[i]);

​    max=min=score[0];

​    count(score,N,&max,&min,&ave);

​    printf("%d %d %5.2f\n",max,min,ave);

​    return 0;

}

 

void count(int a[],int n,int *pmax,int *pmin,float *pave){

​    float sum=0;

​    int i;

​    for(i=0;i<n;i++){

​       if(a[i]>*pmax) *pmax=a[i];

​       if(a[i]<*pmin) *pmin=a[i];

​       sum=sum+a[i];

​    }

​    *pave=sum/n;

}
```

 

### 结构体应用

算法：用结构数组存储书的信息。书名（字符串）、出版社（字符串）、数量（整数）、单价（浮点数）。读入书的信息并按单价由少到多的顺序输出各书信息，然后输出书的总价。

```
struct booktype{

​    char name[30];

​    char concern[15];

​    int num;

​    float price;

};

 

void sortbk(struct booktype *,int);           //排序

float totalprice(struct booktype *,int);         //计算总价格

 

int main(){

​    struct booktype book[50];

​    int i,n;

​    float tprice;

​    scanf("%d",&n);

​    for(i=0;i<n;i++)

​     scanf("%s %s %d %f",&book[i].name,&book[i].concern,&book[i].num,&book[i].price);

​    sortbk(book,n);

  for(i=0;i<n;i++) 

  {

​    printf("%-30s%-20s%-10d%-.2f\n",book[i].name,book[i].concern,book[i].num,book[i].price);

  }

 

​    tprice=totalprice(book,n);

​    printf("%.2f\n",tprice);

​    return(0); 

}

void sortbk(struct booktype *bk,int n){

​    struct booktype bktmp;

​    int i,j,k;

​    for(i=0;i<n-1;i++){

​       k=1;

​       for(j=i+1;j<n;j++){

​           if(bk[j].price<bk[k].price) k=j; 

​       }

​       if(k!=i){

​           bktmp=bk[i];

​           bk[i]=bk[k];

​           bk[k]=bktmp;

​       }

​    }

}

float totalprice(struct booktype *bk,int n){

​    int i;

​    float total=0;

​    for(i=0;i<n;i++){

​       total+=bk[i].num*bk[i].price;

​    }

​    return(total);

}
```

 

### 求最大值和最小值

算法：比较大小，将大的值赋值到max，小的值赋值到min;

```
    scanf("%d",&n);       //设置数值

​    for(i=0;i<n;i++){

​       scanf("%d",&a[i]);

​       max=a[0];        //提前设置好最大值和最小值

​       min=a[0];

​    }

​    for(i=1;i<n;i++){

​       if(a[i]>max) max=a[i];

​       if(a[i]<min) min=a[i];

​    }

 
```

### 求累加和

算法：初始化f1和f2；f1=f2;f2=f2+f1;累加f2/f1；

```
    for(i=1;i<21;i++){

​       c=a+b;

​       a=b;

​       b=c;

​       sum=sum+b/a;

​    }

 
```

