# 409737227_test

```javascript=
var colors = "ccd5ae-e9edc9-fefae0-faedcd-d4a373".split("-").map(a=>"#"+a)
var colors2 = "d8e2dc-ffe5d9-ffcad4-f4acb7-9d8189".split("-").map(a=>"#"+a)
class ball_class{///設定一個物件類別
  constructor(args){//描述物件的初始值
      this.p=args.p||{x:random(width),y:random(height)}//位置
      this.r=random(50,100)//直徑
      this.color=random(colors)//顏色
      this.v=args.v||{x:random(-3,3),y:random(-3,3)}//速度
      this.a =args.a||{x:0,y:0.5}//加速度
      this.mode = random(["happy","bad"])//亂數產生心情 好或不好

     }
draw(){
  push()
  translate(this.p.x,this.p.y)//把原點(0,0)放到(this.p.x,this.p.y)上
  fill(this.color)//球變成紅色
ellipse(0,0,this.r)
if(this.mode=="happy"){
  //劃一個全部的圓
  fill(255)//白色
arc(0,0,this.r/2,this.r/2,0,2*PI)//嘴巴
fill(0)//黑色
arc(0,0,this.r/4,this.r/4,0,2*PI)//眼睛
}
else{
  //畫半圓
fill(255)
arc(0,0,this.r/2,this.r/2,0,PI)
fill(0)
arc(0,0,this.r/4,this.r/4,0,PI)
}
pop()
}
update(){
  //this.v.x = this.v.x*0.998
  //this.v.y = this.v.y*0.998
  //this.p.x = this.p.x+this.v.x//把目前x軸位置加上x軸方向的速率==>新的x軸位置
  //this.p.y = this.p.y+this.v.y//把目前y軸位置加上y軸方向的速率==>新的y軸位置
 // this.v.x = this.v.x+this.a.x//a.y為一個往下的加速度
//this.v.y = this.v.y+this.a.y//v.y代表往下的速率
//碰到下邊

//依照mode值的設定，決定要上下移動還是發散移動
  if(this.mode=="happy"){
    this.p.y =this.p.y + sin(frameCount/8)*5 //(framecount/10)微動的頻率，*5為振福
  }
  else
  {
    this.p.x = this.p.x+this.v.x
    this.p.y = this.p.y+this.v.y
  }
  if((this.p.y+(this.r/2))>height){
    this.p.y = height-this.r/2
    this.v.y = -this.v.y////因為往下跳時 this.v.y為正，當碰到視窗下邊v.y要為負值，經由運算，新的位置就會往上移動回彈
//捧到上邊
  }
  if((this.p.y-(this.r/2))<0){
    this.p.y = this.r/2
    this.v.y = -this.v.y
  }
  //碰到右邊
  if((this.p.x+(this.r/2))>width){
    this.v.x=-this.v.x
    this.p.x = width-this.r/2
  }
  //碰到左邊
  if((this.p.x-(this.r/2))<0){
    this.v.x=-this.v.x
  }
}

}
var ball
var balls =[]//物件陣列,一群相同物件的資料都放在此陣列中
//var  x =50
//var  y =50
//var  r  =100
function setup() {//如果圖片不易動的話，可以在 setup()產生物件
createCanvas(windowWidth, windowHeight);
//circle(50,50,100)//純粹產生一個正圓
///x =50
//y =50
//r  =100
//ball ={  ///宣告物件基本資料
//p:{x:50,y:50},  //p代表位置
//r:100,//r代表直徑
//color: color(252,68,68),//球變成紅色
//v:{x:0,y:1} ///移動的速率
//}
for(i=0;i<60;i=i+1){
  if(i<30){//中間的圓
  ball = new ball_class({
    p:{x:width/2,y:height/2},
    color:random(colors2)
  })///產生一個物件為ball_class類別的物件
}
  else{
    ball = new ball_class({
      //v:{x:random(-0.5,0.5),y:random(-0.5,0.5)}
    })
  }
  balls.push(ball)
}
}

function draw() {//如果圖片不移動或是移動的話，可以在 draw()產生物件
background(220);//不會暫留軌跡，不執行此指令則會暫留軌跡
//ellipse(50,50,100)//在50,50產生一個直徑100的圓，可以產生橢圓
//ellipse(x,y,r)
noStroke()
for(j=0;j<balls.length;j++){// j=j+1 ==>j++
  ball =balls[j]
//fill(ball.color)//球變成紅色
//ellipse(ball.p.x,ball.p.y,ball.r)
ball.draw()
//ball.p.x =ball.p.x+ball.v.x//把目前x軸位置加上x軸方向的速率==>新的x軸位置
//ball.p.y =ball.p.y+ball.v.y//把目前y軸位置加上y軸方向的速率==>新的y軸位置
ball.update()
}
}

```
