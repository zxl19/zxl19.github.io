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

SLAM学习资料存档，包括SLAM基础理论、卡尔曼滤波、组合导航等。

<!-- more -->

## SLAM基础理论

### 书籍

1. 《视觉SLAM十四讲》
2. 《自动驾驶中的SLAM技术》
3. [Factor graphs for robot perception](https://www.cs.cmu.edu/~kaess/pub/Dellaert17fnt.html)
4. [A tutorial on SE(3) transformation parameterizations and on-manifold optimization](http://ingmec.ual.es/~jlblanco/papers/jlblanco2010geometry3D_techrep.pdf)
5. [A micro Lie theory for state estimation in robotics](https://arxiv.org/pdf/1812.01537.pdf)
6. [Quaternion kinematics for the error-state Kalman filter](https://www.iri.upc.edu/people/jsola/JoanSola/objectes/notes/kinematics.pdf)
7. [Probabilistic Robotics](https://gaoyichao.com/Xiaotu//resource/refs/PR.MIT.en.pdf)
8. [State Estimation for Robotics -- First Edition](http://asrl.utias.utoronto.ca/~tdb/bib/barfoot_ser17.pdf)
9. [State Estimation for Robotics -- Draft Second Edition](http://asrl.utias.utoronto.ca/~tdb/bib/barfoot_ser23.pdf)
10. [SO(3) and SE(3) Identities and Approximations](http://asrl.utias.utoronto.ca/~tdb/bib/barfoot_ser17_identities.pdf)
11. [Lie theory cheatsheet](https://norlab.ulaval.ca/research/LieCheatsheet/)
12. [Multiple view geometry in computer vision](https://assets.cambridge.org/97805215/40513/frontmatter/9780521540513_frontmatter.pdf)
13. [Modern Robotics](http://hades.mech.northwestern.edu/images/7/7f/MR.pdf)

### GitHub

1. [gaoxiang12/slambook](https://github.com/gaoxiang12/slambook)
2. [gaoxiang12/slambook2](https://github.com/gaoxiang12/slambook2)
3. [gaoxiang12/slambook-en](https://github.com/gaoxiang12/slambook-en)
4. [gaoxiang12/slam_in_autonomous_driving](https://github.com/gaoxiang12/slam_in_autonomous_driving)
5. [AlbertSlam/Lee-SLAM-source](https://github.com/AlbertSlam/Lee-SLAM-source)
6. [jlblancoc/tutorial-se3-manifold](https://github.com/jlblancoc/tutorial-se3-manifold)
7. [StevenCui/VIO-Doc](https://github.com/StevenCui/VIO-Doc)
8. [PetWorm/IMU-Preintegration-Propogation-Doc](https://github.com/PetWorm/IMU-Preintegration-Propogation-Doc)
9. [PetWorm/IMU_error_state_propagation_doc](https://github.com/PetWorm/IMU_error_state_propagation_doc)
10. [norlab-ulaval/cheatsheet_LieAlgebra](https://github.com/norlab-ulaval/cheatsheet_LieAlgebra)
11. [jlblancoc/factor-graphs-course](https://github.com/jlblancoc/factor-graphs-course)
12. [gongbingg/slam](https://github.com/gongbingg/slam)
13. [Joanna-HE/Supplementary-file-for-IKFoM](https://github.com/Joanna-HE/Supplementary-file-for-IKFoM)
14. [brytsknguyen/slict](https://github.com/brytsknguyen/slict)
15. [brytsknguyen/oblam_deskew](https://github.com/brytsknguyen/oblam_deskew)

### 公开课

1. [泡泡机器人](https://space.bilibili.com/38737757)
2. [深蓝学院](https://www.shenlanxueyuan.com)
3. [RI Seminar: Michael Kaess: Robust and Efficient Real-time Mapping for Autonomous Robots](https://www.youtube.com/watch?v=_W3Ua1Yg2fk)
4. [Optimization-based Localization And Mapping-KTH](https://canvas.kth.se/courses/40649)

## 卡尔曼滤波

### 网站

1. [Kalman Filter Tutorial](https://www.kalmanfilter.net/default.aspx)
2. [The Kalman Filter](https://www.cs.unc.edu/~welch/kalman/)
3. [An Introduction to the Kalman Filter](https://www.cs.unc.edu/~welch/media/pdf/kalman_intro.pdf)
4. [An Introduction to the Kalman Filter-SIGGRAPH 2001](https://www.cs.unc.edu/~tracker/media/pdf/SIGGRAPH2001_CoursePack_08.pdf)
5. [Tutorial: The Kalman Filter](https://web.mit.edu/kirtley/kirtley/binlustuff/literature/control/Kalman%20filter.pdf)
6. [A Kalman Filtering Tutorial for Undergraduate Students](https://aircconline.com/ijcses/V8N1/8117ijcses01.pdf)
7. [Extended Kalman Filter Tutorial](https://homes.cs.washington.edu/~todorov/courses/cseP590/readings/tutorialEKF.pdf)
8. [简明ESKF推导-半闲居士的文章-知乎](https://zhuanlan.zhihu.com/p/441182819)
9. [LIO中ESKF相关公式的详尽说明-xiaotaw的文章-知乎](https://zhuanlan.zhihu.com/p/538975422)
10. [Computing Jacobian, why error state?——优化中为何对误差状态求导-邱笑晨的文章-知乎](https://zhuanlan.zhihu.com/p/75714471)
11. [简单易懂(?)的误差状态卡尔曼滤波器(Error State Kalman Filter, ESKF)的原理与实现（一）原理简介-llo的文章-知乎](https://zhuanlan.zhihu.com/p/545370811)
12. [简单易懂(?)的误差状态卡尔曼滤波器(Error State Kalman Filter, ESKF)的原理与实现（二）算法实现-llo的文章-知乎](https://zhuanlan.zhihu.com/p/545525697)

### GitHub

#### MATLAB

1. [yuzhou42/MSCKF](https://github.com/yuzhou42/MSCKF)
2. [alirezaahmadi/KalmanFilter-Vehicle-GNSS-INS](https://github.com/alirezaahmadi/KalmanFilter-Vehicle-GNSS-INS)
3. [yuzhou42/ESKF-Attitude-Estimation](https://github.com/yuzhou42/ESKF-Attitude-Estimation)

#### Python

1. [rlabbe/filterpy](https://github.com/rlabbe/filterpy)
2. [pykalman/pykalman](https://github.com/pykalman/pykalman)
3. [commaai/rednose](https://github.com/commaai/rednose)
4. [zziz/kalman-filter](https://github.com/zziz/kalman-filter)
5. [enginBozkurt/Error-State-Extended-Kalman-Filter](https://github.com/enginBozkurt/Error-State-Extended-Kalman-Filter)
6. [diegoavillegasg/IMU-GNSS-Lidar-sensor-fusion-using-Extended-Kalman-Filter-for-State-Estimation](https://github.com/diegoavillegasg/IMU-GNSS-Lidar-sensor-fusion-using-Extended-Kalman-Filter-for-State-Estimation)
7. [aipiano/ESEKF_IMU](https://github.com/aipiano/ESEKF_IMU)
8. [soarbear/imu_ekf](https://github.com/soarbear/imu_ekf)
9. [jnez71/kalmaNN](https://github.com/jnez71/kalmaNN)

#### C++

1. [mherb/kalman](https://github.com/mherb/kalman)
2. [hmartiro/kalman-cpp](https://github.com/hmartiro/kalman-cpp)
3. [sfwa/ukf](https://github.com/sfwa/ukf)
4. [xiahouzuoxin/kalman_filter](https://github.com/xiahouzuoxin/kalman_filter)
5. [artivis/kalmanif](https://github.com/artivis/kalmanif)
6. [hku-mars/IKFoM](https://github.com/hku-mars/IKFoM)
7. [jeremyfix/easykf](https://github.com/jeremyfix/easykf)
8. [je310/ESKF](https://github.com/je310/ESKF)
9. [pronenewbits/Embedded_EKF_Library](https://github.com/pronenewbits/Embedded_EKF_Library)
10. [pronenewbits/Embedded_UKF_Library](https://github.com/pronenewbits/Embedded_UKF_Library)
11. [OpenSLAM-org/openslam_MTK](https://github.com/OpenSLAM-org/openslam_MTK)
12. [xinyang-go/eskf](https://github.com/xinyang-go/eskf)
13. [zha0ming1e/InEKF](https://github.com/zha0ming1e/InEKF)

## 组合导航

### 网站

1. [高精度捷联惯性导航算法](http://www.psins.org.cn)
2. [卡尔曼滤波与组合导航原理【西北工业大学 严恭敏】](https://www.bilibili.com/video/BV11K411J7gp)
3. [PSINS导航工具箱入门与详解【西北工业大学 严恭敏】](https://www.bilibili.com/video/BV1R54y1E7ut)
4. [简明预积分推导-半闲居士的文章-知乎](https://zhuanlan.zhihu.com/p/388859808)

### GitHub

1. [benzenemo/TightlyCoupledINSGNSS](https://github.com/benzenemo/TightlyCoupledINSGNSS)
2. [i2Nav-WHU/Wheel-SLAM](https://github.com/i2Nav-WHU/Wheel-SLAM)
3. [yuzhou42/GPS-INS-Integrated-Navigation](https://github.com/yuzhou42/GPS-INS-Integrated-Navigation)
4. [jayoungo/SINS-GPS-Integrated-Navigation](https://github.com/jayoungo/SINS-GPS-Integrated-Navigation)

## 自动驾驶

### 网站

1. [无人驾驶领域，你推荐那些综述性文章？-王方浩的回答-知乎](https://www.zhihu.com/question/355954682/answer/897296676)
2. [Dig into Apollo](https://dig-into-apollo.readthedocs.io/en/latest/index.html)
3. [Apollo 开放平台](https://daobook.github.io/apollo-book/docs/start/index.html)

### GitHub

1. [ApolloAuto/apollo](https://github.com/ApolloAuto/apollo)
2. [daohu527/dig-into-apollo](https://github.com/daohu527/dig-into-apollo)
3. [YannZyl/Apollo-Note](https://github.com/YannZyl/Apollo-Note)
4. [autowarefoundation/autoware](https://github.com/autowarefoundation/autoware)

## 参考

1. [《视觉SLAM学习过程所用资料总结》-行知SLAM的文章-知乎](https://zhuanlan.zhihu.com/p/259917664)
2. [聊聊这两年学习slam啃过的书！-小凡的文章-知乎](https://zhuanlan.zhihu.com/p/293039582)
3. [超全SLAM学习资源汇总-阿木实验室的文章-知乎](https://zhuanlan.zhihu.com/p/116769131)
4. [SLAM相关学习资料：综述/激光/视觉/数据集/常用库-菠萝包包包的文章-知乎](https://zhuanlan.zhihu.com/p/434874344)
5. [李群和李代数——名字听起来很猛其实也没那么复杂-菠萝包包包的文章-知乎](https://zhuanlan.zhihu.com/p/358455662)
6. [Probabilistic Robotics](http://robots.stanford.edu/probabilistic-robotics/)
7. [Tim Barfoot](http://asrl.utias.utoronto.ca/~tdb/)
8. [Modern Robotics](http://hades.mech.northwestern.edu/index.php/Modern_Robotics)
9. [硕士研究生阶段如何学习slam机器人？-Range的回答-知乎](https://www.zhihu.com/question/396119527/answer/1235876702)
10. [严恭敏的个人主页](https://teacher.nwpu.edu.cn/yangongmin.html)
