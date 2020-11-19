#### 贪吃蛇demo

###### 参考两位大神的代码略加修改和注释

[掘金20 行 js 的贪吃蛇](https://juejin.im/entry/6844903481808158734)

[js开发实现简单贪吃蛇游戏（20行代码）](https://blog.csdn.net/hj7jay/article/details/51011269)

###### 增加了选择难度功能，在贪吃蛇吃到食物后会加速，游戏结束后会显示得分。



##### 选择难度

![2](https://github.com/panguohui/MarkdownPhotos/blob/master/6.png?raw=true)



##### 开始页面

![2](https://github.com/panguohui/MarkdownPhotos/blob/master/7.png?raw=true)



##### 游戏结束*（吃一个食物得一分）*



![2](https://github.com/panguohui/MarkdownPhotos/blob/master/9.png?raw=true)

![2](https://github.com/panguohui/MarkdownPhotos/blob/master/8.png?raw=true)



##### 代码

···

<!DOCTYPE html>

<html lang="en">



<head>

    <meta charset="UTF-8">

    <meta name="viewport" content="width=device-width, initial-scale=1.0">

  <title>贪吃蛇demo</title>

</head>



<body>

  <canvas id="box" width="400" height="400" style="background: black;"></canvas>



    <script>

​    //获取输入的难度

​    var rate1,

​      level = parseInt(prompt('You can choose between three difficulty levels: \n1.Easy 2.Middle 3.Hard'));

​    switch (level) {

​      case 1:

​        rate1 = 300;

​        break;

​      case 2:

​        rate1 = 150;

​        break;

​      case 3:

​        rate1 = 100;

​        break;

​    }

​    var snake = [21, 20],

​      food = 22,

​      direction = 1,

​      head,

​      box = document.querySelector('#box').getContext('2d');



​    //绘图函数

​    function draw(seat, color) {

​      box.fillStyle = color;

​      //+1具体到像素点，前两个为x和y坐标，后面两个是画出矩形的长和宽，留下1px边框

​      box.fillRect(seat % 20 * 20 + 1, ~~(seat / 20) * 20 + 1, 18, 18);

​    }



​    //获取按键

​    document.addEventListener('keydown', function (e) {

​      direction = snake[1] - snake[0] === (head = [-1, -20, 1, 20][(e || event).keyCode - 37] || direction) ? direction : head;

​    })



​    //立即执行函数

​    !function () {

​      snake.unshift(head = snake[0] + direction);

​      if (snake.indexOf(head, 1) > 0 || head < 0 || head > 399 || direction === 1 && head % 20 === 0 || direction === -1 && head % 20 === 19) {

​        return alert('Game over ! Your score is ' + (snake.length - 4) + ' .');

​      }

​      //绘制头部

​      draw(head, 'lime');

​      if (head === food) {

​        //while循环随机生成新的food，若创建了重复的则不画出来继续创建。

​        while (snake.indexOf(food = ~~(Math.random() * 400)) > 0);

​        draw(food, 'blue');

​        rate1 = rate1 - 10;

​        console.log(rate1);

​      }

​      else {

​        draw(snake.pop(), 'black');

​      }





​      //arguments.callee调用匿名函数，频率是rate1

​      setTimeout(arguments.callee, rate1);

​    }();



  </script>

</body>



</html>

···

