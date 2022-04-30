# 创建第一个Android Kotlin应用



## 一、创建第一个Kotlin应用程序



1.打开Android Studio，选择Projects>New Project，然后选择Basic Activity.



![image-20220430202941655](C:\Users\86130\Desktop\img\image-20220430202941655.png)



点击Next，选择**Kotlin**语言，然后点击Finish。



## 二、向页面添加更多的布局



### 1.添加按钮和约束，从Palette面板中拖动Button到



设置Button的Top>BottonOf textView，随后添加Button的左侧约束至屏幕的左侧，Button的底部约束至屏幕的底部。查看Attributes面板，修改将id从button修改为toast_button



### 2.调整Next按钮



Next按钮是工程创建时默认的按钮，查看Next按钮的布局设计视图。删除两者之间的链，可以在设计视图右键相应约束，选择Delete；



### 3.添加新的约束



添加Next的右边和底部约束至父类屏幕，Next的Top约束至TextView的底部。最后，TextView的底部约束至屏幕的底部。效果看起来如下图所示：



![image-20220430203550428](C:\Users\86130\Desktop\img\image-20220430203550428.png)



### 4.更改组件的文本



(1).在fragment_first.xml布局文件代码中，找到toast_button按钮的text属性部分



(2).在“text”处悬浮鼠标，点击 **Extract string resource**



(3).令资源名为toast_button_text，资源值为Toast，并点击OK



![image-20220430204859701](C:\Users\86130\Desktop\img\image-20220430204859701.png)



ps: 以上操作可以手动在string.xml文件中定义并引用

 

### 5.更新Next按钮



在属性面板中更改Next按钮的id，从button_first改为random_button。

![image-20220430205837779](C:\Users\86130\Desktop\img\image-20220430205837779.png)



在string.xml文件，右键**next**字符串资源，修改资源名称为**random_button_text**.



### 6.添加第三个按钮



向fragment_first.xml文件中添加第三个按钮，位于Toast和Random按钮之间，TextView的下方。新Button的左右约束分别约束至Toast和Random，Top约束至TextView的底部，Buttom约束至屏幕的底部，如图：



![image-20220430210216029](C:\Users\86130\Desktop\img\image-20220430210216029.png)



### 7.完善UI组件的属性设置



更改新增按钮id为count_button，显示字符串为Count，对应字符串资源值为count_button_text，更改TextView的文本为**0**。



修改后的fragment_first.xml代码：

`<?xml version="1.0" encoding="utf-8"?>`
`<androidx.constraintlayout.widget.ConstraintLayout xmlns:android="http://schemas.android.com/apk/res/android"`
    `xmlns:app="http://schemas.android.com/apk/res-auto"`
    `xmlns:tools="http://schemas.android.com/tools"`
    `android:layout_width="match_parent"`
    `android:layout_height="match_parent"`
    `tools:context=".FirstFragment">`

    <TextView
        android:id="@+id/textview_first"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:fontFamily="sans-serif-condensed"
        android:text="@string/hello_first_fragment"
        android:textColor="@android:color/darker_gray"
        android:textSize="30sp"
        android:textStyle="bold"
        app:layout_constraintBottom_toBottomOf="parent"
        app:layout_constraintEnd_toEndOf="parent"
        app:layout_constraintStart_toStartOf="parent"
        app:layout_constraintTop_toTopOf="parent" />
    
    <Button
        android:id="@+id/random_button"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:text="@string/random_button_text"
        app:layout_constraintBottom_toBottomOf="parent"
        app:layout_constraintEnd_toEndOf="parent"
        app:layout_constraintTop_toBottomOf="@+id/textview_first" />
    
    <Button
        android:id="@+id/toast_button"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:text="@string/toast_button_text"
        app:layout_constraintBottom_toBottomOf="parent"
        app:layout_constraintStart_toStartOf="parent"
        app:layout_constraintTop_toBottomOf="@+id/textview_first" />
    
    <Button
        android:id="@+id/count_button"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:text="@string/count_button_text"
        app:layout_constraintBottom_toBottomOf="parent"
        app:layout_constraintEnd_toStartOf="@+id/random_button"
        app:layout_constraintStart_toEndOf="@+id/toast_button"
        app:layout_constraintTop_toBottomOf="@+id/textview_first" />
`</androidx.constraintlayout.widget.ConstraintLayout>`



## 三、更新按钮和文本框的外观



### 1.添加新的颜色资源

values>colors.xml    添加新颜色screenBackground 值为 #2196F3，这是蓝色阴影色；添加新颜色buttonBackground 值为 #BBDEFB

`<color name="screenBackground">#2196F3</color>`
`<color name="buttonBackground">#BBDEFB</color>`



### 2.设置组件的外观

1. fragment_first.xml的属性面板中设置屏幕背景色为screenBackground

   

`android:background="@color/screenBackground"`



2. 设置每个按钮的背景色为buttonBackground



`android:background="@color/buttonBackground"`



### 3.设置组件的位置

1. Toast与屏幕的左边距设置为24dp，Random与屏幕的右边距设置为24dp

   

2. 设置TextView的垂直偏移为0.3

`app:layout_constraintVertical_bias="0.3"`



运行后：



![image-20220430213836409](C:\Users\86130\Desktop\img\image-20220430213836409.png)



## 四、添加代码完成应用程序交互



### 1.TOAST按钮添加一个toast消息



1. 打开FirstFragment.kt文件，有三个方法：onCreateView，onViewCreated和onDestroyView，在onViewCreated方法中使用绑定机制设置按钮的响应事件。



`binding.randomButton.setOnClickListener {
    findNavController().navigate(R.id.action_FirstFragment_to_SecondFragment)
}`

2. 接下来，为TOAST按钮添加事件，使用findViewById()查找按钮id，代码如下：

   

`// find the toast_button by its ID and set a click listener
view.findViewById<Button>(R.id.toast_button).setOnClickListener {
   // create a Toast with some text, to appear for a short time
   val myToast = Toast.makeText(context, "Hello Toast!", Toast.LENGTH_LONG)
   // show the Toast
   myToast.show()
}`



### 2.使Count按钮更新屏幕的数字

1. 在FirstFragment.kt文件，为count_buttion按钮添加事件：

`view.findViewById<Button>(R.id.count_button).setOnClickListener {
   countMe(view)
}`

2. countMe()为自定义方法，每次点击增加数字1，具体代码为：



`private fun countMe(view: View) {`
   `// Get the text view`
   `val showCountTextView = view.findViewById<TextView>(R.id.textview_first)`

   `// Get the value of the text view.`
   `val countString = showCountTextView.text.toString()`

   `// Convert value to a number and increment it`
   `var count = countString.toInt()`
   `count++`

   `// Display the new value in the text view.`
   `showCountTextView.text = count.toString()`
`}`



## 五、完成第二界面的代码



### 1.向界面添加TextView显示随机数



1. 打开fragment_second.xml的设计视图中，当前界面有两个组件，一个Button和一个TextView
2. 去掉TextView和Button之间的约束



![image-20220430215442881](C:\Users\86130\Desktop\img\image-20220430215442881.png)



3. 拖动新的TextView至屏幕的中间位置，用来显示随机数
4. 设置新的TextView的id为@+id/textview_random
5. 设置新的TextView的左右约束至屏幕的左右侧，Top约束至textview_second的Bottom，Bottom约束至Button的Top
6. 设置TextView的字体颜色textColor属性为@android:color/white，textSize为72sp，textStyle为bold
7. 设置TextView的显示文字为“R”
8. 设置垂直偏移量layout_constraintVertical_bias为0.45
   

### 2.更新显示界面文本的TextView

1. 在fragment_second.xml文件中，选择textview_second文本框，查看text属性，可见

   对应的strings.xml文本为Hello second fragment. Arg: %1$s

   

2. 更改该文本框id为textview_header

   

3. 设置layout_width为match_parent，layout_height为wrap_content。

   

4. 设置top，left和right的margin为24dp，左边距和右边距也就是start和end边距。



5. 向colors.xml添加颜色colorPrimaryDark，并将TextView颜色设置为@color/colorPrimaryDark，字体大小为24sp。



6. strings.xml文件中，修改hello_second_fragment的值为"Here is a random number between 0 and %d."

   

7. 使用Refactor>Rename将hello_second_fragment 重构为random_heading



### 3.更改界面的背景色和按钮布局



1. 向colors.xml文件添加第二个Fragment背景色的值，修改fragment_second.xml背景色的属性为**screenBackground2**

2. 将按钮移动至界面的底部



### 4.启用SafeArgs

1. Gradle的Project部分，在plugins节添加

`id 'androidx.navigation.safeargs.kotlin' version '2.5.0-alpha01' apply false`



2. module部分在plugins节添加

   `id 'androidx.navigation.safeargs'`



### 5.FirstFragment添加代码



1. 打开FirstFragment.kt源代码文件找到onViewCreated()方法，该方法在onCreateView方法之后被调用，可以实现组件的初始化。找到Random按钮的响应代码，注释掉原先的事件处理代码

2. 实例化TextView，获取TextView中文本并转换为整数值
   `val showCountTextView = view.findViewById<TextView>(R.id.textview_first)`
   `val currentCount = showCountTextView.text.toString().toInt()`

3. 将currentCount作为参数传递给`actionFirstFragmentToSecondFragment()`
   `val action = FirstFragmentDirections.actionFirstFragmentToSecondFragment(currentCount)`

4. 添加导航事件代码
   `findNavController().navigate(action)`

   

### 6.添加SecondFragment代码

1. onViewCreated()代码之前添加一行

`val args: SecondFragmentArgs by navArgs()`



2. onViewCreated()中添加：

`val count = args.myArg
val countText = getString(R.string.random_heading, count)
view.findViewById<TextView>(R.id.textview_header).text = countText`

//生成随机数

`val random = java.util.Random()
var randomNumber = 0
if (count > 0) {
   randomNumber = random.nextInt(count + 1)
}`

//显示count值

`view.findViewById<TextView>(R.id.textview_random).text = randomNumber.toString()`



## 七、整体运行结果



## 第一界面图：

![image-20220430224816565](C:\Users\86130\Desktop\img\image-20220430224816565.png)



## 第二界面图：



![image-20220430224828844](C:\Users\86130\Desktop\img\image-20220430224828844.png)