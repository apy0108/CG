Practical No.2 
Problem Statement:  
Implement DDA and Bresenham line drawing algorithm to draw: i) Simple Line ii) 
Dotted Line iii) Dashed Line iv) Solid line ; using mouse interface Divide the screen in four 
quadrants withcenter as (0, 0). The line should work for all the slopes positive as well as 
negative  
CODE:- 
#include<iostream> 
#include<GL/glut.h> 
using namespace std; 
int  Algo,type; 
void Init() 
{ 
} 
{ 
glClearColor(0,0,0,0); 
glColor3f(0,1,0); 
gluOrtho2D(0,640,0,480); 
glClear(GL_COLOR_BUFFER_BIT); 
int sign(float a) 
if(a==0){ 
return 0; 
} 
if(a>0){ 
return 1; 
} 
return -1; 
} 
void B_Line(int x_1,int y_1,int x_2,int y_2,int t){ 
float dy, dx, m , P; 
dy = y_2 - y_1; 
dx = x_2 - x_1; 
m = dy/dx; 
P = 2*dy - dx; 
int x = x_1, y = y_1; 
cout<<"\n x1 = "<<x<<" y1 = "<<y; 
if(m<1){ 
int cnt=1; 
for(int i=0; i<=dx;i++){ 
if(t == 1){ 
glBegin(GL_POINTS); 
glVertex2i(x,y); 
glEnd(); 
} 
if(t == 2){ 
if(i%2==0){ 
glBegin(GL_POINTS); 
                        glVertex2i(x,y); 
                    glEnd(); 
                } 
            } 
            if(t == 3){ 
                 if(cnt <= 10){ 
                    glBegin(GL_POINTS); 
                        glVertex2i(x,y); 
                    glEnd(); 
                } 
                cnt++; 
                if(cnt == 15){ 
                    cnt =1; 
                } 
             } 
             if(P<0){ 
                 x = x +1; 
                y =y; 
                P = P + 2*dy; 
            } 
            else{ 
                 x= x+1; 
                y = y+1; 
                P = P + 2*dy - 2*dx; 
             } 
        } 
    } 
    else{ 
        int cnt = 1; 
        for(int i=0;i<=dy;i++){ 
            if(t == 1){ 
                glBegin(GL_POINTS); 
                    glVertex2i(x,y); 
                glEnd(); 
            } 
            if(t == 2){ 
                 if(i%2==0){ 
                    glBegin(GL_POINTS); 
                        glVertex2i(x,y); 
                    glEnd(); 
                } 
            } 
            if(t == 3){ 
                 if(cnt <= 10){ 
                    glBegin(GL_POINTS); 
                        glVertex2i(x,y); 
                    glEnd(); 
                 } 
                cnt++; 
                if(cnt == 15){ 
                    cnt =1; 
                } 
             } 
            if(P<0){ 
                 x = x; 
                y =y+1; 
                P = P + 2*dx; 
            } 
            else{ 
                 x= x+1; 
                y = y+1; 
                P = P + 2*dx - 2*dy; 
             } 
        } 
    } 
    cout<<"\n xlast = "<<x<<" ylast = "<<y; 
    glFlush(); 
} 
  
void DDA_LINE(int x_1,int y_1,int x_2,int y_2, int t){ 
float dx,dy,length; 
dx = x_2-x_1; 
dy = y_2-y_1; 
if(abs(dx) >= abs(dy)){ 
length = abs(dx); 
} 
else{ 
length = abs(dy); 
} 
float xin, yin; 
xin = dx/length; 
yin = dy/length; 
float x,y; 
x = x_1 + 0.5 * sign(xin); 
y = y_1 + 0.5 * sign(yin); 
int i=0; 
int cnt =1; 
while(i<=length){ 
if(t == 1){ 
glBegin(GL_POINTS); 
glVertex2i(x,y); 
glEnd(); 
        } 
        if(t == 2){ 
             if(i%2==0){ 
                glBegin(GL_POINTS); 
                    glVertex2i(x,y); 
                glEnd(); 
            } 
        } 
        if(t == 3){ 
             if(cnt <= 10){ 
                glBegin(GL_POINTS); 
                    glVertex2i(x,y); 
                glEnd(); 
             } 
            cnt++; 
            if(cnt == 15){ 
                cnt =1; 
            } 
         } 
         x = x + xin; 
        y = y + yin; 
        i++ ; 
  
} 
glFlush(); 
} 
void display() 
{ 
} 
DDA_LINE(0,240,640,240,1); 
B_Line(320,0,320,640,1); 
glFlush(); 
void mymouse(int b,int s, int x, int y) 
{ 
static int x_s,y_s,x_e,y_e,pt=0; 
if(b==GLUT_LEFT_BUTTON && s==GLUT_DOWN) 
{ 
if(pt==0) 
{ 
} 
x_s =x; 
y_s =480 - y; 
pt++; 
glBegin(GL_POINTS); 
glVertex2i(x_s,y_s); 
glEnd(); 
else 
{ 
} 
} 
x_e=x; 
y_e=480-y; 
cout<<"\n x_1_click "<<x_s<<" y_1_click "<<y_s; 
cout<<"\n x_2_click "<<x_e<<" y_2_click "<<y_e<<"\n"; 
glBegin(GL_POINTS); 
glVertex2i(x_e,y_e); 
glEnd(); 
if(Algo == 1){ 
DDA_LINE(x_s,y_s,x_e,y_e,type); 
} 
if(Algo == 2){ 
B_Line(x_s,y_s,x_e,y_e,type); 
} 
else if(b==GLUT_RIGHT_BUTTON && s==GLUT_DOWN) 
{ 
} 
pt=0; 
glFlush(); 
} 
int main(int argc ,char **argv) 
{ 
} 
cout<<"\n Select the Algorithm \n 1. DDA \n 2. Bresenham's \n"; 
cin>>Algo; 
cout<<"Select the Line Type \n 1. Simple Line \n 2. Dotted Line\n 3. Dashed Line \n"; 
cin>>type; 
if((Algo == 1 || Algo == 2 )&&(type==1 || type==2 || type==3)){ 
} 
else{ 
cout<<"\n Option enter are wrong \n"; 
return 0; 
} 
glutInit(&argc,argv); 
glutInitDisplayMode(GLUT_SINGLE|GLUT_RGB); 
glutInitWindowPosition(100,100); 
glutInitWindowSize(640,480); 
glutCreateWindow("DDA-Line"); 
Init(); 
glutDisplayFunc(display); 
glutMouseFunc(mymouse); 
glutMainLoop(); 
return 0; 
Output: 
 
 
 
  

Practical 3 
Problem Statement:  
Implement Bresenham circle drawing algorithm to draw any object. The object should be 
displayed in all the quadrants with respect to center and radius 
Program Code:- 
#include<GL/glut.h> 
#include<iostream> 
using namespace std; 
int r; 
void E_way(int x, int y) 
{ 
glBegin(GL_POINTS); 
glColor3f(1, 1, 0); 
glVertex2i(x+320,y+240); 
glVertex2i(y+320,x+240); 
glColor3f(1, 0, 1); 
glVertex2i(y+320, -x+240); 
glVertex2i(x+320, -y+240); 
glColor3f(0, 1, 1); 
glVertex2i(-x+320,-y+240); //Octant 7 
glVertex2i(-y+320,-x+240); //Octant 8 
glColor3f(1, 1, 0); 
glVertex2i(-y+320,x+240); 
glVertex2i(-x+320,y+240); 
glEnd(); 
glFlush(); 
} 
void B_circle() 
{ 
} 
float d; 
d = 3 - 2*r; 
int x,y; 
x = 0 ;  
y = r ; 
do{ 
E_way(x,y); 
if(d<0) 
{ 
} 
d=d+4*x+6; 
else 
{ 
d= d+4*(x-y)+10; 
y=y-1; 
} 
x=x+1; 
}while(x<y); 
void init(){ 
glClearColor(1,1,1,0); 
glColor3f(1,0,0); 
gluOrtho2D(0,640,0,480); 
glClear(GL_COLOR_BUFFER_BIT); 
} 
int main(int argc, char **argv) 
{ 
} 
cout<<"\n Enter Radius \t "; 
cin>>r; 
glutInit(&argc, argv); 
glutInitDisplayMode(GLUT_SINGLE | GLUT_RGB); 
glutInitWindowPosition(100,100); 
glutInitWindowSize(640,480); 
glutCreateWindow("Circle"); 
init(); 
glutDisplayFunc(B_circle); 
glutMainLoop(); 
return 0; 
Output:  
Practical 4 
Problem Statement : 
Implement the following polygon filling methods :  
i) Flood fill / Seed fill  
ii) Boundary fill ; using 
mouse click, keyboard interface and menu driven programming 
Code:- 
#include <iostream> 
#include <math.h> 
#include <GL/glut.h> 
using namespace std; 
float R=0,G=0,B=0; 
int Algo; 
void init(){ 
glClearColor(1.0,1.0,1.0,0.0); 
glMatrixMode(GL_PROJECTION); 
gluOrtho2D(0,640,0,480); 
} 
void floodFill(int x, int y, float *newCol, float *oldcol){ 
float pixel[3]; 
glReadPixels(x,y,1,1,GL_RGB,GL_FLOAT,pixel); 
if(oldcol[0]==pixel[0] && oldcol[1]==pixel[1] && oldcol[2]==pixel[2]){ 
glBegin(GL_POINTS); 
glColor3f(newCol[0],newCol[1],newCol[2]); 
glVertex2i(x,y); 
glEnd(); 
glFlush(); 
floodFill(x,y+1,newCol,oldcol); 
floodFill(x+1,y,newCol,oldcol); 
floodFill(x,y-1,newCol,oldcol); 
floodFill(x-1,y,newCol,oldcol); 
} 
}     
void boundaryFill(int x, int y, float* fillColor, float* bc){ 
float color[3]; 
glReadPixels(x,y,1.0,1.0,GL_RGB,GL_FLOAT,color); 
if((color[0]!=bc[0] || color[1]!=bc[1] || color[2]!=bc[2]) && (fillColor[0]!=color[0] || 
fillColor[1]!=color[1] || fillColor[2]!=color[2])){ 
glColor3f(fillColor[0],fillColor[1],fillColor[2]); 
glBegin(GL_POINTS); 
glVertex2i(x,y); 
glEnd(); 
glFlush(); 
boundaryFill(x+1,y,fillColor,bc); 
boundaryFill(x-1,y,fillColor,bc); 
boundaryFill(x,y+1,fillColor,bc); 
boundaryFill(x,y-1,fillColor,bc); 
} 
return; 
} 
void mouse(int btn, int state, int x, int y){ 
y = 480-y; 
if(btn == GLUT_LEFT_BUTTON && state == GLUT_DOWN){ 
float bcol[] = {1,0,0}; 
float oldcol[] = {1,1,1}; 
float newCol[] = {R,G,B}; 
if(Algo==1){ 
boundaryFill(x,y,newCol,bcol); 
} 
if(Algo==2){ 
floodFill(x,y,newCol,oldcol); 
}    
} 
} 
void B_Draw(){ 
glClear(GL_COLOR_BUFFER_BIT); 
glColor3f(1,0,0); 
glBegin(GL_LINE_LOOP); 
glVertex2i(150,100); 
glVertex2i(300,300); 
glVertex2i(450,100); 
glEnd(); 
glFlush();   
} 
void F_Draw(){ 
glClear(GL_COLOR_BUFFER_BIT); 
glBegin(GL_LINES); 
glColor3f(1,0,0);glVertex2i(150,100);glVertex2i(300,300); 
glEnd(); 
glBegin(GL_LINE_LOOP); 
glColor3f(0,0,1);glVertex2i(300,300);glVertex2i(450,100); 
glEnd(); 
glBegin(GL_LINE_LOOP); 
glColor3f(0,0,0);glVertex2i(450,100);glVertex2i(150,100); 
glEnd(); 
glFlush(); 
} 
void goMenu(int value){ 
switch(value){ 
case 1: 
R = 0, G = 1, B=0; 
break; 
case 2: 
R = 1, G = 1, B=0; 
break; 
case 3: 
R = 1, G = 0, B=1; 
break; 
} 
glutPostRedisplay(); 
} 
int main(int argc, char** argv){ 
cout<<"\n \t Select the Algorithm "; 
cout<<"\n \t 1. Boundary Fill Algorithm "; 
cout<<"\n \t 2. Flood Fill Algorithm \n \t"; 
cin>>Algo; 
glutInit(&argc, argv); 
glutInitDisplayMode(GLUT_SINGLE|GLUT_RGB); 
glutInitWindowSize(640,480); 
glutInitWindowPosition(200,200); 
glutCreateWindow("A4"); 
init(); 
glutCreateMenu(goMenu); 
glutAddMenuEntry("Color 1 Green",1); 
glutAddMenuEntry("Color 2 Yellow",2); 
glutAddMenuEntry("Color 3 Pink",3); 
glutAttachMenu(GLUT_RIGHT_BUTTON);  
if(Algo==1){ 
glutDisplayFunc(B_Draw); 
} 
if(Algo==2){ 
glutDisplayFunc(F_Draw); 
} 
glutMouseFunc(mouse); 
glutMainLoop(); 
return 0; 
} 
Output:- 
  
  
 
 
 
 
 
 

Practical 5 
Problem Statement : 
Implement Cohen Sutherland polygon clipping method to clip the polygon with respect the 
viewport and window. Use mouse click, keyboard interface. 
Code:- 
#include <iostream> 
#include <math.h> 
#include <time.h> 
#include <GL/glut.h> 
using namespace std; 
int wxmin = 200,wxmax=500,wymax=350, wymin=100; 
int points[10][2]; 
int edge; 
void init(){ 
glClearColor(1.0,1.0,1.0,0.0); 
glMatrixMode(GL_PROJECTION); 
gluOrtho2D(0,640,0,480); 
glClear(GL_COLOR_BUFFER_BIT); 
} 
void Draw(){ 
glClearColor(1.0,1.0,1.0,0.0); 
glClear(GL_COLOR_BUFFER_BIT); 
glColor3f(0.2,0.2,1); 
glBegin(GL_POLYGON); 
for(int i=0; i<edge; i++) 
{ 
glVertex2i(points[i][0],points[i][1]);    
} 
glEnd(); 
glFlush(); 
glColor3f(0,1,0); 
glBegin(GL_LINE_LOOP); 
glVertex2i(200,100); 
glVertex2i(500,100); 
glVertex2i(500,350); 
glVertex2i(200,350); 
glEnd(); 
glFlush(); 
} 
int BottomCliping(int e){ 
float m=0; 
int x=0,k=0; 
int t[10][2]; 
for(int i=0; i<e; i++){ 
if(points[i][1] < wymin){ 
if(points[i+1][1]  < wymin){ 
} 
else if(points[i+1][1] > wymin){ 
float x1,x2; 
float y1,y2; 
                x1 = points[i][0]; 
                y1 = points[i][1]; 
                x2 = points[i+1][0]; 
                y2 = points[i+1][1]; 
                x = ((1/((y2-y1)/(x2-x1))) * (wymin - y1) )+ x1; 
                t[k][0] = x; 
                t[k][1] = wymin; 
                k++;  
            } 
        } 
        else if(points[i][1]>wymin){ 
                       if(points[i+1][1] > wymin){ 
                t[k][0] = points[i][0]; 
                t[k][1] = points[i][1]; 
                k++; 
            } 
            else if(points[i+1][1] < wymin){ 
                float x1,x2; 
                float y1,y2; 
                x1 = points[i][0]; 
                y1 = points[i][1]; 
                x2 = points[i+1][0]; 
                y2 = points[i+1][1]; 
                x = ((1/((y2-y1)/(x2-x1))) * (wymin - y1) )+ x1; 
                t[k][0] = x1; 
t[k][1] = y1; 
k++; 
t[k][0] = x; 
t[k][1] = wymin; 
k++;       
} 
} 
} 
cout<<"k = "<<k; 
for(int i=0; i<10;i++) 
{ 
{ 
points[i][0] = 0; 
points[i][1] = 0; 
} 
for(int i=0; i<k;i++) 
cout<<"\n"<<t[i][0]<<" "<<t[i][1]; 
points[i][0] = t[i][0]; 
points[i][1] = t[i][1]; 
} 
points[k][0] = points[0][0]; 
points[k][1] = points[0][1]; 
return k; 
}  
int TopCliping(int e){ 
float m=0; 
int x=0,k=0; 
int t[10][2]; 
for(int i=0; i<e; i++){ 
if(points[i][1] > wymax){ 
if(points[i+1][1]  > wymax){ 
} 
else if(points[i+1][1] < wymax){ 
float x1,x2; 
float y1,y2; 
x1 = points[i][0]; 
y1 = points[i][1]; 
x2 = points[i+1][0]; 
y2 = points[i+1][1]; 
x = ((1/((y2-y1)/(x2-x1))) * (wymax - y1) )+ x1; 
t[k][0] = x; 
t[k][1] = wymax; 
k++; 
} 
} 
else if(points[i][1]<wymax){ 
if(points[i+1][1] < wymax){ 
t[k][0] = points[i][0]; 
t[k][1] = points[i][1]; 
k++; 
            } 
            else if(points[i+1][1] > wymax){ 
                float x1,x2; 
                float y1,y2; 
                x1 = points[i][0]; 
                y1 = points[i][1]; 
                x2 = points[i+1][0]; 
                y2 = points[i+1][1]; 
                       x = ((1/((y2-y1)/(x2-x1))) * (wymax - y1) )+ x1; 
                               t[k][0] = x1; 
                t[k][1] = y1; 
                k++; 
                t[k][0] = x; 
                t[k][1] = wymax; 
                k++; 
            } 
           } 
        } 
    cout<<"k = "<<k; 
    for(int i=0; i<10;i++) 
    { 
        points[i][0] = 0; 
        points[i][1] = 0; 
        } 
     
for(int i=0; i<k;i++) 
{ 
cout<<"\n"<<t[i][0]<<" "<<t[i][1]; 
points[i][0] = t[i][0]; 
points[i][1] = t[i][1]; 
} 
points[k][0] = points[0][0]; 
points[k][1] = points[0][1]; 
return k; 
} 
int leftCliping(int e){ 
float m=0; 
int y=0, k = 0; 
int t[10][2]; 
for(int i=0;i<e;i++) 
{ 
if(points[i][0] < wxmin){ 
if(points[i+1][0] < wxmin){ 
cout<<"\n Test 1";                                    
} 
else if (points[i+1][0] > wxmin){ 
cout<<"\n Test 2"; 
float x1,x2; 
float y1,y2; 
x1 = points[i][0]; 
                y1 = points[i][1]; 
                x2 = points[i+1][0]; 
                y2 = points[i+1][1]; 
                y = (((y2-y1)/(x2-x1)) * (wxmin - x1) )+ y1; 
                t[k][0] = wxmin; 
                t[k][1] = y; 
                k++;    
            } 
        } 
        else if(points[i][0] > wxmin){ 
                   if(points[i+1][0] > wxmin){ 
                t[k][0] = points[i][0]; 
                t[k][1] = points[i][1]; 
                k++; 
            } 
            else if(points[i+1][0] < wxmin){ 
                float x1,x2; 
                float y1,y2; 
                x1 = points[i][0]; 
                y1 = points[i][1]; 
                x2 = points[i+1][0]; 
                y2 = points[i+1][1]; 
                y = ((y2-y1)/(x2-x1)*(wxmin - x1)) + y1; 
                               t[k][0] = x1; 
                t[k][1] = y1; 
k++; 
t[k][0] = wxmin; 
t[k][1] = y; 
k++; 
} 
}    
} 
cout<<"k = "<<k; 
for(int i=0; i<10;i++) 
{ 
{ 
points[i][0] = 0; 
points[i][1] = 0; 
} 
for(int i=0; i<k;i++) 
cout<<"\n"<<t[i][0]<<" "<<t[i][1]; 
points[i][0] = t[i][0]; 
points[i][1] = t[i][1]; 
} 
points[k][0] = points[0][0]; 
points[k][1] = points[0][1]; 
return k; 
} 
int RightCliping(int e){ 
float m=0; 
int y=0, k = 0; 
int t[10][2]; 
for(int i=0;i<e;i++) 
{ 
if(points[i][0] > wxmax){ 
if(points[i+1][0] > wxmax){ 
} 
else if(points[i+1][0] < wxmax){ 
float x1,x2; 
float y1,y2; 
x1 = points[i][0]; 
y1 = points[i][1]; 
x2 = points[i+1][0]; 
y2 = points[i+1][1]; 
y = (((y2-y1)/(x2-x1)) * (wxmax - x1) )+ y1; 
t[k][0] = wxmax; 
t[k][1] = y; 
k++; 
} 
} 
else if(points[i][0] < wxmax){ 
if(points[i+1][0] < wxmax){ 
t[k][0] = points[i][0]; 
t[k][1] = points[i][1]; 
                k++; 
            } 
            else if(points[i+1][0] > wxmax){ 
                           float x1,x2; 
                float y1,y2; 
                x1 = points[i][0]; 
                y1 = points[i][1]; 
                x2 = points[i+1][0]; 
                y2 = points[i+1][1]; 
                       y = ((y2-y1)/(x2-x1)*(wxmax - x1)) + y1; 
                t[k][0] = x1; 
                t[k][1] = y1; 
                k++; 
                t[k][0] = wxmax; 
                t[k][1] = y; 
                k++; 
            }    
        }    
    } 
    cout<<"k = "<<k; 
    for(int i=0; i<10;i++) 
    { 
        points[i][0] = 0; 
        points[i][1] = 0; 
     
}    
for(int i=0; i<k;i++) 
{ 
cout<<"\n"<<t[i][0]<<" "<<t[i][1]; 
points[i][0] = t[i][0]; 
points[i][1] = t[i][1]; 
} 
points[k][0] = points[0][0]; 
points[k][1] = points[0][1]; 
return k; 
} 
void P_C(){ 
Draw(); 
} 
void goMenu(int value){ 
switch(value){ 
case 1: 
edge = leftCliping(edge); 
Draw(); 
break; 
case 2: 
edge = RightCliping(edge); 
Draw(); 
break; 
case 3: 
edge = TopCliping(edge); 
Draw(); 
break; 
case 4: 
edge = BottomCliping(edge); 
Draw(); 
break; 
} 
glutPostRedisplay(); 
} 
int main(int argc, char** argv){ 
cout<<"\n Enter No of edges of polygon  "; 
cin>>edge; 
for(int i=0;i<edge;i++){ 
cout<<"\n Enter point "<<i<<" x space y "; 
cin>>points[i][0]>>points[i][1]; 
} 
points[edge][0] = points[0][0]; 
points[edge][1] = points[0][1]; 
glutInit(&argc, argv); 
glutInitDisplayMode(GLUT_SINGLE|GLUT_RGB); 
glutInitWindowSize(640,480); 
glutInitWindowPosition(200,200); 
glutCreateWindow("Polygon Clipping"); 
init();    
glutCreateMenu(goMenu); 
glutAddMenuEntry("Left",1); 
glutAddMenuEntry("Right",2); 
glutAddMenuEntry("Top",3); 
glutAddMenuEntry("Bottom",4); 
glutAttachMenu(GLUT_RIGHT_BUTTON); 
glutDisplayFunc(P_C);  
glutMainLoop(); 
return 0; 
Output: 
 
  
Practical 6 
Problem Statement : 
Implement following 2D transformations on the object with respect to axis : –  
i) Scaling ii) Rotation about arbitrary point iii) Reflection 
Code:- 
#include <iostream> 
#include <math.h> 
#include <time.h> 
#include <GL/glut.h> 
#include <vector> 
using namespace std; 
int edge; 
vector<int> xpoint; 
vector<int> ypoint; 
int ch; 
double round(double d){ 
return floor(d + 0.5); 
} 
void init(){ 
glClearColor(1.0,1.0,1.0,0.0); 
glMatrixMode(GL_PROJECTION); 
gluOrtho2D(0,640,0,480); 
glClear(GL_COLOR_BUFFER_BIT); 
} 
void translation(){ 
int tx, ty; 
cout<<"\t Enter Tx, Ty \n"; 
cin>> tx>> ty; 
//Translate the point 
for(int i=0;i<edge;i++){ 
xpoint[i] = xpoint[i] + tx; 
ypoint[i] = ypoint[i] + ty; 
} 
glBegin(GL_POLYGON); 
glColor3f(0,0,1); 
for(int i=0;i<edge;i++){ 
glVertex2i(xpoint[i],ypoint[i]); 
} 
glEnd(); 
glFlush(); 
} 
void rotaion(){ 
int cx, cy; 
cout<<"\n Enter Ar point x , y "; 
cin >> cx >> cy; 
cx = cx+320; 
cy = cy+240; 
glColor3f(0.0, 1.0, 0.0); 
glBegin(GL_POINTS); 
glVertex2i(cx,cy); 
glEnd(); 
glFlush(); 
double the; 
cout<<"\n Enter thetha "; 
cin>>the; 
the = the * 3.14/180; 
glColor3f(0,0,1.0); 
glBegin(GL_POLYGON); 
for(int i=0;i<edge;i++){ 
glVertex2i(round(((xpoint[i] - cx)*cos(the) - ((ypoint[i]-cy)*sin(the))) + cx), 
round(((xpoint[i] - cx)*sin(the) + ((ypoint[i]-cy)*cos(the))) + cy)); 
} 
glEnd(); 
glFlush(); 
} 
void scale(){ 
glColor3f(1.0,0,0); 
glBegin(GL_POLYGON); 
for(int i=0;i<edge;i++){ 
glVertex2i(xpoint[i]-320,ypoint[i]-240); 
} 
glEnd(); 
glFlush(); 
cout<<"\n\tIn Scaling whole screen is 1st Qudrant \n"; 
int sx, sy; 
cout<<"\t Enter sx, sy \n"; 
cin>> sx>> sy; 
//scale the point 
for(int i=0;i<edge;i++){ 
xpoint[i] = (xpoint[i]-320) * sx; 
ypoint[i] = (ypoint[i]-240) * sy;      
} 
glColor3f(0,0,1.0); 
glBegin(GL_POLYGON); 
for(int i=0;i<edge;i++){ 
glVertex2i(xpoint[i],ypoint[i]); 
} 
glEnd(); 
glFlush(); 
} 
void reflection(){ 
char reflection; 
cout<<"Enter Reflection Axis \n"; 
cin>> reflection; 
if(reflection == 'x' || reflection == 'X'){ 
glColor3f(0.0,0.0,1.0); 
glBegin(GL_POLYGON); 
for(int i=0;i<edge;i++){ 
glVertex2i(xpoint[i], (ypoint[i] * -1)+480); 
} 
glEnd(); 
glFlush(); 
} 
else if(reflection == 'y' || reflection == 'Y'){ 
glColor3f(0.0,0.0,1.0); 
glBegin(GL_POLYGON); 
for(int i=0;i<edge;i++){ 
glVertex2i((xpoint[i] * -1)+640,(ypoint[i])); 
} 
glEnd(); 
glFlush(); 
}     
} 
void Draw(){ 
if(ch==2 || ch==3 || ch==4){ 
glColor3f(1.0,0,0); 
glBegin(GL_LINES); 
glVertex2i(0,240); 
glVertex2i(640,240); 
glEnd(); 
glColor3f(1.0,0,0); 
glBegin(GL_LINES); 
glVertex2i(320,0); 
glVertex2i(320,480); 
glEnd(); 
glFlush(); 
glColor3f(1.0,0,0); 
glBegin(GL_POLYGON); 
for(int i=0;i<edge;i++){ 
glVertex2i(xpoint[i],ypoint[i]); 
} 
glEnd(); 
glFlush(); 
} 
if(ch==1){ 
scale(); 
} 
else if(ch == 2){ 
rotaion(); 
} 
else if( ch == 3){ 
reflection(); 
} 
else if (ch == 4){ 
translation(); 
} 
} 
int main(int argc, char** argv){ 
cout<<"\n \t Enter 1) Scaling "; 
cout<<"\n \t Enter 2) Rotation about arbitrary point"; 
cout<<"\n \t Enter 3) Reflection"; 
cout<<"\n \t Enter 4) Translation  \n \t"; 
cin>>ch; 
if(ch==1 || ch==2 || ch==3 || ch==4){ 
cout<<"Enter No of edges \n"; 
cin>> edge; 
int xpointnew, ypointnew; 
cout<<" Enter"<< edge <<" point of polygon \n"; 
for(int i=0;i<edge;i++){ 
cout<<"Enter "<< i << " Point "; 
cin>>xpointnew>>ypointnew; 
xpoint.push_back(xpointnew+320); 
ypoint.push_back(ypointnew+240); 
} 
} 
glutInit(&argc, argv); 
glutInitDisplayMode(GLUT_SINGLE|GLUT_RGB); 
glutInitWindowSize(640,480); 
glutInitWindowPosition(200,200); 
glutCreateWindow("2D"); 
init(); 
glutDisplayFunc(Draw); 
glutMainLoop(); 
return 0; 
else{ 
cout<<"\n \t Check Input run again"; 
return 0; 
} 
} 
Output:- 
  
  
 
 
 
  
Practical 7 
Problem Statement:- 
Generate fractal patterns using  i) Bezier  ii)    Koch Curve 
i) 
Code:- 
Bezier Curve 
#include <iostream> 
#include <math.h> 
#include <time.h> 
#include <GL/glut.h> 
using namespace std; 
int x[4],y[4]; 
void init(){ 
glClearColor(1.0,1.0,1.0,0.0); 
glMatrixMode(GL_PROJECTION); 
gluOrtho2D(0,640,0,480); 
glClear(GL_COLOR_BUFFER_BIT); 
} 
void putpixel(double xt,double yt ) 
{ 
glColor3f(1,0,0); 
glBegin(GL_POINTS); 
glVertex2d(xt,yt); 
glEnd(); 
glFlush(); 
} 
void Algorithm(){ 
glColor3f(0,1,0); 
glBegin(GL_LINES); 
glVertex2i(x[0],y[0]); 
glVertex2i(x[1],y[1]); 
glVertex2i(x[2],y[2]); 
glVertex2i(x[3],y[3]); 
glEnd(); 
glFlush(); 
double t; 
for (t = 0.0; t < 1.0; t += 0.0005) 
{ 
double xt = pow(1-t, 3) * x[0] + 3 * t * pow(1-t, 2) * x[1] + 3 * pow(t, 2) * (1-t) * x[2] + 
pow(t, 3) * x[3]; 
double yt = pow(1-t, 3) * y[0] + 3 * t * pow(1-t, 2) * y[1] + 3 * pow(t, 2) * (1-t) * y[2] + 
pow(t, 3) * y[3]; 
putpixel(xt, yt); 
}} 
int main(int argc, char** argv){ 
cout<<"\n \t Enter The Four Points x space y "; 
for(int i=0;i<4;i++){ 
cout<<"\n \t Enter x and y for "<<i<<" = "; 
cin>>x[i]>>y[i]; 
}     
glutInit(&argc, argv); 
glutInitDisplayMode(GLUT_SINGLE|GLUT_RGB); 
glutInitWindowSize(640,480); 
glutInitWindowPosition(200,200); 
glutCreateWindow("Bezier 4 point"); 
init(); 
glutDisplayFunc(Algorithm); 
glutMainLoop(); 
return 0; 
} 
Output:- 
ii)    Koch Curve 
Code:- 
#include <GL/glut.h> 
#include <math.h> 
GLfloat oldx=-0.7,oldy=0.5; 
void drawkoch(GLfloat dir,GLfloat len,GLint iter) { 
GLdouble dirRad = 0.0174533 * dir;   
GLfloat newX = oldx + len * cos(dirRad); 
GLfloat newY = oldy + len * sin(dirRad); 
if (iter==0) { 
glVertex2f(oldx, oldy); 
glVertex2f(newX, newY); 
oldx = newX; 
oldy = newY; 
} 
else { 
iter--; 
//draw the four parts of the side _/\_  
drawkoch(dir, len, iter); 
dir += 60.0;               
drawkoch(dir, len, iter);  
dir -= 120.0; 
drawkoch(dir, len, iter);  
dir += 60.0; 
drawkoch(dir, len, iter);  
} 
} 
void display(){ 
glClear( GL_COLOR_BUFFER_BIT ); 
glBegin(GL_LINES); 
glColor3f(0.0, 1.0, 0.0); 
drawkoch(0.0,0.04,3); 
drawkoch(-120.0, 0.04, 3); 
drawkoch(120.0,0.04,3); 
glEnd(); 
glFlush();  
} 
int main(int argc, char** argv) 
{ 
glutInit(&argc,argv);  
glutInitDisplayMode(GLUT_SINGLE|GLUT_RGB);       
glutInitWindowSize(500,500);      
glutInitWindowPosition(0,0);  
glutCreateWindow("Koch Curve");      
glutDisplayFunc(display);   
glutMainLoop(); 
} 
Output: 
 
 
 
 
 
 
 
 
 
Practical 8 
Problem Statement:- 
Implement animation principles for any object. 
Code:- 
 #include <GL/gl.h> 
#include <GL/glut.h> 
#include <math.h> 
            
             //global variable diclaration  
 
int frameNumber = 0;           
           //frame no  
      
 void drawWindmill()          
 //Function to draw windmill 
{ 
  
 int i; 
  
 glColor3f(1.0,1.0,0.0);        
 //red green blue 
  
 glBegin(GL_POLYGON);         
        
 glVertex2f(-0.05f, 0);  
     
              //for drawing rectangular base part 
 
 glVertex2f(-0.05f, 3); 
 glVertex2f(0.05f, 3); 
 glVertex2f(0.05f, 0); 
     
    glEnd(); 
     
 glTranslatef(0,3,0);          
 
//x,y,z 
  
 glColor3f(1.0,0.0,0.0);          
 
         //red,green,blue (RED PLATES OF WINDMILL) 
  
 glRotated(frameNumber * (180.0/45), 0, 0, 1);    
 
//(angle,x,y,z) 
  
  for (i = 0; i < 4; i++)         
 
//LOOP TO DRAW FOUR PLATES 
  { 
  glRotated(90, 0, 0, 1);        
 
//90,0,0,Z 
   
  glBegin(GL_POLYGON); 
   
  glVertex2f(0,0);        
 
//FOR DRAWING TYIANGLULAR PLATE 
   
    glVertex2f(1.0f, 0.2f); 
   
    glVertex2f(1.0f,-0.2f); 
      
       glEnd(); 
     }  
} 
  
void display()            
   
//DISPLAY FUNCTION 
{ 
 glClear(GL_COLOR_BUFFER_BIT);         
  
 glLoadIdentity(); 
 
 //TAKES IDENTITY MATRIX 
  
 glPushMatrix();          
 //PUSH MATRIX          
 glTranslated(2.2,1.6,0); 
 
 //SET POSITION OF WINDMILL 
  
 glScaled(0.4,0.4,1); 
 
 //SCALLING WINDMILL WITH POINT (0.4,0.4,1) 
  
 drawWindmill(); 
 
 //FUNCTION CALL TO DRAW WINDMILL 
  
 glPopMatrix();          
  
           //POP MATRIX 
  
  glPushMatrix();         
  
         //PUSH MATRIX 
  
 glTranslated(3.7,0.8,0);      
 
       //SET POSITION OF WINDMILL 
  
 glScaled(0.7,0.7,1);          
 
       //SCALLING WINDMILL WITH POINT(0.7,0.7,1) 
  
 drawWindmill();          
  
    //FUNCTION CALL TO DRAW WINDMILL 
  
 glPopMatrix();          
  
  //POP MATRIX 
  
  
  
 glutSwapBuffers();         
 //SWAP BUFFER 
}   
  
void doFrame(int v)      
{ 
    frameNumber++;          
 //INCREMENT FRAME NO    
  
    glutPostRedisplay();        
 //POST REDISPLAY 
  
    glutTimerFunc(10,doFrame,0); 
} 
  
void init()            
 //FUNCTION INITIALISATION 
{ 
 glClearColor(0,0,0,0); 
  
 glMatrixMode(GL_PROJECTION);      
 //MATRIX MODE  FOR PROJECTION 
  
 glLoadIdentity(); 
                   //LOADS IDENTITY MATRIX 
  
 glOrtho(0, 7, -1, 4, -1, 1);  
       
                 //MIN X,MAX X,MIN Y,MAX Y,MIN Z,MAX Z VALUE 
  
 glMatrixMode(GL_MODELVIEW); 
 
     //MATRIX MODE FOR MODEL VIEW 
} 
  
int main(int argc, char** argv)         
 
            //MAIN FUNCTION 
{ 
    glutInit(&argc, argv);           
     
    glutInitDisplayMode(GLUT_DOUBLE); 
     
    glutInitWindowSize(700,500);  
 
             //DEFINED WINDOW SIZE 700*500 
     
    glutInitWindowPosition(100,100); 
    
            //DEFINED WINDOW POSITION 100,100 
     
    glutCreateWindow("WINDMILL"); 
     
          //NAME OF WINDOW 
     
    init(); 
 
        //FIRSTLY CALL TO INTIALISE VALUE 
     
    glutDisplayFunc(display);  
 
           //DISPLAY   
     
    glutTimerFunc(200,doFrame,0);  
      
        //TIMER FUNC 
  
    glutMainLoop();  
     
    return 0; 
}     
  
 
 
 
 
Output: 
