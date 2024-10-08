# Task02

## 1.配置 C++ 开发环境&安装 OpenCV 库 与构建项目结构

* 我依照着section 1为教程进行操作，这个过程很顺利。

## 2.对图像进行处理操作

* 通过自己摸索和结合自己本来的C++知识，我首先理解了Mat变量这个概念，同时后续的vetor变量，以及后续一系列函数，我已经学会了它们的操作，即使不会，我也知道向chatgpt询问特定函数的语法与作用达到现场学习的目的。
在前四个操作中，没有报错。

## 在接下来的操作中我分别遇到不同类型的问题，我主要的求助方式是chatgpt。

### 第一个问题是：提取红色区域时，第一次所提取的并不完全是红色区域，把白色区域等等也提取进来了。通过不断和chatgpt询问以及VScode自带的函数说明（虽然是英文的），我明白了hsv中的红色这个阈值需要自己来调试（然而红色应该是有严格定义的），我在CSDN上搜索一番，再加上自己的调试，我实现了提取红色区域的优化。

![调试前](assets/1-1.png) 

![优化后](assets/1-3.png) 

### 第二个问题是：我总是烦恼于我检查不出来的“核心已转储”的问题，在几乎对chatgpt询问了题中用到的所有的函数的语法后，我发觉：出于某种原因，chatgpt所给的代码中函数的值并不对（无论如何我的电脑上会出现核心已转储），最终我解决了这个问题，也学习到了函数中对数值的类型的要求。

**例如：imwrite（”img“， img） 是不对的，应该是 imwrite("img.png", img)；*
**以及ffindcontours的括号里第一个输入的图像应该是canny图；*

### 第三个问题是：在对图像绘制boundingbox时，会导致对img原图的修改，如果按照任务书中的顺序来进行的话，那么所生成的结果就不是对原图的修改了，这有两种解决办法，一种是进行操作的时候在定义mat变量读入原图，但我选择另外一种，也就是改变操作顺序，我先实行不会对原图有修改的操作如旋转裁剪等，这些的结果会存储在另外的mat中。这是我优化他们的方法。我在源代码中也有进行对应的注释。

![调试前](assets/4-3.png)

![调试前](assets/4-2.png)

![优化后](assets/4-5.png)

### 第四个问题是：chatgpt所给的计算轮廓面积的代码是一个for循环，这样会使输出的值很多，大部分都是噪声小轮廓，area=0。于是我进行了对应的优化，我把for循环里的计算删掉，给了一个sum值，并在for循环结束之后输出sum值即可。

![调试前](assets/5-1.png)

![优化后](assets/5-2.png)

### 最后一个细小的优化就是:高亮区域的细化，在第三个问题的解决后我仍然觉得高亮区域所提取出来的图像不好，于是这次我详细询问了chatgpt“hsv这些阈值到底都是什么”，也通过这个方式解决了我的疑惑，h色相，s饱和，h亮度，那么根据原图的具体亮度，我再在其中提取高亮区域，我就可以将高阈值的亮度拉满（255），低阈值也拉高到一定程度（我的代码中是150），这样出来的图我就满意一点了。

![调试前](assets/4-5.png)

![优化后](resources/hlgry.png)

## 3.思考题：如何上传的时候不带build/？

* 我的答案：把编译好的OpenCV_Project复制到opencvproject文件夹里，然后上传的时候就不需要包含build/了.

