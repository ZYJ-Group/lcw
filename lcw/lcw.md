VINS详解：https://blog.csdn.net/afucc111/article/details/127104948?spm=1001.2014.3001.5501  
ORBSLAM2详解：https://blog.csdn.net/afucc111/article/details/126237586?spm=1001.2014.3001.5501  

#### 总目标：
    使用毫米波雷达补全激光雷达点云，并赋予点云RGB信息，完成复杂环境建图。  
    任务拆解：  
    
    1、毫米波雷达与激光雷达标定    
    2、毫米波雷达点云优化
    3、毫米波雷达点云与激光雷达点云对齐
    4、设定特殊环境（环境中存在形状不一的玻璃），使用学习方法：根据图像信息得到玻璃的形状
    5、依据玻璃形状，以毫米波雷达与激光雷达点云为基础，填补点云空洞。
    6、点云RGB赋值

##### 2022.11.18 脱离秋招第一周        
#### 计划：  

    1、复现r3live（由于设备被移动需要重新标定）
    2、考虑改变毫米波雷达改变毫米波雷达建图方式：  
    原先是基于轮式里程计+octomap工具完成建图、考虑是否可以使用r3live输出的里程计信息替代轮式里程计，优化建图结果。  
    （这一步主要是增强了毫米波雷达建图的鲁棒性，因为原轮式里程计只可以在地面上使用）
    注：第2步亦可不做，因为现有设备是基于turtlebot2的，所以使用轮式里程计也可以。
    
##### 2022.11.25  
#### 结果：  

    1、激光雷达与相机标定工作：
    使用了香港大学开源框架lidar_camera_calib，但是使用过程中发现bug，使用gdb逐行调试，发现是pcl库中的点云分割器中的一个函数出现内存溢出的错误，猜测是由于pcl、vtk版本等问题。
    遂使用了点对点的标定方法，完成标定。
    2、r3live数据集复现完成
    
#### 计划：  

    1、复现r3live（由于设备被移动需要重新标定）
    2、分析激光雷达点云，查找点云空洞补全方法。
    暂定方案：
          1、激光雷达点云取‘非’处理
          2、icp匹配毫米波雷达点云与上述激光雷达处理后的点云
          
##### 2022.12.01  
#### 结果：  

    1、完成标定
    2、r3live复现完成
    3、大论文框架
    4、fastlio复现完成
    
    <div align=center>
    <img width="500" alt="image" src="https://github.com/ZYJ-Group/lcw/blob/153493d5a3e7584b024556e05c7c9e7b130b9a64/lcw/image/1.png">
    <img width="500" alt="image" src="https://github.com/ZYJ-Group/lcw/blob/153493d5a3e7584b024556e05c7c9e7b130b9a64/lcw/image/4.png">
    <img width="500" alt="image" src="https://github.com/ZYJ-Group/lcw/blob/153493d5a3e7584b024556e05c7c9e7b130b9a64/lcw/image/6.png">
    <img width="500" alt="image" src="https://github.com/ZYJ-Group/lcw/blob/153493d5a3e7584b024556e05c7c9e7b130b9a64/lcw/image/7.png">
    <img width="500" alt="image" src="https://github.com/ZYJ-Group/lcw/blob/153493d5a3e7584b024556e05c7c9e7b130b9a64/lcw/image/8.png">
    </div>
    
#### 计划：  

    1、大论文第一章
    2、r3live、标定优化
