<!DOCTYPE html>
<html lang="zh-CN">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no">
<title>数值积分交互演示</title>
<style>
  body { 
    font-family: -apple-system, BlinkMacSystemFont, "Segoe UI", Roboto, Helvetica, Arial, sans-serif; 
    background-color: #f4f6f8; 
    color: #333; 
    margin: 0; 
    padding: 20px; 
    display: flex; 
    flex-direction: column; 
    align-items: center; 
  }
  .container { 
    background: white; 
    padding: 30px; 
    border-radius: 16px; 
    box-shadow: 0 10px 30px rgba(0,0,0,0.08); 
    max-width: 900px; 
    width: 100%; 
    box-sizing: border-box;
  }
  h2 { margin-top: 0; color: #2c3e50; text-align: center; font-size: 28px;}
  .controls { 
    display: flex; 
    flex-wrap: wrap; 
    gap: 30px; 
    margin-bottom: 25px; 
    align-items: center; 
    justify-content: center; 
    background: #f8f9fa;
    padding: 20px;
    border-radius: 12px;
  }
  .control-group { display: flex; flex-direction: column; gap: 10px; width: 100%; max-width: 350px;}
  label { font-size: 18px; font-weight: 600; color: #34495e;}
  select { 
    padding: 12px; 
    font-size: 18px; 
    border-radius: 10px; 
    border: 2px solid #bdc3c7; 
    background: white;
    outline: none;
  }
  /* 放大滑块，方便 iPad 触控 */
  input[type="range"] { 
    width: 100%; 
    height: 8px; 
    border-radius: 5px;   
    outline: none; 
  }
  input[type="range"]::-webkit-slider-thumb {
    appearance: none;
    width: 28px;
    height: 28px;
    border-radius: 50%;
    background: #3498db;
    cursor: pointer;
  }
  canvas { 
    width: 100%; 
    height: auto; 
    background: #ffffff; 
    border: 2px solid #ecf0f1; 
    border-radius: 12px; 
  }
  .stats { 
    display: flex; 
    justify-content: space-between; 
    margin-top: 25px; 
    font-size: 22px; 
    font-weight: bold; 
    gap: 20px;
  }
  .stat-box { 
    background: #eef2f5; 
    padding: 20px; 
    border-radius: 12px; 
    flex: 1; 
    text-align: center; 
  }
  .highlight { font-size: 28px; display: block; margin-top: 5px; }
</style>
</head>
<body>

<div class="container">
  <h2>📐 数值积分原理演示</h2>
  
  <div class="controls">
    <div class="control-group">
      <label for="method">选择近似方法:</label>
      <select id="method">
        <option value="midpoint">中点法则 (矩形) - Midpoint</option>
        <option value="trapezoidal" selected>梯形法则 (直线) - Trapezoidal</option>
        <option value="simpson">辛普森法则 (抛物线) - Simpson's</option>
      </select>
    </div>
    
    <div class="control-group">
      <label for="n-slider">切片数量 n = <span id="n-val" style="color:#e74c3c;">4</span></label>
      <input type="range" id="n-slider" min="2" max="40" step="2" value="4">
    </div>
  </div>

  <canvas id="canvas" width="1600" height="800"></canvas>
  
  <div class="stats">
    <div class="stat-box" style="color: #7f8c8d;">
      精确面积 (True Area)
      <span class="highlight" id="true-area">...</span>
    </div>
    <div class="stat-box" style="color: #e67e22;" id="approx-box">
      估算面积 (Approximate)
      <span class="highlight" id="approx-area">...</span>
    </div>
  </div>
</div>

<script>
  // 获取 DOM 元素
  const canvas = document.getElementById('canvas');
  const ctx = canvas.getContext('2d');
  const methodSelect = document.getElementById('method');
  const nSlider = document.getElementById('n-slider');
  const nVal = document.getElementById('n-val');
  const approxAreaSpan = document.getElementById('approx-area');
  const trueAreaSpan = document.getElementById('true-area');
  const approxBox = document.getElementById('approx-box');

  // 数学设定: 积分函数 f(x) = 2 + sin(x) + cos(0.5x)
  const f = (x) => 2 + Math.sin(x) + Math.cos(0.5 * x);
  const a = 0;
  const b = 10;
  // 解析解真实面积
  const trueArea = 21 - Math.cos(10) + 2 * Math.sin(5); 
  trueAreaSpan.innerText = trueArea.toFixed(4);

  // Canvas 坐标映射设定
  const padding = 80;
  const plotW = canvas.width - padding * 2;
  const plotH = canvas.height - padding * 2;
  const yMax = 4.5; 

  function mapX(x) { return padding + (x - a) / (b - a) * plotW; }
  function mapY(y) { return canvas.height - padding - (y / yMax) * plotH; }

  // 绘制坐标轴
  function drawAxes() {
    ctx.strokeStyle = '#bdc3c7';
    ctx.lineWidth = 3;
    ctx.beginPath();
    ctx.moveTo(mapX(a) - 20, mapY(0)); ctx.lineTo(mapX(b) + 20, mapY(0)); // X 轴
    ctx.moveTo(mapX(0), mapY(0) + 20); ctx.lineTo(mapX(0), mapY(yMax)); // Y 轴
    ctx.stroke();
  }

  // 绘制真实的函数曲线
  function drawTrueCurve() {
    ctx.strokeStyle = 'rgba(52, 152, 219, 0.4)'; // 浅蓝色粗线
    ctx.lineWidth = 12;
    ctx.lineJoin = 'round';
    ctx.beginPath();
    for(let x = a; x <= b; x += 0.02) {
      if(x === a) ctx.moveTo(mapX(x), mapY(f(x)));
      else ctx.lineTo(mapX(x), mapY(f(x)));
    }
    ctx.stroke();
  }

  // 核心绘图与计算逻辑
  function draw() {
    ctx.clearRect(0, 0, canvas.width, canvas.height);
    drawAxes();
    drawTrueCurve();

    const method = methodSelect.value;
    const n = parseInt(nSlider.value);
    const dx = (b - a) / n;
    let approxArea = 0;

    ctx.lineWidth = 4;

    if (method === 'midpoint') {
      approxBox.style.color = '#27ae60'; // 绿色主题
      ctx.strokeStyle = '#27ae60';
      ctx.fillStyle = 'rgba(46, 204, 113, 0.3)';

      for (let i = 0; i < n; i++) {
        const x0 = a + i * dx;
        const x1 = a + (i + 1) * dx;
        const xMid = (x0 + x1) / 2;
        const y = f(xMid);
        approxArea += y * dx;

        ctx.beginPath();
        ctx.rect(mapX(x0), mapY(y), mapX(x1) - mapX(x0), mapY(0) - mapY(y));
        ctx.fill();
        ctx.stroke();
      }
    } 
    else if (method === 'trapezoidal') {
      approxBox.style.color = '#e67e22'; // 橙色主题
      ctx.strokeStyle = '#d35400';
      ctx.fillStyle = 'rgba(230, 126, 34, 0.3)';

      for (let i = 0; i < n; i++) {
        const x0 = a + i * dx;
        const x1 = a + (i + 1) * dx;
        const y0 = f(x0);
        const y1 = f(x1);
        approxArea += 0.5 * (y0 + y1) * dx;

        ctx.beginPath();
        ctx.moveTo(mapX(x0), mapY(0));
        ctx.lineTo(mapX(x0), mapY(y0));
        ctx.lineTo(mapX(x1), mapY(y1));
        ctx.lineTo(mapX(x1), mapY(0));
        ctx.closePath();
        ctx.fill();
        ctx.stroke();
      }
    } 
    else if (method === 'simpson') {
      approxBox.style.color = '#8e44ad'; // 紫色主题
      
      for (let i = 0; i < n; i += 2) {
        const x0 = a + i * dx;
        const x1 = a + (i + 1) * dx;
        const x2 = a + (i + 2) * dx;
        const y0 = f(x0);
        const y1 = f(x1);
        const y2 = f(x2);
        
        approxArea += (dx / 3) * (y0 + 4 * y1 + y2);

        // 计算用于 Canvas 二次贝塞尔曲线的控制点 Cy
        const cY = 2 * y1 - 0.5 * (y0 + y2);

        ctx.beginPath();
        ctx.moveTo(mapX(x0), mapY(0));
        ctx.lineTo(mapX(x0), mapY(y0));
        ctx.quadraticCurveTo(mapX(x1), mapY(cY), mapX(x2), mapY(y2));
        ctx.lineTo(mapX(x2), mapY(0));
        ctx.closePath();
        
        if ((i/2) % 2 === 0) {
          ctx.fillStyle = 'rgba(155, 89, 182, 0.4)';
          ctx.strokeStyle = '#8e44ad';
        } else {
          ctx.fillStyle = 'rgba(142, 68, 173, 0.6)';
          ctx.strokeStyle = '#732d91';
        }
        
        ctx.fill();
        ctx.stroke();
      }
    }

    approxAreaSpan.innerText = approxArea.toFixed(4);
  }

  // 绑定交互事件
  methodSelect.addEventListener('change', draw);
  nSlider.addEventListener('input', (e) => {
    nVal.innerText = e.target.value;
    draw();
  });

  // 初始绘制
  draw();
</script>
</body>
</html>
