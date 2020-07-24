# world edit 基本

## 指令

## 选择
小斧头选择范围起始点
//pos1 [x,y,z]  //pos2 [x,y,z]  默认选择站立的方块
//hpos1  //hpos2  选择正在看的方块

//count grass : 数草方块的数量

//expand 10 up : 向上扩展10层
//expand 5 : 向看向的方向扩展5层
//contract 10 down : 向下缩减10层

//inset  [-hv] <amount>   各方向内缩
//outset [-hv] <amount>  各方向外扩   h v 指定水平 竖直方向

//shift <amount> [direction]  移动选择的范围，不移动方块

## 撤消
//undo  撤消
//undo 7  撤消7步
//redo  重做
//redo 7 重做7步

## 区域操作
//set fence : 范围内填充栅栏
//set sandstone,glass : 沙石 玻璃各50% 随机， 多个ID的话按个数排百分比
//replace sandstone dirt : 替换方块 沙石换为土壤
//replace dirt : 选择范围内非空替换为土壤
//walls wood : 建一道围墙，不包含顶和底
//outline wood : 建一层皮
//center wood : 设置中心的方块
//hollow 1 wood : 选区中有空洞的话，空洞留一层，其它替换为wood
//hollow 	[thickness] [block] : 包空洞
//move 	[-s] [count] [direction] [leave-id] : 移动方块，可以设置填空的方块
//stack 	[-sa] [count] [direction] : 单向延长
//line 	[-h] <block> [thickness] : 划直线
//curve 	[-h] <block> [thickness] : 划曲线


## 剪贴板
//copy -m : 复制选中方块, 并同时复制与人的位置关系
//cut [leaveBlock] : 
//flip [-p] [dir]: 镜面翻转选中方块, 默认面朝的方向  -p 以玩家为中心翻转
//paste -aso : 粘贴选中的方块 -a 不粘贴空气 -s 可以选择粘贴的区域
//rotate 	<y-axis> [x-axis] [z-axis] : 旋转
//stack 3 up : 向上复制3次选中的方块，默认面朝的方向

## 生成
//hcyl 	<block> <radius>[,<radius>] [height] : 生成竖直的空心圆柱  hcyl wood 5 8
//cyl 	[-h] <block> <radius>[,<radius>] [height] : 生成不空心圆柱
//sphere 	[-h] <block> <radius>[,<radius>,<radius>] [raised? true|false (default)] : 生成球体
//hsphere 	<block> <radius>[,<radius>,<radius>] [raised? true|false (default)] : 生成空心球体
//pyramid 	[-h] <block> <size> : 生成金字塔
//hpyramid 	<block> <size> : 生成空心金字塔

## 工具
//replacenear 	[-f] <size> <from-id> <to-id> 