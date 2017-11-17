# selfdriving
selfdriving information


# 无人驾驶技术点

## 感知

### 定位

#### GPS / BDS + IMU融合（卡尔曼滤波）

#### 视觉定位

##### 双目左右图像特征点提取（Harris / SIFT / HOG算法）

##### 对比两帧对应关系（RANSAC / ICP算法）

##### 推算两帧之间运动，计算位置

#### 激光点云定位（粒子滤波）

### 视觉感知

#### 图像分割（像素级的前景分类，背景剔除）

##### FCN / U-Net / SegNet / DeconvNet等算法

#### 目标检测（定位目标，确定目标位置及大小）

##### Faster R-CNN / MSCNN / SSD等算法

#### 目标识别（定性目标，确定目标是什么）

##### CNN加分类器如SVM

#### 目标跟踪（追踪目标运动轨迹）

##### tracking-by-detection思想，基于马尔科夫算法（MDP）

### 激光感知

#### 障碍物检测与跟踪（与视觉感知算法雷同）

#### 路面检测（检测路面材质和坡度）

#### 实时3D地图构建（3D SLAM）

#### 高精地图生成

##### 原始数据处理 -> 点云生成 

##### 点云对齐 -> 2D反射地图生成

##### 高精地图标注 -> 地图生成

### 雷达感知（不需过多处理，可用于避障的最后一道防线）

### 听觉感知

#### 识别特殊车辆音频信号（如救护车 / 消防车）

#### 识别应急广播 / 语音交互指令

## 决策规划

### 信息综合

#### 无人车信息（当前状态、历史状态）

#### 障碍物信息（定位、距离、行为意图 / 预测轨迹等）

#### 高精地图（交通标识、车道、道路宽度 / 坡度 / 曲率等）

#### 实时交通信息（路况 / 事件）

#### 音频处理信息

### 信息融合
行为决策

#### 行为

##### 行车 / 跟车

##### 换道 / 超车

##### 让行 / 躲避

##### 转弯 / 停车

#### 方法

##### Rule-based（有限状态机 / 决策树等）

##### 增强学习应用（Deep Q-Learning等）

##### 马尔科夫决策（MDP）

### 轨迹规划

#### 全局路径规划（基于导航地图，AStar / Dijkstra）

#### 车道级轨迹规划（基于高精地图，ADASIS协议）

#### 局部运动规划

##### 基于采样算法（OMPL）

##### 基于搜索算法（SBPL）

##### 局部避障（DWA）

## 控制

### 横向控制

#### 经典控制方法（如比例积分微分PID）

#### 最优控制方法（基于预瞄式横向动力学模型）

#### Hoo鲁棒控制方法

#### 基于反馈线性化方法

#### 自适应控制方法

#### 滑模控制方法

#### 预测控制方法（如基于线性时变预测模型）

#### 模糊控制方法

### 纵向控制

#### 直接式结构控制（由一个控制器输出控制给所有子系统）

#### 分层式结构控制（设计上、下位控制器）

### 综合控制

#### 分解式协调控制（独立设计横纵向控制律，设计协调横纵向控制逻辑）

#### 集中式协调控制（对车辆横纵向耦合动力学模型直接控制求解，得到横纵向控制律）

## 安全

### 系统安全

#### 通信安全

##### 通信加密与验证

##### 限制关键系统之间通信

#### 固件安全

##### 可验证

##### OTA

#### 各子系统冗余备份设计

#### 实时原始数据记录

### 系统测试

#### 模拟器测试

#### 封闭区域模拟场景测试

#### 公开道路实际场景测试

#### 防碰撞测试

#### 极端环境测试

### 故障实时检测与规避

### 人机交互安全设计

## 云平台&大数据

### 标注数据集

#### 2D / 3D数据（分类图像，标注点云）

#### 驾驶场景数据

#### 异常场景数据（碰撞 / 事故等）

### 离线模型训练

#### 感知模型训练 / 验证

#### 决策模型训练 / 验证

### 驾驶模拟仿真

#### 感知 / 决策 / 控制仿真

#### 历史数据回放

### 大数据运营平台

#### 无人驾驶数据采集 / 存储

#### 数据检索 / 分析 / 可视化

#### 无人车运营监控

### 高精地图生产平台

## 基础部件

### 传感器

#### GPS / BDS + INS

##### GPS / BDS（RTK，10HZ）

##### IMU（200HZ）

#### LIDAR

##### 机械旋转式（Velodyne，20HZ旋转）

##### 固态激光

###### MEMS（用旋转的微振镜来反射激光器的光线来扫描）

###### OPA（光学相控阵技术）

###### Flash（短时间发射出探测区域的激光，高灵敏接收器接收）

#### RADAR

##### 毫米波（77GHZ / 24GHZ）

##### 超声波（20KHZ）

#### 视觉摄像头

##### 芯片类型

###### CCD（电荷耦合元件）

###### CMOS（互补金属氧化物半导体）

##### 应用场景

###### 前视（单目/双目，ACC / FCW / LDW / AEB等）

###### 后视（广角，AP）

###### 环视（广角，SVC / AP）

###### 内置（广角，疲劳检测）

#### 红外传感器

##### 夜视场景

#### 听觉

##### 局域（麦克风阵列） 

##### 广域（电台 / 手机等音频）

### 计算单元

#### 芯片方案

##### GPU

###### NVIDIA PX2

##### DSP

###### TI TDA2 SoC

##### FPGA

###### Altera Cyclone V SoC

##### ASIC

###### MobilEye EyeQ5

#### 计算架构

##### 中心式

###### 各子节点将原始数据传输给中心，
中心处理数据，制定决策

##### 分布式

###### 各子节点完成高度数据处理，
向中心传输结果数据，
中心根据结果信息制定决策

##### 混合式

###### 考虑中心式和分布式弊端的平衡架构

### 通信

#### DSRC

##### 欧美，基于IEEE802.11p 

#### LTE-V2X

##### 中国，基于3G / 4G / 5G

### 中间件

#### ROS

#### 端DL框架

##### Tensorflow / Caffe2 / Mxnet
