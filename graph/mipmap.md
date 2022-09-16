# Mipmap

Ref: http://www.cs.cmu.edu/afs/cs.cmu.edu/academic/class/15869-f11/www/readings/williams83_mipmap.pdf

在图形学中，Texture 用来表示一个物体表面的颜色信息。

* Texture space 是一个 2D space
* World space 是一个 3D space
* Screen space 是一个 2D space

Texture space (u,v) 和 World space (x,y,z) 之间的映射就是 Texture Mapping。

如果 Texture 是 100x100 的，Screen 是 500x500 的，那么屏幕上的几个点都映射到 Texture 上的同一个点，就会造成走样。
考虑一下在一个人胳膊上纹了一个名字，后来这个人胳膊变粗了，纹的名字也就认不出来了。这个问题可以通过插值解决。

如果 Texture 是 500x500 的，Screen 是 100x100 的，其实也会发生走样，可能表现为近处锯齿（jaggies），远处摩尔纹（morie）。
近处锯齿，原因和 Texture 过小是一样的。远处摩尔纹，粗略地说，是因为无法将多个点（texel）的纹理塞进一个屏幕像素。

Mipmap (L. Williams 83) 通过提供不同 level 的纹理，解决这一问题。Level 0 是精度最高的，也是原始的 Texture，Level 1 的精度减半，Level 2 再减半。
比如 Level 0 是 128x128 的，那么 Level 1 就是 64x64 的，Level 2 就是 32x32 的。

Level D 的选择使用这个公式

$$
D = \log_2 \max \left(
  \sqrt{
    \left( \frac{du}{dx} \right)^2 + 
    \left( \frac{dv}{dx} \right)^2}, 
  \sqrt{
    \left( \frac{du}{dy} \right)^2 +
    \left( \frac{dv}{dy} \right)^2}
\right)
$$

