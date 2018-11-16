# 过渡 transition: transition-property transition-duration transition-timing-function transition-delay;

( https://developer.mozilla.org/en-US/docs/Web/CSS/transition )

## 1. transition-property: 指定过渡的属性值，比如 "transition-property:width;" 就是只指定width属性参与这个过渡。

## 2. transition-duration: 指定这个过渡的持续时间 s/ms

## 3. transition-timing-function: 指定过渡动画缓动类型，有ease | linear | ease-in | ease-out | ease-in-out | cubic-bezier() | steps() | frames() | step-start | step-end 

( https://developer.mozilla.org/en-US/docs/Web/CSS/transition-timing-function )
<img src="https://github.com/iqidan/Notes/blob/master/Images/transition-timing-function.jpg" style="width: 500px;">
	
1. linear: 线性过渡(匀速);

2. ease-in: 由慢到快;

3. ease-out: 由快到慢;

4. ease-in-out: 由慢到快在到慢;

5. cubic-bezier(x1, y1, x2, y2): 三次贝塞尔曲线动画,可以自定义动画快慢效果(最多变换三次速度) 
	先慢后块 cubic-bezier(.54,.16,.81,.31) 
	先快后慢cubic-bezier(.2,.58,.37,.79) 
	匀速 cubic-bezier(.35,.35,.57,.57) 

(
三次赛贝尔曲线介绍: https://blog.csdn.net/hsany330/article/details/73609083

赛贝尔曲线生成: http://yisibl.github.io/cubic-bezier/ 

赛贝尔曲线介绍与原理: https://baike.baidu.com/item/贝塞尔曲线/1091769?fr=aladdin
) 

6. steps(num, direction): 过渡分割成段执行 num:分段数量 direction:start(每段过渡开始时刻就执行到最终状态)|end(每个过渡结束时刻执行到最终状态)
	(https://segmentfault.com/a/1190000007042048)

7. frames(num): 貌似支持不是很好,与steps很相似（目前本机测试只有safari支持 版本 12.0 (14606.1.36.1.9)）

8. step-start: 每段过渡开始时刻就执行到最终状态, 相当于steps(1, start)

9. step-end: 每个过渡结束时刻执行到最终状态, 相当于steps(1, end)

## 4. transition-delay 延迟过渡时间 s/ms

测试代码：https://github.com/iqidan/Notes/blob/master/CSS/Codes/transition.html
