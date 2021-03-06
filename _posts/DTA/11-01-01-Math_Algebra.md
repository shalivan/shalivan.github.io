---
title: Algebra
description: Math
categories:
- DTA
tags:
- Math
permalink: /mathalgebra/
---




# Notation

|  |Order of operations|
|--- | --- |
|(), [], {} | Parentheses, Brackets, Braces
|x^a , √ | Exponents, radicals
|x, / | Multiplication, Division
|+, - | Addition, Subtraction


| |value| |
|--- | --- | --- |
|0.000 000 256  | 2.56x10^-7 | 1.64e-07
|0.000 2 | 2x10^-4 | 2e-04
|0.2	|2×10^−1| 2e-1
|1	|1×10^0|  Scientific notation
≈ 1.6180 |φ (phi)   | a+b/a Golden ration from fibonacci seq / Golden Angle = 137.5  
| ≈ 2.71828 |e | unique number whose natural logarithm is equal to one   
| ≈ 3.141592 | π (pi)  |  
 | ≈ 4.669 |δ| Feigenbaum Constant ratios in a bifurcation diagram for a non-linear map.
|10 | 1×10^1 | 1e+1 - order of magnitude
|100 | 1×10^2 | 1e+2  - two orders of magnitude
|200 | 2×10^2 | 1e+2





# Linear Algebra
`projective geometry` - points lines and planes, concept of `duality`  (rotation is translation with pivot in infinity)




## Vectors

#### Equations

| Operation |||- |
|- | - | - |- |
|a+b| a+b - move b to tip of a. | Vector
|a-b |  a-b = a+(-b) | Vector
|Dual |a° | Vector
|Dot product |  a°b | Scalar  -1 - 1| 1 = similar, 0 = perpendicular - orthogonal (90°), -1 = opposite dir (180°)
|Cross product | AxB|Normal vector | Normal of plane created by 2 vec len depend on angle n  (only in 3 dimentions)
|Wedge product 2 vect | A^B   | Bivector | plane with orientation witch contain a and b. (magnitude and orient) Exterior |product > (similar to cross)   
|Wedge product 3 vect | A^B^C   | Trivector | Extruded bivector if vect are linearly dependent wedge = 0 ()
|Contraction product| a╜x = B,   a╜b = a*b | |dot in higher dimenmtion (how similar)
|Geometric product | ab = a╜b - a^b, aB = a╜B + a^B  | Real + Bivector| complex number inner(dot) + outer product(wedge,'cross') (plane) -
|Sandwitch product | axa^-1 |  Vector | Reflection
|Rotor | | | is rotattion by double reflection  (quaternion: vector i scalar  quaternion is vector len rotor )
|Quaternion | | Vector4 |

Quaternions, Dual quaternions, Exterior Algebra





https://bivector.net/ - Vectors  
https://eater.net/quaternions - Quaternions    
http://immersivemath.com/ila/index.html  - immersive math        
https://www.desmos.com/calculator - function plot  





-----



## Matrixes
`Tensor` - is like vector  written by components made of dot products of component vectors

---
#### Derivative
1

2



#### Fourier
Fourier Transform: decomposing to freq. .  rtepresent sampled signal as sin and cos
Fast Fourier Transform: recognizing symetry

#### Laplace
Tel us both if sinusoids and exponentials are represented in the function  

divergence of the gradient of some function. so say you have a heightfield (like a 2d grid with a scalar quantity on that grid, defining height).

the laplacian of the height value at any given voxel, will be a scalar value that basically tells you what the rate of change in that voxel will be, if you flow along the height fields gradient.

when you're doing this on a volume grid there's a "discrete laplacian operator" that's basically just a kernel that approximates the real thing

so if u want to sort of guide the growth, you would want to basically define a divergence field (diverg of field '+' when go awa -" when go to this point , )to mix in or merge on top (similar to how u would guide a smoke/flip sim). basically you would want to find the directions you want to flow towards, compute the divergence of that, and then add that on top of your laplace values. but id have to know how the growth is being driven, to confirm if that would work

If you want it to get more interesting rather than your growth weight being just the laplacian you can do something like growthweight = laplacian * dot(volumegradient, vec) where vec comes out of some 3d noise or something


#### Monte-Carlo
random
statistical model with random and proportions to calculate ie area



#### Gerstner Waves


---------



# .md Latex notation

\\( \sqrt{\frac{n!}{k!(n-k)!}} \\) or
this one \\( x^2 + y^2 = r^2 \\).

$$a*b$$

$$axxb$$

$$u^^v$$

$$a^2 + b^2 = c^2$$

$$ \mathsf{Data = PCs} \times \mathsf{Loadings} $$


$$sum_(i=1)^n i^3=((n(n+1))/2)^2$$
