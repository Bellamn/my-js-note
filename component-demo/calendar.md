# 日历组件demo
```html
<div id="jsContainer">
    <table class="calendar">
        <thead>
            <tr><th class="pre"><</th><th colspan="5" class="date">2020.01</th><th class="next">></th></tr>
            <tr><th>一</th><th>二</th><th>三</th><th>四</th><th>五</th><th>六</th><th>日</th></tr>
        </thead>
        <tbody>
            <tr><td></td><td></td><td>1</td><td>2</td><td>3</td><td>4</td><td>5</td></tr>
            <tr><td>6</td><td>7</td><td>8</td><td class="current">9</td><td>10</td><td>11</td><td>12</td></tr>
            <tr><td>13</td><td>14</td><td>15</td><td>16</td><td>17</td><td>18</td><td>19</td></tr>
            <tr><td>20</td><td>21</td><td>22</td><td>23</td><td>24</td><td>25</td><td>26</td></tr>
            <tr><td>27</td><td>28</td><td>29</td><td>30</td><td>31</td><td></td><td></td></tr>
        </tbody>
    </table>
</div>
```


```css
table.calendar {
    font-size: 14px;
    border-collapse: collapse;
    width: 100%;
    table-layout: fixed;
}

table.calendar th{
    background: #f5f5f5;
    color: #999;
}
table.calendar th,
table.calendar td {
    border: 1px solid #e1e1e1;
    padding: 0;
    height: 32px;
    line-height: 32px;
    text-align: center;
}

table.calendar td.current{
    background: #1890ff;
    color: #fff;
}

table.calendar th.pre,
table.calendar th.next{
    color: #1890ff;
    cursor: pointer;
}
table.calendar th.date{
    color: #000;
}
```

```javascript
function Calendar(container, year, month) {
    this.year = year;
    this.month = month;
    this.html = html;
    this.el = null; //TODO: 创建分页组件根节点
    if (!el) return;
    this.el.className = 'calendar';
    this.el.innerHTML = this.html();
    container.appendChild(this.el);

    this.el.addEventListener('click', event => {
        var el = event.target;
        var isPre = el.classList.contains('pre');
        var isNext = el.classList.contains('next');
        if (!isPre && !isNext) return;
        if (isPre) {
            //TODO: 更新this.month和this.year
        } else {
            //TODO: 更新this.month和this.year
        }
        this.el.innerHTML = this.html();
    });

    function html() {
        var date = new Date();
        var year = +this.year || 0;
        var month = (+this.month || 0) - 1;
        var day = date.getDate();
        //TODO: 生成组件的内部html字符串
        return '';
    }
}
```