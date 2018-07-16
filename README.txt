{\rtf1\ansi\ansicpg1252\cocoartf1561\cocoasubrtf200
{\fonttbl\f0\fswiss\fcharset0 Helvetica;}
{\colortbl;\red255\green255\blue255;}
{\*\expandedcolortbl;;}
\margl1440\margr1440\vieww21460\viewh11920\viewkind0
\pard\tx566\tx1133\tx1700\tx2267\tx2834\tx3401\tx3968\tx4535\tx5102\tx5669\tx6236\tx6803\pardirnatural\partightenfactor0

\f0\fs26 \cf0 READ ME\
\
A method to find the inverse of the transformation which places the camera was developed to render lines and polygons in 3D with perspective view. All of the vertices that are used to render the polygon will be multiplied by the transformation. The points were multiplied to CameraToScreen transformation which conducted by multiplying the simple metric and the projectionToScreen matrix. This method excelled on successfully render the fist page. Clipping problems occurred starting at second page, where a clipping of Z axis are needed. A clipper class was made to clip Z which implements well and finished second page. Starting from pageC, polygons need to be rendered under the depthcueDrawable, I modified the depthcueDrawable, however, it is not enough to render well. I found interpolating between 1/z is the key, 1/z was passed to fillpolygonRenderer instead of z. Another calculation of 1/z in setpixel was added in depthdrawable. FillPolygonRender was modified to have correct shader passed in.  This shader was initialized by ambient light. Using Lambda function, I multiplied ambient light shader to each pixel I’m trying to draw. Along with some modification in Simp interpreter, rest of simp pages are able to draw, however, it takes too long to draw. It is impossible to draw some polygon with very large or small magnitude of x and y. Therefore, I added X and Y clipper to my clipper class, which does similar thing as Z clipper. However, there were bugs occurs after X and Y clipping. The simp interpreter were modified to have vertices be multiplied by CTM and then clipped by Z, Simple perspective metrics was multiplied right after. Before multiplying the projectToScreen matrix, I clipped X and Y with perspective of the limits set by camera command. Finally, projectionToScreen is applied. In ObjectRead class, I simply did lots of function calls of simpInterpreter, which were modified as statics. Some features like “normal” and “texture” I have not done yet. For pageJ, I have found a obj file that someone else did from turbosquid.com. There were lots of debugging to get satisfied graphs. The specifications of 3D perspective view rendering are all satisfied.



