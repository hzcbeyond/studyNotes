###颜色、样式和阴影###
1. fillStyle:                       设置或返回用于填充绘画的颜色、渐变或模式
2. strokeStyle:                     设置或返回用于笔触的颜色、渐变或模式
3. shadowColor:                     设置或返回用于阴影的颜色
4. shadowBlur:                      设置或返回用于阴影的模糊级别
5. shadowOffsetX:                   设置或返回阴影距形状的水平距离
6. shadowOffsetY:                   设置或返回阴影距形状的垂直距离

---

### 方法 ###
1. createLinearGradient();          创建线性渐变（用在画布内容上);
2. createPattern()                  在指定的方向上重复指定的元素;
3. createRadialGradient()           创建放射状/环形的渐变（用在画布内容上）;
4. addColorStop()                   规定渐变对象中的颜色和停止位置


### 线条样式 ### 
1. lineCap                          设置或返回线条的结束端点样式
2. lineJoin	                        设置或返回两条线相交时，所创建的拐角类型
3. lineWidth                        设置或返回当前的线条宽度
4. miterLimit                       设置或返回最大斜接长度

### 矩形 ### 
1. rect()                           创建矩形
2. fillRect()                       绘制“被填充”的矩形
3. strokeRect()                     绘制矩形（无填充）
4. clearRect()                      在给定的矩形内清除指定的像素


### 路径 ### 

1. fill()                           填充当前绘图（路径）
2. stroke()                         绘制已定义的路径
3. beginPath()                      起始一条路径，或重置当前路径
4. moveTo()                         把路径移动到画布中的指定点，不创建线条
5. closePath()                      创建从当前点回到起始点的路径
6. lineTo()                         添加一个新点，然后在画布中创建从该点到最后指定点的线条
7. clip()                           从原始画布剪切任意形状和尺寸的区域
8. quadraticCurveTo()               创建二次贝塞尔曲线
9. bezierCurveTo()                  创建三次方贝塞尔曲线
10. arc()                           创建弧/曲线（用于创建圆形或部分圆）
11. arcTo()                         创建两切线之间的弧/曲线
12. isPointInPath()                 如果指定的点位于当前路径中，则返回 true，否则返回 false

### 转换 ###

1. scale()                          缩放当前绘图至更大或更小
2. rotate()                         旋转当前绘图
3. translate()                      重新映射画布上的 (0,0) 位置
4. transform()                      替换绘图的当前转换矩阵
5. setTransform()                   将当前转换重置为单位矩阵。然后运行 transform()

### 文本 ###
1. font                             设置或返回文本内容的当前字体属性
2. textAlign                        设置或返回文本内容的当前对齐方式
3. measureText()                    返回包含指定文本宽度的对象


### 图像绘制 ### 
1. drawImage()                      向画布上绘制图像、画布或视频 

### 其他方法 ### 
1. save()	                        保存当前环境的状态
2. restore()	                    返回之前保存过的路径状态和属性
3. createEvent()	                
4. getContext()	
5. toDataURL()	