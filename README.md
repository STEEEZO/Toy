### Shadertoy host for Unity

1. Write a Shadertoy shader or find one you like on [Shadertoy](https://www.shadertoy.com/).

2. Copy the shader source and save as a textfile (shadername.txt) somewhere in your Unity project. Unity will create a text asset for you.

3. Add the Toy component to your Camera.

4. Drag & Drop the Shadertoy text asset into the Shadertoy Text property in the Toy component inspector.

We recommend you use the [Shadertoy](https://www.shadertoy.com/) service to work on your GLSL shaders.

### Shadertoy license

Make sure you respect the license of any Shadertoy code you use.

### Troubleshooting

Toy converts Shadertoy GLSL source code to ShaderLab/cg naively. Things it cannot handle automatically are:

#### Nested matrix multiplication
```glsl
mat3 M = N * (P * Q);
```
replace with 
```glsl
mat3 TMP = P * Q;
mat3 M = N * TMP;
```

#### Shorthand ivec and bvec initializers
The converter cannot tell whether argument is a scalar or another vec
```glsl
bvec2 bv = bvec2(b);
ivec2 iv = ivec2(i);
```
replace with 
```glsl
bvec2 bv = bvec2(b, b);
ivec2 iv = ivec2(i, i);
```

#### cg is more picky than glsl about vector initialization
Avoid using initializers that mix argument types, use e.g.
```glsl
float s = 1.0;
vec2 v2 = vec2(s, s);
vec3 v3 = vec3(v2, s);
vec4 v4 = vec4(s);
```
