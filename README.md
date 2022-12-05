
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">

    <title>canvas_render_heart</title>
    <style>
	body{
		filter: blur(0.5px);
		background: #000;
	}
	.box{
		position: absolute;
		top: 10%;
		left: 5%;
		width: 500px;
		height: 500px;
		background: rgba(255,0, 10, .2);
		border-radius: 50%;
		mix-blend-mode: screen;
		filter: blur(100px);
	}
    canvas{
      display:block;
     /*  border:2px solid red;*/
       margin:0 auto;
      
    }
  h1{
    color:white;
    position:absolute;
    top:80%;
    left:60%;
    text-align:center;
    font-weight:400;
    text-shadow:1px 1px 8px rgba(255,0,0,.7)
   }
    </style>
</head>
<body>
    <h1><i>彬</i></h1>
	<div class="box"></div>
    <canvas id="heart"></canvas>
	
</body>
</html>
<script>
	
        var canvas=document.getElementById("heart");
        canvas.width=600;
        canvas.height=600;
        canvas.style.width=canvas.width+"px";
        canvas.style.height=canvas.height+"px";
		
        var context=canvas.getContext("2d");
        context.translate(canvas.width/2,canvas.height/2);//将坐标系移动到canvas的中心
        context.scale(1,-1);
        context.moveTo(0,0);
        
        //颜色
		//context.fillStyle = 'rgb(255,0,150)'
	    context.fillStyle = 'red'
     
		// context.lineWidth = 0
		// context.strokeStyle = 'rgba(0,0,0,0)'
		function xin(t,r,j,ws){
			this.trans = t
			this.rs = r,
			this.ws = ws,
			this.index = j,
			this.x=this.trans*this.ws*Math.sin(this.index)*Math.sin(this.index)*Math.sin(this.index)
			this.y=this.trans*(16*Math.cos(this.index)-5*Math.cos(2*this.index)-2*Math.cos(3*this.index)-Math.cos(4*this.index));
		}
		
		let ws = 18
		let hs = 16
		let wsSpeed = 0.15
		let hsSpeed = 0.15
		let speed = 0.2

		
		let wqs = []
		let nqs = []
		let hxz = []
		let hxz2 = []
		let dc = []
		
		
		let xings = [wqs,nqs,hxz,hxz2,dc]
		
		sdata()
		
		function sdata(){
			//外圈
			for(let j = 0; j < 500; j+=speed){
				let trans = 9 + Math.random() * 2.5
				let size = Math.random()*2
				let xins = new xin(trans,size,j,ws)
				wqs.push(xins)
			}

			//内圈   300
			for(let j = 0; j < 300; j+=speed){
				let trans = 7 + Math.random() * 5
				let size = Math.random()*2.5
				let xins = new xin(trans,size,j,ws)
				nqs.push(xins)
			}
			
			//核心轴 600 11 2
			for(let j = 0; j <600; j+=speed){
				let trans = 11 + Math.random() * 2
				let size = Math.random()*3.5
				let xins = new xin(trans,size,j,ws)
				hxz.push(xins)
				
			}
			//核心轴2  300
			for(let j = 0; j < 500; j+=speed){
				let trans = 0 + Math.random() * 2.7
				let size = Math.random()* 2.5
				let xins = new xin(trans,size,j,ws)
				hxz2.push(xins)
				
			}
			
			// //顶层  900
			// for(let j = 0; j < 500; j+=speed){
			// 	let trans = 3.5 + Math.random() * 13
			// 	let size = Math.random()*2
			// 	let xins = new xin(trans,size,j,ws)
			// 	dc.push(xins)
			// }	
			
			setInterval(()=>{
				context.clearRect(-canvas.width/2,-canvas.height/2,canvas.width,canvas.height)
				ws += wsSpeed
				if(ws < 16){
					wsSpeed *= -1
				}else if(ws > 18){
					wsSpeed *= -1
				}
				hs += hsSpeed
				if(hs < 14){
					hsSpeed *= -1
				}else if(hs > 16){
					hsSpeed *= -1
				}
				
				hxz.forEach(v=>{
					context.beginPath()
					context.arc(v.trans*ws*Math.sin(v.index)*Math.sin(v.index)*Math.sin(v.index),v.trans*(hs*Math.cos(v.index)-5*Math.cos(2*v.index)-2*Math.cos(3*v.index)-Math.cos(4*v.index)),v.rs,0,Math.PI * 2)
					context.fill()
					context.stroke()
					context.closePath()       
				})
				hxz2.forEach(v=>{
					context.beginPath()
					context.arc(v.trans*ws*Math.sin(v.index)*Math.sin(v.index)*Math.sin(v.index),v.trans*(hs*Math.cos(v.index)-5*Math.cos(2*v.index)-2*Math.cos(3*v.index)-Math.cos(4*v.index)),v.rs,0,Math.PI * 2)
					context.fill()
					context.stroke()
					context.closePath()       
				})
				
				nqs.forEach(v=>{
					context.beginPath()
					context.arc(v.trans*ws*Math.sin(v.index)*Math.sin(v.index)*Math.sin(v.index),v.trans*(hs*Math.cos(v.index)-5*Math.cos(2*v.index)-2*Math.cos(3*v.index)-Math.cos(4*v.index)),v.rs,0,Math.PI * 2)
					context.fill()
					context.stroke()
					context.closePath()       
				})
				
				wqs.forEach(v=>{
					context.beginPath()
					context.arc(v.trans*ws*Math.sin(v.index)*Math.sin(v.index)*Math.sin(v.index),v.trans*(hs*Math.cos(v.index)-5*Math.cos(2*v.index)-2*Math.cos(3*v.index)-Math.cos(4*v.index)),v.rs,0,Math.PI * 2)
					context.fill()
					context.stroke()
					context.closePath()       
				})
				
				
				dc = []
				//顶层
				for(let j = 0; j < 300; j+=speed){
					let trans = 1 + Math.random() * 20
					let size = Math.random()*2
					let xins = new xin(trans,size,j,ws)
					dc.push(xins)
				}	
				
				dc.forEach(v=>{
					context.beginPath()
					context.arc(v.x,v.y,v.rs,0,Math.PI * 2)
					context.fill()
					context.stroke()
					context.closePath()       
				})
				
			},100)
			
		}
		
		// draw()
		function draw(){
			
			xings.forEach(k=>{
				
				k.forEach(v=>{
					context.beginPath()
					context.arc(v.x,v.y,v.rs,0,Math.PI * 2)
					context.fill()
					context.stroke()
				})
				
			})
			
		}
	
		
		
    
</script>
