
Below is a starter code for your Three.js project. 


## Before using the starter: 

1)  Create a project folder and then navigate to it;
   
2)  Inside project folder run:
```
npm init -y
```

3) Install required dependencies
```
npm i vite
npm i three
```

4) Include optional dependencies
```
npm i lil-gui
npm i gsap
```

5) In **package.json** file, update the "scripts" section with the following:
```
{
	"scripts": {
		"dev": "vite",
		"build": "vite build"
	}
}
```
 <br> 
 
**NOTE #1:** *This project initially includes lil-gui as a debug tool. In case you don't need it, you might need to remove lil-gui parts in JS file and also omit the installation step for lil-gui*

**NOTE #2:**  *This starter assumes that your HTML, CSS and JS files are located inside the same directory. If that is not the case for your project, then do not forget to update the import path.*

**NOTE #3:**  *In case you want to change either CSS or JS file from below starter, make sure to also  update the new filename inside the HTML file*

## 1. HTML

```
<!DOCTYPE html>
<html lang="en">
<head>
	<meta charset="UTF-8">
	<meta name="viewport" content="width=device-width, initial-scale=1.0">
	<link rel="stylesheet" href="./style.css">
	<title> Three.js Starter </title>
</head>
<body>
	<!-- Create a <canvas> element with ID of: 'webgl-canvas' -->
	<canvas id="webgl-canvas"></canvas>
	<script src="./script.js" type="module"></script>
</body>
</html>
```

## 2. CSS

```
/* Remove default browser styling */
*, *:before, *:after {
	margin: 0;
	padding: 0;
}


/* Make sure the canvas element is always covering the viewport, even when user scrolls */
canvas#webgl-canvas {
	position: fixed;
	top: 0;
	left: 0;
	outline: none;
}
```


## 3A. JS (with Orbit Controls)

```
import * as THREE from "three";
import GUI from "lil-gui";
import { OrbitControls } from "three/examples/jsm/Addons.js";
	
// HOOK FOR HTML CANVAS ELEMENT
const CANVAS_EL = document.querySelector('canvas#webgl-canvas');
	
// USED TO TWEAK THE ISSUE WITH INTERNAL THREEJS COLOR MANAGEMENT
const GUI_GLOBALS = {
	color: "#59a1f3"
}
	
// GLOBAL OBJECT USED TO HANDLE WINDOW RESIZING
const SIZES = {
	WIDTH: window.innerWidth,
	HEIGHT: window.innerHeight,
	updateAspect: function() { return this.WIDTH / this.HEIGHT }
}
	
// Adjust canvas size when resizing the window
window.addEventListener("resize", () => {
	SIZES.WIDTH = window.innerWidth;
	SIZES.HEIGHT = window.innerHeight;
	camera.aspect = SIZES.updateAspect();
	camera.updateProjectionMatrix();
	renderer.setSize(SIZES.WIDTH, SIZES.HEIGHT);
	renderer.setPixelRatio(Math.min(window.devicePixelRatio, 2));
});
	
// Toggle fullscreen mode on double click
window.addEventListener('dblclick', () => {
	const fullScreenEl = document.fullscreenElement || document.webkitFullscreenElement;
	if(!fullScreenEl) {
		if(CANVAS_EL.requestFullscreen) CANVAS_EL.requestFullscreen();
		else if(CANVAS_EL.webkitRequestFullscreen) CANVAS_EL.webkitRequestFullscreen();
	} else {
	if(document.exitFullscreen) document.exitFullscreen();
	else if(document.webkitExitFullscreen) document.webkitExitFullscreen();
	}
});
	
// Initialize the scene
const scene = new THREE.Scene();
	
// Create a basic cube and add it to the scene
const geometryMaterial = new THREE.MeshBasicMaterial({ color: GUI_GLOBALS.color });
const geometry = new THREE.Mesh(
	new THREE.BoxGeometry(1, 1, 1),
	geometryMaterial
);
scene.add(geometry);
	
const camera = new THREE.PerspectiveCamera(75, SIZES.WIDTH / SIZES.HEIGHT, 1, 100);
camera.position.z = 3; // Initially put camera backwards to create some distance between the camera and object
scene.add(camera);
	
const renderer = new THREE.WebGLRenderer({
	canvas: CANVAS_EL
});
renderer.setSize(SIZES.WIDTH, SIZES.HEIGHT);
renderer.render(scene, camera);
	
// Optional - instantiate lil-gui debug panel (first install dependency with: npm i lil-gui)
const gui = new GUI();
	
// Optional - initialize OrbitControls
const controls = new OrbitControls(camera, CANVAS_EL);
controls.enableDamping = true;  // In case you want smoother animation
	
// Lil-gui controls (optional)
gui.add(geometry.scale, "x").min(1).max(2).step(0.1).name("Scale X");
gui.add(geometry.scale, "y").min(1).max(2).step(0.1).name("Scale Y");
gui.addColor(GUI_GLOBALS, "color").onChange(() => geometryMaterial.color.set(GUI_GLOBALS.color));
	
// Set up and further use timer for precise animation regardless of device frame rate
const timer = new THREE.Timer();
	
const loop = () => {
	timer.update();
	controls.update();
	const elapsedTime = timer.getElapsed();
	geometry.rotation.x = Math.cos(elapsedTime / 2); // Animation in case you need it
	geometry.rotation.y = Math.sin(elapsedTime / 2); // Animation in case you need it
	camera.lookAt(geometry.position);
	renderer.render(scene, camera);
	window.requestAnimationFrame(loop);
}
	
loop();
```


## 3B. JS (with custom controls)

```
import * as THREE from "three";
import GUI from "lil-gui";
	
// HOOK FOR HTML CANVAS ELEMENT
const CANVAS_EL = document.querySelector('canvas#webgl-canvas');
	
// USED TO TWEAK THE ISSUE WITH INTERNAL THREEJS COLOR MANAGEMENT
const GUI_GLOBALS = {
	color: "#59a1f3"
}
	
// GLOBAL OBJECT USED TO HANDLE WINDOW RESIZING
const SIZES = {
	WIDTH: window.innerWidth,
	HEIGHT: window.innerHeight,
	updateAspect: function() { return this.WIDTH / this.HEIGHT }
}
	
// GLOBAL OBJECT USED FOR CUSTOM CONTROLS
const CURSOR = {
	xPos: 0,
	yPos: 0,
	STRENGTH: 5,
}
	
// Adjust canvas size when resizing the window
window.addEventListener("resize", () => {
	SIZES.WIDTH = window.innerWidth;
	SIZES.HEIGHT = window.innerHeight;
	camera.aspect = SIZES.updateAspect();
	camera.updateProjectionMatrix();
	renderer.setSize(SIZES.WIDTH, SIZES.HEIGHT);
	renderer.setPixelRatio(Math.min(window.devicePixelRatio, 2));
});
	
// Toggle fullscreen mode on double click
window.addEventListener('dblclick', () => {
	const fullScreenEl = document.fullscreenElement || document.webkitFullscreenElement;
	if(!fullScreenEl) {
		if(CANVAS_EL.requestFullscreen) CANVAS_EL.requestFullscreen();
		else if(CANVAS_EL.webkitRequestFullscreen) CANVAS_EL.webkitRequestFullscreen();
	} else {
		if(document.exitFullscreen) document.exitFullscreen();
		else if(document.webkitExitFullscreen) document.webkitExitFullscreen();
	}
});
	
// Custom camera control on mouse move. Alternatively use controls (eg. Orbit Controls)
window.addEventListener('mousemove', (event) => {
	CURSOR.xPos = event.clientX / SIZES.WIDTH - 0.5;
	CURSOR.yPos = -(event.clientY / SIZES.HEIGHT - 0.5);
})
	
// Initialize the scene
const scene = new THREE.Scene();
	
// Create a basic cube and add it to the scene
const geometryMaterial = new THREE.MeshBasicMaterial({ color: GUI_GLOBALS.color });
const geometry = new THREE.Mesh(
	new THREE.BoxGeometry(1, 1, 1),
	geometryMaterial
);
scene.add(geometry);
	
const camera = new THREE.PerspectiveCamera(75, SIZES.WIDTH / SIZES.HEIGHT, 1, 100);
camera.position.z = 3; // Initially put camera backwards to create some distance between the camera and object
scene.add(camera);
	
const renderer = new THREE.WebGLRenderer({
	canvas: CANVAS_EL
});
	
renderer.setSize(SIZES.WIDTH, SIZES.HEIGHT);
renderer.render(scene, camera);
	
// Optional - instantiate lil-gui debug panel (first install dependency with: npm i lil-gui)
const gui = new GUI();
	
// Lil-gui controls (optional)
gui.add(geometry.scale, "x").min(1).max(2).step(0.1).name("Scale X");
gui.add(geometry.scale, "y").min(1).max(2).step(0.1).name("Scale Y");
gui.addColor(GUI_GLOBALS, "color").onChange(() => geometryMaterial.color.set(GUI_GLOBALS.color));
	
// Set up and further use timer for precise animation regardless of device frame rate
const timer = new THREE.Timer();
	
const loop = () => {
	timer.update();
	const elapsedTime = timer.getElapsed();
	geometry.rotation.x = Math.cos(elapsedTime / 2); // Animation in case you need it
	geometry.rotation.y = Math.sin(elapsedTime / 2); // Animation in case you need it
	camera.position.x = CURSOR.xPos * CURSOR.STRENGTH;
	camera.position.y = CURSOR.yPos * CURSOR.STRENGTH;
	camera.lookAt(geometry.position);
	renderer.render(scene, camera);
	window.requestAnimationFrame(loop);
}
	
loop();
```

## After adding the starter

Now you can simply run the server to start developing your project:

```
npm run dev
```