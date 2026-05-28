<!DOCTYPE html>  
<html lang="zh-CN">  
<head>  
    <meta charset="UTF-8">  
    <meta name="viewport" content="width=device-width, initial-scale=1.0, user-scalable=no">  
    <title>3D摇奖机 近100期数据版</title>  
    <style>  
        *{margin:0;padding:0;box-sizing:border-box;}  
        body{background:#121826;color:#fff;font-family:-apple-system,BlinkMacSystemFont,"PingFang SC";padding:20px;}  
        .title{font-size:22px;text-align:center;color:#ffd33d;margin-bottom:25px;}  
        .roll-wrap{display:flex;justify-content:center;gap:10px;margin:30px 0;}  
        .num-box{width:70px;height:100px;border:2px solid #ffd33d;border-radius:8px;  
            background:#1e293b;overflow:hidden;position:relative;}  
        .num-list{position:absolute;width:100%;text-align:center;transition:transform 0.08s linear;}  
        .num-list div{height:100px;line-height:100px;font-size:55px;font-weight:bold;color:#fff;}  
        .btn-group{display:flex;justify-content:center;gap:15px;margin:20px 0;}  
        .btn{padding:10px 22px;font-size:17px;border-radius:6px;border:none;  
            background:#ffd33d;color:#000;font-weight:600;}  
        .stat{background:#1e293b;padding:15px;border-radius:8px;margin-top:20px;font-size:14px;line-height:1.6;}  
        .hot{color:#ff5555;}  
        .cold{color:#4cd964;}  
    </style>  
</head>  
<body>  
    <div class="title">福彩3D 模拟摇奖机</div>  
  
    <div class="roll-wrap">  
        <div class="num-box">  
            <div class="num-list" id="n0">  
                <div>0</div><div>1</div><div>2</div><div>3</div><div>4</div>  
                <div>5</div><div>6</div><div>7</div><div>8</div><div>9</div>  
            </div>  
        </div>  
        <div class="num-box">  
            <div class="num-list" id="n1">  
                <div>0</div><div>1</div><div>2</div><div>3</div><div>4</div>  
                <div>5</div><div>6</div><div>7</div><div>8</div><div>9</div>  
            </div>  
        </div>  
        <div class="num-box">  
            <div class="num-list" id="n2">  
                <div>0</div><div>1</div><div>2</div><div>3</div><div>4</div>  
                <div>5</div><div>6</div><div>7</div><div>8</div><div>9</div>  
            </div>  
        </div>  
    </div>  
  
    <div class="btn-group">  
        <button class="btn" id="start">开始摇奖</button>  
        <button class="btn" id="stop">停止开奖</button>  
    </div>  
  
    <div class="stat">  
        <p>📊 参考近100期开奖频次（0-9）</p>  
        <p>百位：[12,15,10,8,11,9,13,7,6,9] <span class="hot">热号:1、6</span> <span class="cold">冷号:7、8</span></p>  
        <p>十位：[10,11,14,7,12,8,10,9,15,4] <span class="hot">热号:2、8</span> <span class="cold">冷号:9</span></p>  
        <p>个位：[9,13,11,10,7,12,8,14,10,6] <span class="hot">热号:1、7</span> <span class="cold">冷号:4</span></p>  
        <p>💡 号码按历史冷热概率生成，非纯随机</p>  
    </div>  
  
<script>  
// 近100期频次：百位、十位、个位  
const weight = [  
    [12,15,10,8,11,9,13,7,6,9],  
    [10,11,14,7,12,8,10,9,15,4],  
    [9,13,11,10,7,12,8,14,10,6]  
];  
let timer = [null,null,null];  
let isRoll = false;  
const dom = [document.getElementById('n0'),document.getElementById('n1'),document.getElementById('n2')];  
  
// 加权随机选号  
function getNum(pos){  
    let pool = [];  
    for(let i=0;i<10;i++){  
        for(let j=0;j<weight[pos][i];j++) pool.push(i);  
    }  
    return pool[Math.floor(Math.random()*pool.length)];  
}  
  
// 开始滚动  
document.getElementById('start').addEventListener('click',()=>{  
    if(isRoll) return;  
    isRoll = true;  
    for(let i=0;i<3;i++){  
        let y = 0;  
        timer[i] = setInterval(()=>{  
            y += 100;  
            dom[i].style.transform = `translateY(-${y}px)`;  
        },70);  
    }  
});  
  
// 停止定格  
document.getElementById('stop').addEventListener('click',()=>{  
    if(!isRoll) return;  
    isRoll = false;  
    for(let i=0;i<3;i++){  
        clearInterval(timer[i]);  
        let num = getNum(i);  
        dom[i].style.transform = `translateY(-${num*100}px)`;  
    }  
});  
</script>  
</body>  
</html>  
