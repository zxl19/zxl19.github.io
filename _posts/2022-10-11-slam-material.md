---
layout: post
title: SLAM学习资料存档
date: 2022-10-11
author: zxl19
tags: [SLAM, Archive]
comments: true
toc: true
pinned: false
---

我的SLAM学习资料存档，包括SLAM基础理论、卡尔曼滤波、组合导航等。

<!-- more -->

## SLAM基础理论

### 入门教材

1. [Course on SLAM](https://www.iri.upc.edu/people/jsola/JoanSola/objectes/toolbox/courseSLAM.pdf)
2. [SLAM for Dummies](https://dspace.mit.edu/bitstream/handle/1721.1/119149/16-412j-spring-2005/contents/projects/1aslam_blas_repo.pdf)

### 综述教材

1. 《视觉SLAM十四讲》
2. 《自动驾驶中的SLAM技术》
3. [Factor graphs for robot perception](https://www.cs.cmu.edu/~kaess/pub/Dellaert17fnt.html)
4. [Probabilistic Robotics](https://gaoyichao.com/Xiaotu//resource/refs/PR.MIT.en.pdf)
5. [State Estimation for Robotics -- First Edition](http://asrl.utias.utoronto.ca/~tdb/bib/barfoot_ser17.pdf)
6. [State Estimation for Robotics -- Draft Second Edition](http://asrl.utias.utoronto.ca/~tdb/bib/barfoot_ser23.pdf)
7. [Multiple view geometry in computer vision](https://assets.cambridge.org/97805215/40513/frontmatter/9780521540513_frontmatter.pdf)
8. [Modern Robotics](http://hades.mech.northwestern.edu/images/7/7f/MR.pdf)

### 微分几何和李群

#### 速查表

1. [SO(3) and SE(3) Identities and Approximations](http://asrl.utias.utoronto.ca/~tdb/bib/barfoot_ser17_identities.pdf)
2. [Lie theory cheatsheet](https://norlab.ulaval.ca/research/LieCheatsheet/)

#### 位姿参数化

1. [A tutorial on SE(3) transformation parameterizations and on-manifold optimization](http://ingmec.ual.es/~jlblanco/papers/jlblanco2010geometry3D_techrep.pdf)
2. [Quaternions and Rotations](https://graphics.stanford.edu/courses/cs348a-17-winter/Papers/quaternion.pdf)
3. [Lie Groups for 2D and 3D Transformations](https://ethaneade.com/lie.pdf)

#### 在线位姿转换

1. [Engineering Notes](https://danceswithcode.net/danceswithcode.net/engineeringnotes/index.html)
2. [3D Rotation Converter](https://www.andre-gaschler.com/rotationconverter/)
3. [Quaternions](https://quaternions.online)

#### 李群和李代数

1. [A micro Lie theory for state estimation in robotics](https://arxiv.org/pdf/1812.01537)
2. [Kalman Filters on Differentiable Manifolds](https://arxiv.org/pdf/2102.03804)
3. [Quaternion kinematics for the error-state Kalman filter](https://www.iri.upc.edu/people/jsola/JoanSola/objectes/notes/kinematics.pdf)
4. [Differential Geometry and Lie Groups](https://www.cis.upenn.edu/~jean/gbooks/manif.html)
5. [如何通俗地解释李群和李代数的关系？-李狗嗨的回答-知乎](https://www.zhihu.com/question/356466246/answer/931315125)
6. [李群和李代数——名字听起来很猛其实也没那么复杂-菠萝包包包的文章-知乎](https://zhuanlan.zhihu.com/p/358455662)
7. [老师，我太想写SLAM了-李群/李代数篇-吴小奇的文章-知乎](https://zhuanlan.zhihu.com/p/688748332)
8. [工科生学习微分几何和李群学习的建议？-贺磊的回答-知乎](https://www.zhihu.com/question/29908951/answer/89652188)
9. [工科生学习微分几何和李群学习的建议？-FrankDellaert的回答-知乎](https://www.zhihu.com/question/29908951/answer/3608055723)

### 后端优化

1. [SLAM中后端优化的技术细节-Wincent的文章-知乎](https://zhuanlan.zhihu.com/p/616060837)
2. [如何理解SLAM中的First-Estimates Jacobian？-jing胖的回答-知乎](https://www.zhihu.com/question/52869487/answer/132517493)
3. [如何理解SLAM中的First-Estimates Jacobian？-拿破轮的回答-知乎](https://www.zhihu.com/question/52869487/answer/2437797244)
4. [如何理解SLAM中的First-Estimates Jacobian？-庞富民的回答-知乎](https://www.zhihu.com/question/52869487/answer/258663651)
5. [First Estimate Jacobian与非线性优化迭代求解Jacobian相互矛盾吗？-快使用双截棍巴拉的回答-知乎](https://www.zhihu.com/question/291360996/answer/478536964)
6. [一文看尽4种SLAM中零空间的维护方法-wuRDmemory的文章-知乎](https://zhuanlan.zhihu.com/p/341322063)

### GitHub

#### 理论知识

1. [gaoxiang12/slambook](https://github.com/gaoxiang12/slambook)
2. [gaoxiang12/slambook2](https://github.com/gaoxiang12/slambook2)
3. [gaoxiang12/slambook-en](https://github.com/gaoxiang12/slambook-en)
4. [gaoxiang12/slam_in_autonomous_driving](https://github.com/gaoxiang12/slam_in_autonomous_driving)
5. [AlbertSlam/Lee-SLAM-source](https://github.com/AlbertSlam/Lee-SLAM-source)
6. [StevenCui/VIO-Doc](https://github.com/StevenCui/VIO-Doc)
7. [Taeyoung96/SLAM-Resources-for-Beginner](https://github.com/Taeyoung96/SLAM-Resources-for-Beginner)
8. [jlblancoc/tutorial-se3-manifold](https://github.com/jlblancoc/tutorial-se3-manifold)
9. [PetWorm/IMU-Preintegration-Propogation-Doc](https://github.com/PetWorm/IMU-Preintegration-Propogation-Doc)
10. [PetWorm/IMU_error_state_propagation_doc](https://github.com/PetWorm/IMU_error_state_propagation_doc)
11. [gongbingg/slam](https://github.com/gongbingg/slam)
12. [jlblancoc/factor-graphs-course](https://github.com/jlblancoc/factor-graphs-course)
13. [norlab-ulaval/cheatsheet_LieAlgebra](https://github.com/norlab-ulaval/cheatsheet_LieAlgebra)
14. [TheSeanParker/SLAM_Materials](https://github.com/TheSeanParker/SLAM_Materials)
15. [lovelyyoshino/Chinese_Notes](https://github.com/lovelyyoshino/Chinese_Notes)
16. [Joanna-HE/Supplementary-file-for-IKFoM](https://github.com/Joanna-HE/Supplementary-file-for-IKFoM)

#### 源码分析

1. [TurtleZhong/Map-based-Visual-Localization](https://github.com/TurtleZhong/Map-based-Visual-Localization)
2. [slam-code/SLAM](https://github.com/slam-code/SLAM)
3. [brytsknguyen/slict](https://github.com/brytsknguyen/slict)
4. [lovelyyoshino/FAST_LIO2_Noted](https://github.com/lovelyyoshino/FAST_LIO2_Noted)
5. [Tompson11/SLAM_comparison](https://github.com/Tompson11/SLAM_comparison)
6. [ckddls1321/SLAM_Resources](https://github.com/ckddls1321/SLAM_Resources)
7. [ganlumomo/VisualInertialOdometry](https://github.com/ganlumomo/VisualInertialOdometry)
8. [YZH-bot/SLAM_NOTED](https://github.com/YZH-bot/SLAM_NOTED)
9. [lovelyyoshino/direct_lidar_inertial_odometry-noted](https://github.com/lovelyyoshino/direct_lidar_inertial_odometry-noted)
10. [brytsknguyen/oblam_deskew](https://github.com/brytsknguyen/oblam_deskew)
11. [YZH-bot/SLAM_Box](https://github.com/YZH-bot/SLAM_Box)

### 公开课

1. [泡泡机器人](https://space.bilibili.com/38737757)
2. [深蓝学院](https://www.shenlanxueyuan.com)
3. [自动驾驶之心](https://www.zdjszx.com)
4. [RI Seminar: Michael Kaess: Robust and Efficient Real-time Mapping for Autonomous Robots](https://www.youtube.com/watch?v=_W3Ua1Yg2fk)
5. [Optimization-based Localization And Mapping-KTH](https://canvas.kth.se/courses/40649)

## 卡尔曼滤波

### 网站

1. [Kalman Filter Tutorial](https://www.kalmanfilter.net/default.aspx)
2. [The Kalman Filter](https://thekalmanfilter.com)
3. [The Kalman Filter](https://www.cs.unc.edu/~welch/kalman/)
4. [An Introduction to the Kalman Filter](https://www.cs.unc.edu/~welch/media/pdf/kalman_intro.pdf)
5. [An Introduction to the Kalman Filter-SIGGRAPH 2001](https://www.cs.utexas.edu/~pingali/CS378/2008sp/papers/SIGGRAPH2001_CoursePack_08.pdf)
6. [Tutorial: The Kalman Filter](https://web.mit.edu/kirtley/kirtley/binlustuff/literature/control/Kalman%20filter.pdf)
7. [A Kalman Filtering Tutorial for Undergraduate Students](https://aircconline.com/ijcses/V8N1/8117ijcses01.pdf)
8. [Extended Kalman Filter Tutorial](https://homes.cs.washington.edu/~todorov/courses/cseP590/readings/tutorialEKF.pdf)
9. [Understanding the Basis of the Kalman Filter Via a Simple and Intuitive Derivation](https://courses.physics.illinois.edu/ece420/sp2019/7_UnderstandingKalmanFilter.pdf)
10. [卡尔曼滤波（Kalman Filter）原理与公式推导-涅索斯衬衫的文章-知乎](https://zhuanlan.zhihu.com/p/48876718)
11. [卡尔曼滤波器（观测器）原理极简介绍-Aurelian的文章-知乎](https://zhuanlan.zhihu.com/p/42390886)
12. [卡尔曼滤波Kalman Filter之美在于什么？-自动驾驶之心的回答-知乎](https://www.zhihu.com/question/281995386/answer/3371567219)
13. [不同视角下的卡尔曼滤波-袁良信的文章-知乎](https://zhuanlan.zhihu.com/p/6934889820)
14. [怎样才叫真正理解卡尔曼滤波Kalman Filter？-荒唐病人的回答-知乎](https://www.zhihu.com/question/47559783/answer/2980976068)
15. [怎样才叫真正理解卡尔曼滤波Kalman Filter？-Taylor的回答-知乎](https://www.zhihu.com/question/47559783/answer/3340606745)
16. [怎样才叫真正理解卡尔曼滤波Kalman Filter？-半闲居士的回答-知乎](https://www.zhihu.com/question/47559783/answer/1935734819330979739)
17. [怎样才叫真正理解卡尔曼滤波Kalman Filter？-刘厂长的回答-知乎](https://www.zhihu.com/question/47559783/answer/2988744371)
18. [卡尔曼滤波方程组的深刻理解有哪些？-莫一林的回答-知乎](https://www.zhihu.com/question/53815343/answer/2689408189)
19. [卡尔曼滤波方程组的深刻理解有哪些？-WMSOFT的回答-知乎](https://www.zhihu.com/question/53815343/answer/1890583049370063516)
20. [卡尔曼滤波(1)：单变量卡尔曼滤波-gezp的文章-知乎](https://zhuanlan.zhihu.com/p/669327717)
21. [卡尔曼滤波(2)：线性卡尔曼滤波-gezp的文章-知乎](https://zhuanlan.zhihu.com/p/669330840)
22. [卡尔曼滤波(3)：连续时间线性系统的离散化-gezp的文章-知乎](https://zhuanlan.zhihu.com/p/670192674)
23. [卡尔曼滤波(4)：扩展卡尔曼滤波-gezp的文章-知乎](https://zhuanlan.zhihu.com/p/671410841)
24. [卡尔曼滤波(5)：无迹卡尔曼滤波-gezp的文章-知乎](https://zhuanlan.zhihu.com/p/672668369)
25. [简明ESKF推导-半闲居士的文章-知乎](https://zhuanlan.zhihu.com/p/441182819)
26. [slam中基于滤波的方法的问题及如何调参?-半闲居士的回答-知乎](https://www.zhihu.com/question/601596796/answer/3127818634)
27. [LIO中ESKF相关公式的详尽说明-xiaotaw的文章-知乎](https://zhuanlan.zhihu.com/p/538975422)
28. [Computing Jacobian, why error state?——优化中为何对误差状态求导-邱笑晨的文章-知乎](https://zhuanlan.zhihu.com/p/75714471)
29. [简单易懂(?)的误差状态卡尔曼滤波器(Error State Kalman Filter, ESKF)的原理与实现（一）原理简介-llo的文章-知乎](https://zhuanlan.zhihu.com/p/545370811)
30. [简单易懂(?)的误差状态卡尔曼滤波器(Error State Kalman Filter, ESKF)的原理与实现（二）算法实现-llo的文章-知乎](https://zhuanlan.zhihu.com/p/545525697)
31. [Error-State Kalman Filter理解与梗概推导-m米咔00的文章-知乎](https://zhuanlan.zhihu.com/p/359014822)
32. [FAST-LIO论文解读与详细公式推导-铁马冰河入梦来的文章-知乎](https://zhuanlan.zhihu.com/p/587500859)
33. [FAST-LIO公式推导-鬼木士的文章-知乎](https://zhuanlan.zhihu.com/p/561877392)
34. [Faster-LIO：快速激光IMU里程计-半闲居士的文章-知乎](https://zhuanlan.zhihu.com/p/468628910)
35. [lightning-lm-半闲居士的文章-知乎](https://zhuanlan.zhihu.com/p/1969360325880030621)

### 交互式仿真

1. [Interactive Kalman Filter](https://thekalmanfilter.com/interactive-kalman-filter/)
2. [The Extended Kalman Filter: An Interactive Tutorial for Non-Experts](https://simondlevy.github.io/ekf-tutorial/)
3. [1€ Filter Demo](https://gery.casiez.net/1euro/InteractiveDemo/)
4. [technitute/AKFSF-Simulation-CPP](https://github.com/technitute/AKFSF-Simulation-CPP)

### GitHub

#### MATLAB

1. [alirezaahmadi/KalmanFilter-Vehicle-GNSS-INS](https://github.com/alirezaahmadi/KalmanFilter-Vehicle-GNSS-INS)
2. [yuzhou42/MSCKF](https://github.com/yuzhou42/MSCKF)
3. [meyiao/LaserSLAM](https://github.com/meyiao/LaserSLAM)
4. [RomaTeng/EKF-SLAM-on-Manifold](https://github.com/RomaTeng/EKF-SLAM-on-Manifold)
5. [jaijuneja/ekf-slam-matlab](https://github.com/jaijuneja/ekf-slam-matlab)
6. [yuzhou42/ESKF-Attitude-Estimation](https://github.com/yuzhou42/ESKF-Attitude-Estimation)

#### Python

1. [rlabbe/Kalman-and-Bayesian-Filters-in-Python](https://github.com/rlabbe/Kalman-and-Bayesian-Filters-in-Python)
2. [rlabbe/filterpy](https://github.com/rlabbe/filterpy)
3. [pykalman/pykalman](https://github.com/pykalman/pykalman)
4. [commaai/rednose](https://github.com/commaai/rednose)
5. [zziz/kalman-filter](https://github.com/zziz/kalman-filter)
6. [enginBozkurt/Error-State-Extended-Kalman-Filter](https://github.com/enginBozkurt/Error-State-Extended-Kalman-Filter)
7. [diegoavillegasg/IMU-GNSS-Lidar-sensor-fusion-using-Extended-Kalman-Filter-for-State-Estimation](https://github.com/diegoavillegasg/IMU-GNSS-Lidar-sensor-fusion-using-Extended-Kalman-Filter-for-State-Estimation)
8. [aipiano/ESEKF_IMU](https://github.com/aipiano/ESEKF_IMU)
9. [soarbear/imu_ekf](https://github.com/soarbear/imu_ekf)
10. [jnez71/kalmaNN](https://github.com/jnez71/kalmaNN)

#### C++

1. [mherb/kalman](https://github.com/mherb/kalman)
2. [hmartiro/kalman-cpp](https://github.com/hmartiro/kalman-cpp)
3. [sfwa/ukf](https://github.com/sfwa/ukf)
4. [hku-mars/IKFoM](https://github.com/hku-mars/IKFoM)
5. [xiahouzuoxin/kalman_filter](https://github.com/xiahouzuoxin/kalman_filter)
6. [artivis/kalmanif](https://github.com/artivis/kalmanif)
7. [je310/ESKF](https://github.com/je310/ESKF)
8. [jeremyfix/easykf](https://github.com/jeremyfix/easykf)
9. [pronenewbits/Embedded_EKF_Library](https://github.com/pronenewbits/Embedded_EKF_Library)
10. [pronenewbits/Embedded_UKF_Library](https://github.com/pronenewbits/Embedded_UKF_Library)
11. [OpenSLAM-org/openslam_MTK](https://github.com/OpenSLAM-org/openslam_MTK)
12. [xinyang-go/eskf](https://github.com/xinyang-go/eskf)
13. [zha0ming1e/InEKF](https://github.com/zha0ming1e/InEKF)

## 组合导航

### 教材

1. 《捷联惯导算法与组合导航原理》
2. 《惯性仪器测试与数据分析》
3. 《惯性导航》

### 网站

1. [高精度捷联惯性导航算法](http://www.psins.org.cn)
2. [卡尔曼滤波与组合导航原理【西北工业大学 严恭敏】](https://www.bilibili.com/video/BV11K411J7gp/)
3. [PSINS导航工具箱入门与详解【西北工业大学 严恭敏】](https://www.bilibili.com/video/BV1R54y1E7ut/)
4. [武汉大学多源智能导航实验室](http://i2nav.cn)
5. [武汉大学惯性导航课程合集【2021年秋】](https://www.bilibili.com/video/BV1nR4y1E7Yj/)
6. [武汉大学研究生组合导航课程合集【2022年春】](https://www.bilibili.com/video/BV1na411Z7rQ/)
7. [A Guide To using IMU (Accelerometer and Gyroscope Devices) in Embedded Applications-Starlino Electronics](http://www.starlino.com/imu_guide.html)
8. [An introduction to inertial navigation](https://www.cl.cam.ac.uk/techreports/UCAM-CL-TR-696.pdf)
9. [A Short Tutorial on Inertial Navigation System and Global Positioning System Integration](https://ntrs.nasa.gov/api/citations/20150018921/downloads/20150018921.pdf)
10. [Introduction to Inertial Navigation](https://www.navlab.net/Publications/Introduction_to_Inertial_Navigation.pdf)
11. [Introduction to Inertial Navigation and Kalman Filtering](https://www.navlab.net/Publications/Introduction_to_Inertial_Navigation_and_Kalman_Filtering.pdf)
12. [简明预积分推导-半闲居士的文章-知乎](https://zhuanlan.zhihu.com/p/388859808)

### GitHub

1. [LiZhengXiao99/Navigation-Learning](https://github.com/LiZhengXiao99/Navigation-Learning)
2. [rodralez/NaveGo](https://github.com/rodralez/NaveGo)
3. [benzenemo/TightlyCoupledINSGNSS](https://github.com/benzenemo/TightlyCoupledINSGNSS)
4. [yandld/nav_matlab](https://github.com/yandld/nav_matlab)
5. [i2Nav-WHU/Wheel-SLAM](https://github.com/i2Nav-WHU/Wheel-SLAM)
6. [jayoungo/SINS-GPS-Integrated-Navigation](https://github.com/jayoungo/SINS-GPS-Integrated-Navigation)
7. [yuzhou42/GPS-INS-Integrated-Navigation](https://github.com/yuzhou42/GPS-INS-Integrated-Navigation)
8. [zelanzou/NaveCodePro](https://github.com/zelanzou/NaveCodePro)

## 自动驾驶

### 网站

1. [无人驾驶领域，你推荐那些综述性文章？-王方浩的回答-知乎](https://www.zhihu.com/question/355954682/answer/897296676)
2. [Dig into Apollo](https://dig-into-apollo.readthedocs.io/en/latest/index.html)
3. [Apollo 开放平台](https://daobook.github.io/apollo-book/docs/start/index.html)
4. [Algorithms for Automated Driving](https://thomasfermi.github.io/Algorithms-for-Automated-Driving/Introduction/intro.html)

### 专栏汇总

1. [SLAM与多传感器融合定位（专栏文章汇总）-任乾的文章-知乎](https://zhuanlan.zhihu.com/p/83775731)
2. [从零开始做自动驾驶定位（文章汇总）-任乾的文章-知乎](https://zhuanlan.zhihu.com/p/113616755)
3. [自动驾驶和机器人学习和总结专栏汇总-goldqiu的文章-知乎](https://zhuanlan.zhihu.com/p/645737781)

### GitHub

1. [commaai/openpilot](https://github.com/commaai/openpilot)
2. [ApolloAuto/apollo](https://github.com/ApolloAuto/apollo)
3. [autowarefoundation/autoware](https://github.com/autowarefoundation/autoware)
4. [daohu527/dig-into-apollo](https://github.com/daohu527/dig-into-apollo)
5. [OpenDriveLab/End-to-end-Autonomous-Driving](https://github.com/OpenDriveLab/End-to-end-Autonomous-Driving)
6. [OpenDriveLab/Birds-eye-view-Perception](https://github.com/OpenDriveLab/Birds-eye-view-Perception)
7. [YannZyl/Apollo-Note](https://github.com/YannZyl/Apollo-Note)
8. [thomasfermi/Algorithms-for-Automated-Driving](https://github.com/thomasfermi/Algorithms-for-Automated-Driving)
9. [slam-code/apollo](https://github.com/slam-code/apollo)
10. [nwaysir/Autopilot-Updating-Notes](https://github.com/nwaysir/Autopilot-Updating-Notes)

## VR&AR

1. [GeekLiB/AR-Source](https://github.com/GeekLiB/AR-Source)
2. [GeekLiB/Lee-VR-Source](https://github.com/GeekLiB/Lee-VR-Source)

## 参考

1. [超全SLAM学习资源汇总-阿木实验室的文章-知乎](https://zhuanlan.zhihu.com/p/116769131)
2. [SLAM相关学习资料：综述/激光/视觉/数据集/常用库-菠萝包包包的文章-知乎](https://zhuanlan.zhihu.com/p/434874344)
3. [硕士研究生阶段如何学习slam机器人？-Range的回答-知乎](https://www.zhihu.com/question/396119527/answer/1235876702)
4. [Probabilistic Robotics](http://robots.stanford.edu/probabilistic-robotics/)
5. [Tim Barfoot](http://asrl.utias.utoronto.ca/~tdb/)
6. [Modern Robotics](http://hades.mech.northwestern.edu/index.php/Modern_Robotics)
7. [工科生学习微分几何和李群学习的建议？-Aurelian的回答-知乎](https://www.zhihu.com/question/29908951/answer/309969236)
8. [Jean Gallier's Home Page for Books](https://www.cis.upenn.edu/~jean/gbooks/gbooks.html)
9. [工具网站推荐-欧拉角四元数在线可视化转化网站/三维在线旋转变换网站-CSDN博客](https://blog.csdn.net/hw140701/article/details/106255294)
10. [卡尔曼滤波仿真模拟网站合集-萧然的文章-知乎](https://zhuanlan.zhihu.com/p/1910702278677099081)
11. [怎样才叫真正理解卡尔曼滤波Kalman Filter？-确定有穷自动机的回答-知乎](https://www.zhihu.com/question/47559783/answer/2308644063)
12. [严恭敏的个人主页](https://teacher.nwpu.edu.cn/yangongmin.html)
13. [组合导航-开源工程推荐-郭洋的文章-知乎](https://zhuanlan.zhihu.com/p/640781392)
