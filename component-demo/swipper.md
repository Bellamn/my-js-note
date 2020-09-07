# 简易swipper
```html
<!-- 视图层 -->
<div class="swiper">
    <!-- 容器 -->
    <div class="swiper-container">
        <!-- 滑块 -->
        <div class="swiper-item" style="background: #000">1</div>
        <div class="swiper-item" style="background: #4269eb">2</div>
        <div class="swiper-item" style="background: #247902">3</div>
    </div>
</div>

```
```css
.swiper {
    position: relative;
	width: 300px;
	
    /* 下面是为了让大家看的更清楚，加的修饰 */
    padding: 30px 0;
    margin: 0 auto;
    background: #FFB973;
}
.swiper .swiper-container {
    position: relative;
    /* 为啥要设置-300px呢，因为我想让他默认在第二个滑块的位置，一会会给大家演示 */
    left: -300px;
    /* 让容器尽可能的宽，这样才能容纳更多的滑块 */
    width: 10000%;
    /* 让内部滑块可以排成一行 */
    display: flex;

    /* 下面是为了让大家看的更清楚，加的修饰 */
    background: red;
    padding: 15px 0;
}
.swiper .swiper-container .swiper-item {
    /* 宽度设置1%会按照外层视图的宽度来铺满 */
    width: 1%;
    height: 300px;
    background: #eee;

    /* 下面是为了让大家看的更清楚，加的修饰 */
    text-align: center;
    font-size: 40px;
    color: #fff;
}
.swiper .swiper-container, .move {
    transition: left 0.2s ease-in-out;
} 
```
```javascript
// 首先获取视图层元素
const swiperEl = document.querySelector('.swiper');
// 在视图层里边查找容器元素
const containerEl = swiperEl.querySelector('.swiper-container');
// 获取到所有的滑块元素
const itemEls = containerEl.querySelectorAll('.swiper-item');
// 获取到滑块的宽度
const itemWidth = itemEls[0].offsetWidth;
let index = 0;
let state = 0;  		// 鼠标默认状态
let startEvent = null;
let oldEvent = null;    // 用来记录鼠标上次的位置
// 获取容器的初始left值
//let left = containerEl.offsetLeft;
let left = 0 - itemWidth * index;
// 设置容器的初始位置
containerEl.style.left = left + 'px';
containerEl.addEventListener('mousedown', (event) => {
    state = 1;  // 设置为1表示按下了鼠标
    startEvent = oldEvent = event;   // 当鼠标按下时候记录初始位置
    console.log('鼠标按下了');
});

containerEl.addEventListener('mousemove', (event) => {
    if (state != 1) return; // 只有当state == 1时候才允许执行该事件

    // 用当前鼠标的位置来和上次鼠标的位置作比较
    // 如果当前鼠标的pageX小于上次鼠标的pageX，那就表示鼠标在向左拖动，就需要把容器left值减去鼠标移动的距离
    if (event.pageX < oldEvent.pageX) {
        left -= oldEvent.pageX - event.pageX;
    }
    else {
        left += event.pageX - oldEvent.pageX;
    }
    // 完事之后记得把当前鼠标的位置赋值给oldEvent
    oldEvent = event;
    // 最后再把left赋值给容器
    containerEl.style.left = left + 'px';
    console.log('鼠标移动了');
});

containerEl.addEventListener('mouseup', (event) => {
    state = 0;  // 恢复默认状态
    // 鼠标抬起时候，和按下的坐标作比对，用来判断是向左滑动还是向右滑动
    // 向左滑动那么就是要显示下一个滑块，所以index要加1
    if (event.pageX < startEvent.pageX) {
        index ++;
    }
    else {
        index --;
    }
    if (index < 0) {
        index = 0;
    }
    else if (index > itemEls.length - 1) {
        index = itemEls.length - 1;
    }
    // 追加一个move样式
    containerEl.className += ' move';
    // 当过度动画结束后，一定要把这个类给移除掉
    containerEl.addEventListener('transitionend', () => {
        // 正则替换 \s+ 表示一个或多个空白字符
        containerEl.className = containerEl.className.replace(/\s+move/, '');
    })
    left = 0 - itemWidth * index;
    containerEl.style.left = left + 'px';
    console.log('鼠标抬起了');
});

```
