<!doctype html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>Document</title>
</head>
<body>
  <div class="axis">
    <div class="item"></div>
    <div class="item"></div>
    <div class="item"></div>
    <div class="item"></div>
    <div class="item"></div>
    <div class="item"></div>
  </div>
  <style>
    body {
      perspective: 1000px;
    }
    .axis {
      width: 1px;
      height: 300px;
      margin: 0 auto;
      position: relative;
      animation: rotate 12s linear infinite;
      transform-style: preserve-3d;
      transform: translateZ(0)
    }
    
    .item {transform-origin: 50% 50% 0px; position: absolute; left: -50px; top: 0; width: 100px; height: 150px; border-radius: 5px; overflow: hidden}
    :root {
      --zIndex: 200px;
      --opacity: 0.8;
    }
    .item:nth-child(1) {background: rgba(0, 153, 51, var(--opacity)); transform: rotateY(0deg) translate3d(0, 50%, var(--zIndex))}
    .item:nth-child(2) {background: rgba(0, 204, 204, var(--opacity)); transform: rotateY(60deg) translate3d(0, 50%, var(--zIndex))}
    .item:nth-child(3) {background: rgba(51, 0, 51, var(--opacity)); transform: rotateY(120deg) translate3d(0, 50%, var(--zIndex)) }
    .item:nth-child(4) {background: rgba(51, 255, 204, var(--opacity)); transform: rotateY(180deg) translate3d(0, 50%, var(--zIndex)) }
    .item:nth-child(5) {background: rgba(102, 0, 0, var(--opacity)); transform: rotateY(240deg) translate3d(0, 50%, var(--zIndex)) }
    .item:nth-child(6) {background: rgba(102, 153, 204, var(--opacity)); transform: rotateY(300deg) translate3d(0, 50%, var(--zIndex)) }
    
    .item:before {width: 200%; height: 400%; transform-origin: 50% 50%; position: absolute; left: 0; right: 0; content: ''; background: rgba(255, 255, 255, 0.3); transform: translate(0px, -100px) rotateZ(30deg);}
    
    @keyframes rotate {
      0% {transform: rotateY(0deg)}
      100% {transform: rotateY(360deg)}
    }
  </style>
</body>
</html>
