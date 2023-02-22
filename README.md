# RobotRTS_Mas

Mas哨兵开发框架文档

相关链接：

> RoboRTS文档：https://robomaster.github.io/RoboRTS-Tutorial/#/sdk_docs/architecture
>
> RoboRTS仓库：https://github.com/RoboMaster/RoboRTS
>
> 嵌入式端仓库：https://github.com/RoboMaster/RoboRTS-Firmware
>
> roborts_base模块最新仓库：https://github.com/RoboMaster/RoboRTS-Base
>
> 可参考：
>
> 中科院自动化所rmua：https://github.com/DRL-CASIA/RMAI2020-Planning
>
> 哈工深ruma：https://github.com/Critical-HIT-hitsz/RMUA2022

>URDF文档：http://wiki.ros.org/cn/urdf
>机器人状态发布者（Robot State Publisher）文档：http://wiki.ros.org/robot_state_publisher


第一次写readme不太会有问题随时问我
步骤可能有写的不清楚一类的，有问题找我就好啦！我也不一定会的（
因为图纸还没完成所以是用近似比例的值设定的参数（称为sam_XXXXX)

## 机器人首次设置Nav必须要进行的工作

一、 设置URDF
# 文件结构（要用工具软件RVIZ）

sam_bot_description
    |———— config
        |———— ekf.yaml
        |———— nav2_paramsyaml
    |———— launch
        |———— display.launch.py 启动文件
    |———— rviz
        |———— urdf_config.rviz 初始化RVIZ并可以启动后立即查看
    |———— src
        |———— description
            |———— sam_bot_description.urdf  构建机器人模型，碰撞体积以及尺寸等
    |———— world
        |———— my_world.sdf
    |———— CMakeLists.txt 是cmake阿巴阿巴阿巴
    |———— package.xml  添加构建项目所需依赖包
    |———— README.md    

# 如何使用
构建项目：
进入项目根目录并执行以下命令：

colcon build

. install/setup.bash

构建成功后，执行以下命令来安装该ROS 2软件包并启动该项目：

ros2 launch sam_bot_description display.launch.py

现在ROS 2应该会启动一个机器人发布者节点并使用上面编写的URDF启动RVIZ
然后你现在就可以看到可视化的简陋max机器人模型啦！
好耶ヾ(✿ﾟ▽ﾟ)ノ！

在RVIZ左边的RobotModel下启用Collision Enabled来验证是否正确设置了碰撞区域（如果还将Visual Enabled关闭掉可能会更容易查看）

这一步骤可以查看是否正确定义机器人URDF，有利于发布正确坐标变换

关节状态发布者GUI里面滑动车轮滑动条可以看到车轮关节转动

上面这些工作的目的：发布从base_link到sensor_frames的正确坐标变换
