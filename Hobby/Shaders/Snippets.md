#### XY Coordinate Normalization 
Bonzomatic
```c	
	vec2 uv = out_texcoord;
	uv -= 0.5;
	uv /= vec2(v2Resolution.y / v2Resolution.x, 1)/2;


```

 X coordinates are in \[-1,78,1.78] range using the above code in a 1920x1080 screen.
Y is in \[-1,1]
