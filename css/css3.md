# css3

## 3D变换

  perspective: 模拟人眼距离被观察物体的距离; 默认无,也就是说在一个2d平面中; 建议值800px;

  perspective-origin: 观察原点(从哪个位置看), 默认为物体的正中心

  transform-origin: 变形原点(元素绕哪个点转), 默认为左上角

  transform-style: preserve-3d 给元素添加3d观察效果

  backface-visibility: 元素背面可见性, 默认可见, 设为 hidden 隐藏

  z轴正方向为屏幕到人眼的方向, 元素进行3d变换时坐标轴也会跟随进行变换, 也就是说坐标轴相对于元素本身是不变的