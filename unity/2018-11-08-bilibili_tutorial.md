# 一个很长的视频教程

[史上最全Unity3D教程](https://www.bilibili.com/video/av28779788/?p=13)   


## 界面

## 基本操作
按下滚轮拖动场景， 滑动滚轮缩放
右键+wasd  场景移动
Alt+右键  缩放

Alt+左鼠  旋转场景
右键   旋转摄像机

## 材质
Material : 用来设置shader的面板
## 天空盒
## 摄像机
*unity初识02-05*
clear flag: 对无物体区域的处理方式
culling mask: 对 game object 的layer 进行过滤 (game object都有tag和layer属性,可以用来过滤)  
projection : 投影方式, 透视还是正交
field of view: 镜头的远近, 瞄准镜的方式.
clipping planes: 渲染物体的范围
viewport rect: 视口范围,摄像机内容的显示位置 (小地图,后视镜,分屏等)
Depth: 不同镜头画面的显示优先级
*unity初识02-06* 小地图制作实践  
C-S-f : 快速定位摄像机到当前scene视点位置(其它obj其实也可以)  
设置空物体player, 摄像机作为子物体

## 渲染管线
*unity初识02-07*  
游戏->图形API->[GPU]->顶点处理->图元装配->光栅化->像素处理->缓存->显示  
*unity初识02-08*   
Occlusion Culling : 遮挡剔除
Instant Occlusion Culling: 即时遮挡剔除插件 InstantOC
在物体密集遮挡的场景才适合使用OC.  
*unity初识02-09*  
录制动画
LOD Levels of Detail: 根据模型重要程度,分配渲染资源
InstantOC中设置 LOD 距离, 模型名字必须叫 Lod_0 Lod_1 Lod_2 这种

## 照明系统
*unity初识02-10*  
Global Illumination: 全局光照 GI  
直接光- 光源发的光  
间接光
环境光
反射光

### 参考书目
<<Unity4.x>>第8章 光照烘焙技术  
<<Unity4.x>>第10章 遮挡剔除技术  
<<Unity4.x>>第12章 2-3节 渲染管线
<<3D数学基础>>第15章 图形数学

*unity初识03-01*  
复习  
*unity初识03-02*  
阴影  
无阴影  不接收阴影  双面阴影(对单面的墙)  只显示阴影
设置质量等级  Edit ->   -> Quality 
可以设置阴影距离

### 环境光
Lighting 面板中的 Scene标签中设置, Ambient --
### 反射光
所有的物体反射天空盒的光, Lighting 面板的Scene标签中, Reflection --
*unity初识03-03*  
### 间接光照  
物体接受光照后反射的光  
通过 Light 组件中 Bounce Intensity 反弹强度控制  
场景里不动的物体标记为静态(static -> lightmap static),标记为静态的物体才会产后间接光
启用lighting面板中的precomputed realtime gi, 没选auto的话就手动点build

### 实时GI 烘焙GI
实时GI只大游戏,高性能机器用. 手游用烘焙GI就可以.
烘焙GI,把光生成贴图,直接贴到物体上. 
*unity初识03-04*  
物体设置为静态
light组件 -> Baked

Lighting 面板, Baked GI勾上, build.

让动态物体感知光源, light probes 组件(光源侦测)可以通过probe收集光影信息,对运动物体进行光照插值.
场景添加light probe group -> 布置小球probe -> 烘焙收集信息 -> 动态物体mesh renderer勾选使用 light prob.
## 声音
*unity初识03-05*  
3D声音  
2D声音  
Audio Source 组件, 可以挂到其它物体上  
3D声音属性  
volume rolloff: 音量衰减方式

## Unity脚本  c# js moo
*unity脚本01-03*  
Edit -> profer  -> External Tools 设置编辑工具

[SerializeField] 私有属性在unity面板中可以查看  
private int a = 100;
[HideInInspector]  在面板中隐藏
public int b = 3;
[Range(0,100)]  // 在面板中有范围 
public int c = 4;
*unity脚本01-04*  
private void Awake(){}  
private void Start(){}  
初始化方法, Awake 先于 Start , 大小写敏感. 只运行一次
OnEnable(){} 只要可用就执行
*unity脚本01-05 and 06*  
private void FixedUpdate()  固定时间循环调用,用来计算物理操作,移动之类的,间隔不受渲染速度影响  
private void Update()  渲染帆执行, 执行间隔不固定. 适用于处理游戏逻辑. 
private void LateUpdate() 在Update() 后面执行, 比如同一帧的跟随逻辑. (跃然差个一帧的没什么 区别)  
OnBecameVisible()
OnBecameInvisible()  
OnDisable()
OnDestroy()
OnApplicationQuit()
*unity脚本01-07*  
调试方法  
查看源码 项目目录 -> Library -> ScriptAssemblies  用ILspy查看 
查看源码 项目目录 -> Library -> UnityAssemblies  用ILspy查看 
*unity脚本01-08*  
vstu2013 , vs 调试 c#

*unity脚本01-09*  
### 脚本主要的类 Component GameObject Texture......

已废弃的测试方法
```
private void OnGUI(){
    if(GUILayout.Button("按钮")){
        print("button press")
    }
}
```
```
//获取组件
this.GetComponent<MeshRenderer>().material.color = Color.red;
GetComponentInChildren
GetComponentInParent
GetComponents
this.GameObject
this.tag
this.transform
```
*unity脚本01-10*  
*unity脚本01-11*  
```
foreach(Transform child in transform){
    child.position += Vector3.up * 10.0;  // child 是每个子物体的 transform
}
position  在世界中的位置  localPosition 相对于父物体的位置
this.transform.localScale // 相对于父亲缩放比例的缩放比例
this.transform.lossyScale // 只读,自身的缩放比率, 相对于原来模型的 
```
*unity脚本01-12*  
```
this.transform.Translate(0, 0, 1); // 向自身坐标系z轴方向移动1米, 参数是x,y,z轴的移动距离  
this.transform.Translate(0, 0, 1,Space.World); // 向世界坐标系z轴方向移动1米, 参数是x,y,z轴的移动距离  
this.transform.Rotate(0, 10, 0); // 绕自身坐标系y轴旋转10度
this.transform.Rotate(0, 10, 0,Space.World); // 绕世界坐标系y轴旋转10度
this.transform.RotateAround(Vector3.zero,Vector3.up,1); // 点,轴,角度
if(GUILayout.RepeatButton("按钮")){  // 按住不松,重复执行代码
    print("button press")
}
this.transform.LookAt(); // 看向某个位置
```
*unity脚本01-13*  
```
this.transform.root // 获取根物体
this.transform.parent // 获取父物体
this.transform.SetParent(pp) // 设置父物体
this.transform.SetParent(pp, false) // 设置父物体, 第2个参数设置是否保持在世界中的位置,默认是true
this.transform.Find("子物体名称") // 查找子物体
this.transform.Find("子物体名称/孙物体") // 查找多重子物体, 基本不用这种查找,依赖物体组合结构
this.transform.GetChild(); // 根据索引查找
```
*unity脚本01-14*  
GameObject  
activeInHierarchy 在场景中是否激活,受父影响  
activeSelf 只读, 不受父影响   
```
Light light = this.gameObject.AddComponent<Light>();
light.color = Color.red;  // 等等设置属性
light.type = LightType.Point;

GameObject lightGo = new GameObject();  // 新建物体, 组件不能新建,只能添加

GameObject.Find("objName"); // 根据名字查找(不建议使用, 查找范围太大)
GameObject[] all = GameObject.FindGameObjectsWithTag("tag"); // 获取所有带此标签的物体
GameObject obj = GameObject.FindWithTag("tag"); // 获取单个物体
Object obj = GameObject.FindObjectOfType(Type type)
Object[] all = GameObject.FindObjectsOfType(Type type);
GameObject.Destroy();
```
*unity脚本02-01,02*  
*unity脚本02-03*  
Time 类   
```
float t = Time.time; // 游戏执行的时间 
float t = Time.unscaledTime; // 不受缩放影响的游戏执行的时间 
float t = Time.realtimeSinceStartup; // 不受缩放影响的游戏执行的时间 
Time.deltaTime  // 最后一帧渲染完成消耗的时间
Time.timeScale  // 时间缩放, 可以实现慢动作, 默认值是1,当设置为0时,FixedUpdate中的代码不执行
```
```
public void Update(){
    this.transform.Rotate(0,1,0); // 每帧执行, 旋转速度不稳定
    this.transform.Rotate(0,1 * Time.deltaTime,0); // 根据渲染时间执行, 旋转速度稳定
    this.transform.Rotate(0,1 * Time.unscaledDeltaTime,0); // 根据渲染时间执行, 旋转速度稳定, 不受时间缩放的影响
}
public void FixedUpdate(){
    this.transform.Rotate(0,1,0); // 固定间隔执行, 旋转速度稳定
}
```

using UnityEngine.UI; // 使用组件
*unity脚本02-06,07*  
在 Update() 中固定的间隔执行代码
```
nextTime = 0;
totalTime = 0;
private void Update(){
    if(Time.time >= nextTime){  // 第一种, 与Time.time比较
        second--;
        txtTimer.text = string.Format("{0:d2}:{1:d2}", second/60, second%60)
        nextTime = Time.time + 1;
    }
    totalTime += Time.deltaTime;
    if(totalTime > 1){ // 第二种, 累加, 这个会有更大的累加误差
        second==;
        totalTime = 0;
    }    
}

private void Timer(){
    second--;
    if(second <= 0){
        CancleInvoke("Timer");
    }
}
private void Start(){  // 第三种,使用定时方法
    InvokeRepeating("Timer", 1, 1); // (方法名, 第一次执行的时间, 间隔时间)
}
```
*unity脚本02-08*  
预制件 Prefab  
把Hierarchy中物体拖到project面板中可以作为模板  
Select : 通过预制件选择对应物体  
Revert: 恢复到预制件设置    
Apply: 物体修改应用到所有预制件物体    
*unity脚本02-09*  
动画  
录制动画 
动画视图  window->animation  
步骤 1 物体添加 animation组件 2 选择物体 3 动画视图中点击create,保存位置 4 动画面板中添加属性 (时间轴上是秒数和帧数)
*unity脚本02-10*  
代码调用动画(旧版动画方法)  
```
private void OnMouseDown(){ // 点击物体时执行, 物体需要有碰撞盒组件 
    if(doorOpen){
        anim["Door"].speed = 1; // 正播, 在Start中初始化
    }else{
        anim["Door"].speed = -1; // 倒播
        anim["Door"].time = anim["Door"].length;  // 把开始时间设置为结尾
    }
    anim.Play("Door");
    doorOpen = !doorOpen;
}
animation.Play("动画名")
Play // 直接播放
CrossFade  // 两个动画连接播放, 自动过渡
PlayQueued  // 排除播放
```
## 项目实践
*unity脚本02-11,12*  
敌人设置
沿指定路线移动  EnemyMotor
减血死亡  EnemyStatusInfo
攻击  EnemyAnimation
各种动画  EnemyAnimation

EnemyAI
EnemySpawn  生成器
*unity脚本03-03,04*  
创建几个主要类的轮廓
*unity脚本03-05*  
```
public GameObject[] enemyType; // 脚本中引用  Project 中的资源, 在面板中拖进去

实例化对象 
GameObject go = Instantiate(enemyType, point, Quaternion.identity);  // 类型, 位置,是否旋转 
```
*unity脚本03-06*  
实现 移动 旋转 按路径寻路移动
*unity脚本03-07*  
动画播放
*unity脚本03-08*  
其它功能实现
```
[RequireComponent(typeof(EnemyAnimation))]   // 引入依赖组件(非必要, 可以在面板中自动挂载依赖的组件)
```
*unity脚本03-09,10,11*  
路线,怪物生成 


## 用户输入 
*三维数学01-01*   
Input 输入 可以读取 鼠标键盘屏幕触摸和感应器  
建议在Update()中读取  
```
bool result = Input.GetMouseButton(0);  // 左键按下一直返回true  0左键  1右键  2中键
bool result = Input.GetMouseButtonDown(0);  // 左键按下只返回一次true
bool result = Input.GetKey(KeyCode.A); 
bool result = Input.GetKeyDown(KeyCode.A); 
bool result = Input.GetKeyUp(KeyCode.A); 
Input.GetKey(KeyCode.C) && Input.GetKeyDown(D)// 检测同时按下两个键
```
练习 右键瞄准镜
1 镜头接近 2 逐渐接近 3 多级别每次切换
*三维数学01-02,03*   
在update中实现
```
Mathf.Lerp(camera.fieldOfView,60,0.1f); // 由快到慢, 无限接近
```
*三维数学01-04*   
枪口火光特效等
*三维数学01-05*   
虚拟按键绑定 w s a d 等 
InputManager 帮助管理绑定  Edit -> ProjectSettings -> Input

Gravity 复位速度
Sensitivity 灵敏度

```
获取
bool result = Input.GetButton("虚拟轴名"); // 是否按下
bool result = Input.GetButton("Horizontal"); // 是否按下
bool result = Input.GetButtonDown("虚拟轴名");
bool result = Input.GetButtonUp("虚拟轴名"); 
float value = Input.GetAxis("虚拟轴名"); // 三值  -1 0 1
float value = Input.GetAxisRaw("虚拟轴名");  // 连续值
```
*三维数学01-06*   
鼠标键盘控制移动和转向 实现  
```
public float rotateSpeed = 1; // 灵敏度
private void FixedUpdate(){  // 在 Update() 中要乘上 deltaTime
    float x  = Input.GetAxis("Mouse X");
    float y  = Input.GetAxis("Mouse Y");
    x *= rotateSpeed;
    y *= rotateSpeed;
    this.transform.Rotate(-y, 0 , 0);
    this.transform.Rotate(0, x , 0, Space.World);
}
private void Update(){
    float h = Input.GetAxis("Horizontal");
    float v = Input.GetAxis("Vertical");
    
    if(h != 0 || v != 0){
        h *= moveSpeed * Time.deltaTime;
        v *= moveSpeed * Time.deltaTime;
        
        this.transform.Translate(h, 0, v);
    }
}
```
## 三维数学
*三维数学01-07*   
什么是向量  大小 方向  模长
```
Vector3 pos = this.transform.position;
Debug.DrawLine(Vector3.zero, pos); // 画线debug
pos.magnitude; // 取模长
```
标准化向量  归一化向量  单位向量
```
normal = pos.normalized; 
normal = pos / pos.magnitude;
```
*三维数学01-08*   
向量的运算  
相减  `[x1,y1,z1] - [x2, y2, z2] = [x1-x2, y1-y2, z1-z2]`  几何上就是三角形的三条边, 平移到原点

相加  
子弹向着方向移动 `bullet.Translate(direction.normalized);`
等同于 `bullet.postion += direction.normalized`
*三维数学01-09*    
向量与标题的乘除  
乘法 [x,y,z] * k = [x * k , y * k, z * k];
除法 [x,y,z] / k = [x / k , y / k, z / k];
几何意义 : 线的缩放

角的度量方式  
角度 弧度  
1度 1/360周  
1弧度  弧长等于半径时.
```
r = d * Math.PI / 180;  // 角度 -> 弧度
r = d * Mathf.Deg2Rad;
d = r / Mathf.Deg2Rad;  // 弧度 -> 角度
d = r * Mathf.Rad2Deg;
d = r * 180 / Mathf.PI;  
```
*三维数学01-10*    
三角函数  边 角 -> 边
直角三角形  角 对边 a 邻边 b 斜边 c 
正弦 sin x = a / c  余弦  cos x = b / c  正切  tan x = a / b   
Mathf.Sin(float radian)
Mathf.Cos(float radian)
Mathf.Tan(float radian)
反三角函数  边 边 -> 角
反正弦  arcsin a / c = x; 反余弦 arccos b / c = x;  反正切  arctan a / b = x;
Mathf.Asin(float radian)
Mathf.Acos(float radian)
Mathf.Atan(float radian)

transform.TransformPoint(0,0,10); // 将点从自身坐标系转换到世界坐标系

*三维数学01-11*    
*三维数学02-01*    
复习
参考书籍
<<3D数学基础>>  4,5章

*三维数学02-02,03*    
向量点乘和叉乘  
点乘 点积 内积 ●  Dot()    
[x1,y1,z1] ● [x2, y2, z2] = x1x2 + y1y2 + z1z2
几何意义  a●b = |a| * |b| * cos<a,b>  
两个单位向量 a, b  |a| == 1  |b| == 1  , a ● b = cos<a,b>
两个微量的单位向量相乘后再乘以二者夹角的余弦值  
两个向量的夹角余弦值  `float cos = Vector3.Dot(pos1.normalized, pos2.normalized)`
反余弦得出角的范围 0-180

叉乘 叉积 外积 x Cross()  
[x1,y1,z1] x [x2, y2, z2] = [y1*z2 - z1*y2, z1*x2 - x1*z2, z1*y2 - y1*z2]  
几何意义:结果为两个向量所组成面的垂直向量,模长为两向量模长乘积夹角的正弦值  
```
Vector vector = Vector3..Cross(pos1, pos2)
if(vector.y < 0){
    angle = 360 - angle;
}
```
应用: 1 创建垂直于平面的向量 2 判断两个向量的相对位置,左边还是右边  
*三维数学02-04*    
欧拉角 用三个角度来保存旋转方位,x与z沿自身坐标系旋转,y沿世界坐标系旋转  
API `Vector3 eulerAngle = this.transform.eulerAngles;`  *欧拉角没有方向和大小*   
`Vector3 eulerAngle = this.transform.localEulerAngles;`
优点  (1) 仅用3个数,占用空间小 (2) 符合人的思考方式 (3) 任意三个数都是合法的  
缺点  (1) 存在多个描述,不唯一.  0,5,0 与 0,365,0 表示同一个角位移 . (2) 万向节死锁  世界y轴与自身z重合了  
为了保证唯一性, x 限制在 -90到90之间, y 与 z 限制在 0 到 360 之间.   所以用这个,x轴转到90度就转不动了

```
this.transform.eulerAngles += new Vector3(1, 0, 0);  沿x轴转1度
this.transform.eulerAngles += new Vector3(0, 1, 0);  沿y轴转1度
this.transform.eulerAngles += new Vector3(0, 0, 1);  沿z轴转1度
```
*三维数学02-05*    
四元数 Quaternion  
在3D图形学中代表旋转,由一个三维向量(xyz)和一个标量(w)组成.  
API  `Quaternion qt = this.transform.rotation;`   
```
// 设置物体旋转角度 
Quaternion qt = new Quaternion();  
// 设置旋转轴和旋转角度
Vector3 axis = Vector3.up;
float rad = 50 * Mathf.Deg2Rad;
qt.x = Mathf.Sin(rad /2) * axis.x;
qt.y = Mathf.Sin(rad /2) * axis.y;
qt.z = Mathf.Sin(rad /2) * axis.z;
qt.w = Mathf.Cos(rad /2);
this.transform.rotation = qt;

this.transform.rotation = Quaternion.Euler(0,50,0); // 欧拉角转为四元数
```
四元数相乘表示组合旋转, 沿自身的xyz轴旋转
`this.transform.rotation *= Quaternion.Euler(1,0,0);`相当于`this.transform.rotate(1,0,0);`   
优点  避免万向节死锁  
缺点  (1) 难于使用,不方便单独修改  (2) 有不合法的值  

*三维数学02-06*    
枪口特效实现  

*三维数学02-07*    
四元数与向量相乘可以用来旋转向量   
四元数与四元数相乘,是累加旋转  
```
// 计算右前方30度10米的点
this.transform.position += new Vector3(0,0,10); // 当前正前方10米
this.transform.rotate(0,30,0 ); // 旋转30度
```
*三维数学02-08*    
计算切点坐标(玩家以圆柱论,爆炸有效判断)  玩家到炸弹的半径向量,旋转到切点的夹角即得到切点
脚本给炸弹,有炸弹才判断是否能炸到
*三维数学02-09*    
计算切点的实现  
*三维数学02-10*    
Vector3 3维向量类介绍  
*三维数学02-11*    
Vector3 移动方法  
```
speed = 0.1f
// 物体匀速移动到 (0,0,10), 可以达到
this.transform.position = Vector3.MoveTowards(fromPos, destPos, speed);
// 先快后慢, 无限接近,不能到达 
this.transform.position = Vector3.Lerp(fromPos, destPos, speed);
// 变速运动  动画调节 
public AnimationCurve curve;  // 可以在面板中编辑曲线
public speed duration; // 控制整个过程的时间 (秒数)

x += Time.deltaTime / duration;
this.transform.position = Vector3.Lerp(Vector3.zero, destPos, curve.Evaluate(x));
this.transform.position = Vector3.LerpUnclamped(Vector3.zero, destPos, curve.Evaluate(x));
```
*三维数学02-12*    
四元数 方法  
```
Quaternion.Euler(0,0,1);   //  欧拉角 -> 四元数
Vector3  euler = qt.eulerAngles;  //  四元数 -> 欧拉角

// 轴角旋转
this.transform.rotation = Quaternion.AngleAxis(50, Vector3.up); // 沿y轴转50度, 可以任意指定轴

Quaternion.LookRotation();  // z轴指向指定的位置
Transform  tf;
Vector3 target = tf.target;
Quaternion dir = Quaternion.LookRotation(target - this.transform.postion);
this.transform.rotation = dir; // 立即转向, 等同于 this.transform.LookAt(tf);
this.transform.rotation = Quaternion.Lerp(this.transform.rotation, dir, 0.1f);  // 先快后慢转向
this.transform.rotation = Quaternion.RotateTowards(this.transform.rotation, dir, 0.1f);  // 匀速转向

// 判断转动角度接近
if(Quaternion.Angle(this.transform.rotation, dir) < 1){   // 相差小于1度
    this.transform.rotation = dir;
}

// x轴注视旋转
this.transform.right = tf.position = this.transform.postion;  // 立即注视

Quaternion dir =  Quaternion.FromToRotation(Vector3.right, tf.postion - this.transform.position);
this.transform.right = dir;  // 另一种转向, 加lerp可以变速
```
identity  静态参数, 世界原始坐标

*三维数学03-01*    
曲线公式转代码  
以椭圆路线运行  
以贝塞尔曲线运行  
*三维数学03-02*    
实现用户输入wasd,角色转向角度并向前走  
*三维数学03-03*    
Unity坐标系  
World space  包含游戏场景中每个对象的位置和方向  
Local space  每个物体独立的坐标系  
Screen space  屏幕左下角为原点, x向右, y向上, z轴为到相机的距离. 单位是像素
   作用: 表示物体在屏幕中的位置  
*三维数学03-04*    
Viewport space  类似屏幕坐标, 左下为(0,0), 右上为(1,1). 没有单位,使用比例. 
  设置小地图位置时用的就是视口坐标系.  

坐标系转换  
LocalSpace -> WorldSpace  
```
transform.forward
transform.right
transform.up
transform.TransformPoint
transform.TransformDirection
transform.TransformVector
```
WorldSpace -> LocalSpace   
```
transform.InverseTransformPoint
transform.InverseTransformDirection
transform.InverseTransformVector
```
world   screen   viewport
世界坐标 屏幕坐标的转换
```
Camera.main.WorldToScreenPoint
Camera.main.WorldToViewportPoint
Camera.main.ScreenToWorldPoint
Camera.main.ViewportToWorldPoint
```
*三维数学03-05*    
实例练习,屏幕左进右出,  上进下出
*三维数学03-06*    
物理引擎   刚体  碰撞器  触发器  
rigidbody 刚体, 附加物理属性  
collider  碰撞器  
  convex 网格碰撞器时需要勾选上  
不动的物体只加碰撞器, 能动的加刚体和碰撞器.
*三维数学03-07*    
刚体  
Mass  质量  
drag  阻力  参考值 砖头 0.001   羽毛 10  
Angular drag  角阻力 旋转时的阻力  
Interpolate : 用于缓解刚体运动时的抖动  
Collision Detection: 碰撞检测模式. 快速运动物体设置  
Constraints: 刚体运动的约束.  

Use Gravity: 重力  
Is Kinematic: 运动学刚体. 勾选后不受物理引擎控制,只主动发力,不接受被撞的力.   
  
*三维数学03-08*    
碰撞产生的条件  
1 两个物体都有碰撞器组件  
2 运动的物体有刚体组件  
```
碰撞执行时
void OnCollisionEnter(Collision collOther);  // 接触的第一帧执行  
void OnCollisionStay(Collision collOther)
void OnCollisionExit(Collision collOther)

Collision 可以获取碰撞体  碰撞点  法线
```
Collision 中可以获取
*三维数学03-09*    
触发器 : 勾选了 Is trigger的碰撞器  
条件: (1)两者都有碰撞组件 (2)其中之一带有刚体 (3)其中之一勾选isTr   
```
碰撞执行时
void OnTriggerEnter(Collider collOther);  // 接触的第一帧执行  
void OnTriggerStay(Collider collOther)
void OnTriggerExit(Collider collOther)
```
触发器歪用法:  用一个大球做触发器, 范围内感知可作用的敌人. 检测太多的话性能不好。 （攻击范围不规则的可以用， 五角星攻击范围。。？？） 
*三维数学03-10*    
检测速度超快的子弹与物体的碰撞  
解决方法: 不使用物理碰撞检测, 在开始时使用射线检测.  
```
//  重载11, 这方法有很多重载
RaycastHit hit;
public LayerMask mask;
Physics.Raycast(this.transform.position, this.transform.forward, hit, 1000, mask);  // (起点, 方向, 击中点, 最大距离, 层mask)
if(...){
    targetPos = hit.point;
}else{
    // 向前 1000米的位置
}
``` 
*三维数学03-11*    
武器的策划案解读  
创建枪,单发枪和连发枪的类  
*三维数学03-12*    
人物多碰撞器添加  
*三维数学03-13*    
武器代码实现  
*三维数学03-13*    
子弹,特效实现  
```
// 读取资源
```

## 用户图形界面
*用户图形界面01-01*    
复习物理引擎
Physic Material   实现不同物理效果的材质  
Bounciness  弹力, 取值是一个范围  0 没弹力 1 弹力非常足  
Bounce Combine 设置两碰撞弹力分配  
末尾处有射线检测击中物体的说明(快速运动物体的碰撞检测，子弹等)    
```

    // 子弹类
    public class Bullet{
        public float moveSpeed = 50;
        Transform targetPos;
        public LayerMask mask;
        void Start(){
            RaycastHit hit;
            // (起点, 方向, 击中点, 最大距离, 层mask)
            bool hitted = Physics.Raycast(this.transform.position, this.transform.forward, hit, 1000, mask);  
            if(hitted){
                targetPos = hit.point;
            }else{
                // 向前 1000米的位置
                targetPos = this.transform.postion + this.transform.forward * 1000;
            }
        }

        void Update(){
            this.transform.position = Vector3.MoveTowards(this.transform.position, targetPos, Time.delta * moveSpeed);
            if((this.transform.position - targetPos).sqrMagnitude < 0.1f){
                print("接触目标点")；
                Destroy(this.gameObject);
            }

            // Trail Renderer
        }
        // 触发的第一帧执行
        void OnTriggerEnter(Collider other){

        }
        // 碰撞的第一帧执行
        void OnCollisionEnter(Collision other){

        }
    }
```
*用户图形界面01-02*    
武器代码, 枪的实现  
1 有子弹，可以发射；否则等换弹匣 2 发射时，放音效，动画， 显示火花 3 可以单发或连发  
Gun  SingleGun  AutoGun
```

    public class Gun : MonoBehaviour{
        public int ammoCapacity = 15;  // 容量
        public int currentAmmoBullets = 15; // 当前数量

        public int remainBullets = 90; // 剩余子弹数

        GunAnimation anim;
        MuzzleFlash muzzleFlash; // 火花

        pubic GameObject bulletPrefab; // 子弹预制
        public Transform firePointTf; // 开火位置

        void Start(){
            anim = GetComponent<GunAnimation>();
            muzzleFlash = GetComponnetInChildren<MuzzleFlash>();
        }
        public void Firing(){
            // 玩家发射： 枪口方向
            // 敌人发射： 玩家头部

            // 准备子弹， 看弹匣里有没有
            if(!Ready()){
                return;
            }

            // 播放
            audioSource.PlayOneShot(clip);
            anim.action.Play(anim.fireAnimation);
            Instantiate(bulletPrefab, firePointTF.position, Quaternion.LookRotation(direction));
        }
        // 准备子弹
        private bool Ready(){
            // 弹匣内没有或正在换
            if(currentAmmoBullets <= 0 || anim.action.IsPlaying(anim.updateAmmoAnimName)){
                return false;
            }

            currentAmmoBullets--;

            if(currentAmmoBullets ==0 ){
                anim.action.Play(anim.lackBulletAnimName)
            }
            return true;

        }
        // 更换弹匣
        public void UpdateAmmo(){
            if(remainBullets <=0 || currentAmmoBullets == ammoCapacity)
                return;

            // 剩余数大于容量装满， 否则装上剩余的
            currentAmmoBullets = remainBullets >= ammoCapacity ? ammoCapacity : remainBullets;
            remainBulets -= currentAmmoBullets;
            anim.action.Play(anim.updateAmmoAnimName);
        }
    }

    // 枪的动画
    public class GunAnimation:MonoBehaviour{
        // 开枪动画
        public string fireAnimName = "PlayerGun01_Fire"
        // 换弹匣动画
        public string updateAmmoAnimName = "..."
        // 缺子弹动画
        public string lackBulletAnimName = "...";

        public AnimationAction action;

        void Awake(){
            // 动画要同步拖到枪上才能找到
            action = new AnimationAction(GetComponentInChildren<Animation>());
        }
    }

    public class SingleGun : Gun{

        protected override void Start(){
            base.Start();
        }
        private void Update(){
            if(firing){
                base.Firint(base.firePointTF.forward);
            }
        }
    }

```


对于第三人称的主角移动，rigidbody.MovePosition() : 通过调整刚体的Position 来实现对角色的移动控制    
提示 1： 不直接修改刚体的position而是通过调用公共函数MovePosition() : 使运动更加平滑（使用内插值）  
提示 2： 不使用transform.position而是使用刚体的position : 前者会导致物体的Colliders重新计算相对于刚体的位置，会更加耗费性能  
[Unity3d--第三人称角色移动控制][1]  


*用户图形界面01-03*    
更换弹匣  
播放特别短的动画, 用 PlayQueued() 不用 CrossFade()  
*用户图形界面01-04*    
*用户图形界面01-05*    
子弹的实现  
玩家信息类  

```
// 单例实现玩家信息类
public class PlayerInfo:MonoBehaviour{
    public static PlayerInfo Instance{get; private set;}

    private void Awake(){
        Instance = this;
    }

    public float HP = 1000;
    public float maxHP = 1000;
    public void Damage(float amount){
        ....
    }
}
```
*用户图形界面01-06*    
完成敌人打玩家  
*用户图形界面01-07*    
子弹,特效逻辑  
*用户图形界面01-08, 09*    
继续实现  

*用户图形界面02-01*    
敌人生成器系统  
武器系统

*用户图形界面02-02*    
```  
// 解决问题, 敌人注视玩家,躺倒 
1. 修改targetPos的y值
2. Quaternion -> euler , 只取y值的旋转   this.transform.eulerAngle = new Vector3(0, euler.y, 0);
```
*用户图形界面02-03*    
HTC VIVE  
*用户图形界面02-04*    
SteamVR工具包
...
...
*用户图形界面03-03*    
中间都是 VIVE介绍  


*用户图形界面03-04*    
UGUI  
全新的布局系统  

强大的事件机制  

最佳的执行效能  

*用户图形界面03-05,06*    
Canvas 画布
所有UI组件必须放在Canvas之下
sort order : 多个画布的深度顺序
模式: 覆盖模式  摄像机模式   世界模式  
有物体在UI前显示的需求才用摄像机模式,其它主要用覆盖模式.   
世界模式一般在VR中用, 在墙面或地面上贴字之类的UI.  
*用户图形界面03-07*    
Rect Transform  
Pivot 轴心, 轴心点可以调整, 会影响控件的移动旋转缩放.  x,y是在UI中的比例  
Ancher : 锚点, 固定控件相对锚点的位置.   
*用户图形界面03-08*    
代码访问锚点
```
RectTransform rtf = this.transform as RectTransform;
RectTransform rtf = GetComponent<RectTransform>();
rtf.anchoredPosition3D; // 自身轴心点相对于锚点的位置  
rtf.anchorMin  // 设置/获取锚点
rtf.pivot
rtf.rect.width  // 获取UI宽度
rtf.rect.height  // 高度
rtf.SetSizeWithCurrentAnchors(...);  // 设置宽高
rtf.sizeDelta; // 当锚点不分开时,数值可以理解为宽高. 其实它的值是(物体大小 - 锚点间距)
```
RectTransformUtility  矩阵变换工具. UGUI 相关的一些工具方法  

*用户图形界面03-09*    
Image  
Text  

```
    
    // 修改控件属性
    Text info;
    info = GameObject.Find("Canvas/Text").GetComponent<Text>();
    info.text = "这里是要显示的文字";
```
*用户图形界面03-10*    
Button  录制button动画  
Toggle  复选框  
其它一些控件等  

*用户图形界面03-11*    
2048界面实现  
开始做项目前,先做分辨率设置. 设置缩放设置 Cavas 中设置   
*用户图形界面03-12*    
2048接着做
*用户图形界面04-01*    
2048接着做
Sprite Packer : 精灵打包  , 设置同一个Packing Tag  
*用户图形界面04-02*    
实现  
加载精灵图片, 静态资源管理类  
*用户图形界面04-03*    
继续实现  
字典存储资源   
Start() 与 Awake() 加载资源, Awake() 更早  
*用户图形界面04-03*    
实现  
生成数字  
*用户图形界面04-04*    
继续实现  
c#  可空值类型  int? a = null;   取值  a.Value;
*用户图形界面04-05*    
调用GameCore中生成的数字,更新界面  
*用户图形界面04-06*    
用户输入处理  
UGUI事件  UI组件上绑定事件处理方法  
1 编辑器绑定  
2 AddListener  只能注册在编辑器中能显示的事件 
```
this.transform.Find("Button").GetComponent<Button>();
btn.onClick.AddLIstener(Fun1);
```
*用户图形界面04-06,07*    
3 实现接口  可以注册所有接口定义的事件
4 自定义框架  
*用户图形界面04-08*    
实现接口方法注册事件  
```
// 组件挂到相关有图片和文字的组件上
class MyClass:MonoBehaviour,IPointerClickHandler{
    
    public void OnPointerClick(PointerEventData eventData){
        ....
    }
    
    public void OnDrag(PointerEventData eventData){ // 通用的拖动
        // 将屏幕坐标转换为物体的世界坐标
        RectTransform parentRTF = this.transform.parent as RectTransform;
        Vector3 worldPos;
        // 参数 (父物体的变换组件,屏幕坐标,摄像机,out 世界坐标)
        RectTransformUtility.ScreenPointToWorldPointInRectangle(parentRTF, eventData.position, eventData.pressEventCamera, out worldPos);
        this.transform.position = worldPos;
    }
}
```
*用户图形界面04-09*  
实现拖动时图片与光标相对位置不变

*用户图形界面04-10*  
2048滑动实现  
*用户图形界面04-11*  
iTween 动画库  
```
iTween.MoveTo(gameObject, targetPos, time);
iTween.MoveTo(gameObject, iTween.Hash(
    "position", targetPos,
    "speed", moveSpeed,
    "easetype", type
));
```
DoTween 动画库,同类竞品,性能不如自己手写    

*用户图形界面04-11*  
2048加点特效,生成数字时由小变大  

## 关卡创建
*关卡创建01*  


## 重新加载当前关卡
```

    using UnityEngine.SceneManagement;

    SceneManager.LoadScene(SceneManager.GetActiveScene().buildIndex);
    // 或者
    SceneManager.LoadScene(SceneManager.GetActiveScene().name);
```

## 其它

### 调用摄像机
```

    if (Application.HasUserAuthorization(UserAuthorization.WebCam)){
        WebCamDevice[] devices = WebCamTexture.devices;
        for (int i = 0; i < devices.Length; i++){
            if (devices[i].isFrontFacing){  // 选用前面的摄像头
                deviceName = devices[i].name;
                break;
            }
        }
        tex = new WebCamTexture(deviceName, 1280, 720, 3);
        tex.Play();
    }
    savePic(){  // 保存图片
        Texture2D t = new Texture2D(1280, 720);
        t.SetPixels(tex.GetPixels());
        t.Apply();
        picBytes = t.EncodeToPNG();
        File.WriteAllBytes(Application.persistentDataPath + "/" + Time.time + ".png", byt);
    }
```
### 物体显示图片
直接Image类型的图片拖上去
### 获得物体长宽高
terrainWidth = gameObject.collider.bounds.size.x;

### 动态加载图片作为贴图
```
    
    using UnityEditor;
    Texture2D t = (Texture2D)AssetDatabase.LoadAssetAtPath("Assets/Textures/texture.jpg", typeof(Texture2D));
    GameObject.Find("Game1BG").GetComponent().mainTexture = txt2d;
```
### 加载声音和播放
```

    AudioClip audioClip = Resources.Load<AudioClip>("Audio/" + path);
    int audioID = EazySoundManager.PlayMusic(audioClip, 1f, false, false);
    audio = EazySoundManager.GetAudio(audioID);
```
### 在editor和设备上都能退出
```

    #if UNITY_EDITOR
        UnityEditor.EditorApplication.isPlaying = false;
        Debug.Log ("编辑状态游戏退出");
    #else
        Application.Quit();
        Debug.Log ("游戏退出");
    #endif
```


refs:  

[1]: https://blog.csdn.net/Ming991301630/article/details/78077093



































