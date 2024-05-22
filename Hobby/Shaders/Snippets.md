#### XY Coordinate Normalization 
Bonzomatic
```c	
	uv 	vec2 uv = out_texcoord;
	uv -= 0.5;
	uv /= vec2(v2Resolution.y / v2Resolution.x, 1);


```

