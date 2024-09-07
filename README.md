# Guide belt
## 项目介绍  
我们小组的毕业设计是一款基于视觉识别和触感反馈的导盲腰带。主要分为视觉识别模块、数据交互模块与腰带模块三个部分。分别由三位同学负责。  
## 视觉识别模块  
视觉识别模块初步确定使用深度相机或是类似功能实现。通过深度相机，腰带可以感知周围环境，对周围物体进行实时建模，并进行实时测距。通过此方法建立数字化模型后，应当测算每个区域内所有障碍物特征点距离佩戴者的欧拉距离。此欧拉距离不应考虑远高于使用者头顶的障碍物情况，同时测算的距离应当是两点间（特征点-使用者）最短线段在水平面上投影的距离。此距离在下文中提到的扇区计算中会作为每个区域的“距离”使用。  
## 数据交互模块  
数据交互模块主要负责将输入的距离数据转化为腰带可用的电信号。我们设计将人正面的180°范围分为五个扇区，每个扇区再以腰部作为水平面分为上下两个部分。每个部分中距离人体直线距离最近的点会被视为这个扇区内障碍物距离人体的距离，这个距离会被正比例反馈到腰带上的触觉（或是听觉）反馈模块。 为了防止临时信号（例如两侧挥动的手臂）影响测量，交互模块应该具有一定的数据处理能力，可以屏蔽无效的距离数据。  
上文提到的数据处理算法应该是数据交互模块的本体。数据交互模块的目的应当是将多种不同格式的输出经过数据处理后发送给腰带上的执行器。  
## 腰带模块  
腰带模块需要具有合理的人机工学关系，合适的质量与可靠的结构强度。为了支持上文描述的五扇区规则，腰带上应该具有五个功能组，每个功能组具有上下两个能提供触觉（或是听觉）反馈的操作点。腰带执行器应该选用震动马达或者类似按摩仪使用的气泵气囊，需要控制好输出压力的比例以在佩戴舒适和警示有效间取得平衡。此外，腰带应该具有一定的可扩展性与合理的续航。对于续航部分，需要选择可靠的电池与合理的充电设备。对于扩展性部分，可以考虑添加摔倒保护模块、照明模块（防止夜间其他人撞到盲人）、自动报警模块等实用性内容。这部分可以通过在腰带上添加通用接口解决。
## 市场调研
市场调研发现，目前市面上的导盲产品主要为手杖与眼镜。手杖为传统的导盲手杖添加了诸如温度传感器、超声波测距模块等设备，而眼镜则是集成了测距模块的装有声音反馈设备的小型设备。查看网络评论发现，现有的导盲手杖有抓握不便和警示不及时等问题，而导盲眼镜主要问题则是价格过高。小组认为导盲手杖其作为手持式设备的特性决定了其使用不会方便，而眼镜作为小型化设备其对体积和质量的要求也导致其价格水涨船高。总的来说，小组认为导盲腰带有穿戴便捷，价格低廉以及测距范围大等多个优点，具有很好的市场前景与较好的技术实现性。
## 测距原理  
不论使用何种方式进行建模，腰带的测距原理都是一定的。首先，系统将会把用户正面的180°范围划分为五个扇区。若平均划分，每个扇区应当占用36°。考虑到通常我们对正面区域的测量精度要求更高，我们可以略微缩小中间三个扇区的角度来获得更精确的测量效果。  

对于每个扇区，我们还需要将其从上而下划分为两个或三个区块。考虑到视觉识别模块的检测范围，每个扇区垂直方向的角度应当是小于180°的。系统将会将这一角度平均划分为多个区块。  

对于每个区域，我们在测距时应该取区间内距离用户最近的特征点的水平欧拉距离作为该区域的障碍物距离。也就是说，只要区间内有任意一点进入了腰带的警戒范围，腰带上对应的电机就会作出反应引导用户回避障碍物。由于腰带在设计时每个扇区就只设置了2-3个执行器，其输出压力时也只能输出点状的触感而非实时将周围情况完整反馈给用户。所以上述测距方法导致的误差和数据丢失不会对腰带的主要功能产生任何影响。  
对于腰带来说，每个扇区应当对应一个且唯一一个执行器。这个执行器的角度并不需要与实际测控方向1：1对应，只要能表示出大概的方向，就可以指示障碍物相对用户的水平和垂直位置。随着距离接近，按压力度也会线性加大。  
事实上，对于每个扇区来说，其对应的唯一执行器只需要执行一个操作：输出与输入的唯一数字距离成正比关系的按压力。通过多个这样的扇区与执行器的堆叠，用户就能感知到自身面前180°范围内的障碍物位置情况。  
## 腰带模型  
## 视觉识别原理  
## 数据处理流程图  
