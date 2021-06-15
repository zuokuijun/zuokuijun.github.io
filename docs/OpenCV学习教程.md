

>  用于记录OpenCV 视觉库的学习过程
>

## 一. 图像显示

* 新建工程文件

* 添加库函数的链接

  ```c++
  TEMPLATE = app
  CONFIG += console c++11
  CONFIG -= app_bundle
  CONFIG -= qt
  
  CONFIG += link_pkgconfig
  PKGCONFIG += opencv
  
  SOURCES += \
          main.cpp
  ```

* 编写测试程序

  ```c++
  
  #include <iostream>
  #include <opencv2/core/core.hpp>
  #include <opencv2/highgui/highgui.hpp>
  #include <opencv2/imgproc/imgproc.hpp>
  #include <opencv2/opencv.hpp>
  using namespace std;
  using namespace cv;
  
  int main(int argc,char *argv[])
  {
    Mat img = imread("/home/zuokuijun/opencvTest/1.jpg");
    imshow("[input a image]",img);
    waitKey(6000);
  }
  ```

  * 显示一张图片，并且6秒后显示窗口关闭
## 二、图像腐蚀

```c++
    Mat image = imread("/home/zuokuijun/OpenCV/charter2/1.jpg");
    imshow("image dmage process",image);
    Mat element = getStructuringElement(MORPH_RECT,Size(15,15));
    Mat dstImage;
    //start erode precess
    erode(image,dstImage,element);
    imshow("result image",dstImage);
    waitKey(0);
```

<p align="center">
<img src="./images/fushi.png"/>
</p>

## 三、图像模糊

```c++
      Mat image = imread("/home/zuokuijun/OpenCV/charter2/1.jpg");
      imshow("image blur",image);
      Mat dstImage;
      blur(image,dstImage,Size(7,7));
      imshow("blur result image",dstImage);
      waitKey(0);
```

<p align=center>
 <img src="./images/blur.png"/>
</p>

## 四、边缘检测

```c++
    Mat srcImage = imread("/home/zuokuijun/OpenCV/charter2/1.jpg");
    imshow("canny detection initial image",srcImage);
    Mat dstImage,edge,grayImage;

    dstImage.create(srcImage.size(),srcImage.type());
    cvtColor(srcImage,grayImage,COLOR_BGR2GRAY);

    blur(grayImage,edge,Size(3,3));

    Canny(edge,edge,3,9,3);

    imshow("canny detection result",edge);

    waitKey(0);
    return 0;
```

<p align="center">
<img src="./images/canny.png"/>
</p>

## 五、读取并播放视频

**此处的代码与下一部分调用摄像头进行图像采集的代码基本类似，只是在生成VideoCapture对象时，这里在实例化的过程中需要指定播放视频所在的具体路径**

<p align="center">
<img src="./images/video.png"/>
</p>

## 六、调用摄像头采集图像

```c++
    VideoCapture capture(0);
    Mat edges;
    while(1)
    {
        Mat frame;
        capture >> frame;

        cvtColor(frame,edges,CV_BGR2GRAY);

        blur(edges,edges,Size(7,7));

        Canny(edges,edges,0,30,3);
        imshow("my camera",edges);
        waitKey(30);
    }
    return 0;
```

<p align="center">
<img src="./images/camera.png"/>
</p>