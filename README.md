# CGLAB3

DDA ALGORITHM

//  mplement DDA line drawing algorithm. Make sure your algorithm is working for all
//  slope cases. (Print the intermediate pixel values in all cases)


#include<iostream>
#include<GL/glut.h>
#include<bits/stdc++.h>
using namespace std;

int x1 , y_1 , x2 , y2;
bool printed =false;
void DrawLine(int &x1 , int &y_1 , int &x2 , int &y2)
{

     float dx=x2-x1;
     float dy=y2-y_1;
     float m=dy/dx;
     
     float x=x1;
     float y=y_1;
     glBegin(GL_POINTS);
          
         if(m<=1)
         {
              for(int i=0;i<=abs(dx);i++)
              {
                   glVertex2i(round(x), round(y));
                   
                   if(!printed)
                     cout<<"("<<round(x)<<" ,"<<round(y)<<")"<<endl;
                   
                   x=x+1;
                   y=y+m;
              }
         }else{
              
              for(int i=0;i<=abs(dy);i++) 
              {
                   glVertex2i(round(x), round(y));
                    if(!printed)
                     cout<<"("<<round(x)<<" ,"<<round(y)<<")"<<endl;
                   
                   y=y+1;
                   x=x+(1/m);
              }
         }
     glEnd();
     printed=true;
     glFlush();   
}
void Display()
{
     glClear(GL_COLOR_BUFFER_BIT);
     glPointSize(3);
         DrawLine( x1 , y_1 , x2 , y2);
     glFlush();
}
void MyInit()
{
   glClearColor(0,0,0,0);
   
   glMatrixMode(GL_PROJECTION);
   glLoadIdentity();
   gluOrtho2D(0,600,0,600);
}
int main(int c , char* v[])
{
      cout<<"enter first point\n";
      cin>>x1>>y_1;
      cout<<"enter lasta point \n";
      cin>>x2>>y2;
      glutInit(&c , v);
      glutInitWindowSize(600,600);
      glutInitDisplayMode(GLUT_RGB | GLUT_SINGLE);
      glutCreateWindow(" Line drawing algorithm ");
      
      MyInit();
      glutDisplayFunc(Display);
      glutMainLoop();
      return 0;
}




SECOND METHOD 


#include<iostream>
#include<GL/glut.h>
#include<bits/stdc++.h>
using namespace std;

int x1 , y_1 , x2 , y2;
bool printed =false;
void DrawLine(int &x1 , int &y_1 , int &x2 , int &y2)
{

     float dx=x2-x1;
     float dy=y2-y_1;
     float steps=max(abs(dx) , abs(dy) );
     float xn=dx/steps;
     float yn=dy/steps;
     
     float x=x1;
     float y=y_1;
     glBegin(GL_POINTS);
         bool printed=false;
         for(int i=0;i<=steps;i++)
         {
             glVertex2f(round(x), round(y));
             if(!printed)
             {
                cout<<"("<<round(x)<<" "<<round(y)<<")"<<endl;
             }
             x=x+xn;
             y=y+yn;
        }
     printed=true;
     glEnd();
     glFlush();   
}
void Display()
{
     glClear(GL_COLOR_BUFFER_BIT);
      glLoadIdentity();
      glPointSize(3);
         glTranslatef(200,300 ,0);
         DrawLine( x1 , y_1 , x2 , y2);
     glFlush();
}
void MyInit()
{
   glClearColor(0,0,0,0);
   
   glMatrixMode(GL_PROJECTION);
   glLoadIdentity();
   gluOrtho2D(0,600,0,600);
   glMatrixMode(GL_MODELVIEW);
}
int main(int c , char* v[])
{
      cout<<"enter first point\n";
      cin>>x1>>y_1;
      cout<<"enter lasta point \n";
      cin>>x2>>y2;
      glutInit(&c , v);
      glutInitWindowSize(600,600);
      glutInitDisplayMode(GLUT_RGB | GLUT_SINGLE);
      glutCreateWindow(" Line drawing algorithm ");
      
      MyInit();
      glutDisplayFunc(Display);
      glutMainLoop();
      return 0;
}



bresenham slgorithm

#include <GL/glut.h>
#include <iostream>
#include <cmath>
using namespace std;

int x1,y_1 , x2, y2;
bool printed=true;
void Bresenham(int &x1 , int &y_1 , int &x2 , int y2)
{
    float dx=x2-x1;
    float dy=y2-y_1;
    float m=dy/dx;
    
    float x=x1;
    float y=y_1;
    float p0=2*dy-dx;
    glBegin(GL_POINTS);
    if(m<1){
        
        for(int i=0;i<=abs(dx);i++){
        
             if(p0<0){
                 glVertex2i(round(x) , round(y));
                 if(printed==true)
                 cout<<"("<<round(x)<<","<<round(y)<<")"<<endl;
                 
                 x=x+1;
                 y=y;
                 p0=p0+2*dy;
             }else{
               
                glVertex2i(round(x) , round(y));
                 
                 y=y+1;  
                 x=x+1;
                 p0=p0+2*dy-2*dx;
             }
        }
    }else{
        
        for(int i=0;i<=abs(dy);i++){
        
             if(p0<0){
                  glVertex2i(round(x) , round(y));
                  if(printed==true)
                      cout<<"("<<round(x)<<","<<round(y)<<")"<<endl;
                    
                  y=y+1;
                  x=x;
                  p0=p0+2*dx;
                      
             }else{
             
                  glVertex2i(round(x) , round(y));
                  x=x+1;
                  y=y+1;
                  p0=p0+2*dx-dy;
             }
        }
        printed=false;
    }
    glEnd();
    glFlush();
}
void display()
{
    glClear(GL_COLOR_BUFFER_BIT);
    glColor3f(1.0, 1.0, 1.0);

    Bresenham(x1 , y_1 , x2 , y2);

    glFlush();
}

void init()
{
    glClearColor(0.0, 0.0, 0.0, 1.0);
    glMatrixMode(GL_PROJECTION);
    glLoadIdentity();
    gluOrtho2D(-10,10,-10,10);
}

int main(int argc, char** argv)
{
    cout<<"Enter start point\n";
    cin>>x1>>y_1;
    cout<<"Enter end point\n";
    cin>>x2>>y2;
    
    glutInit(&argc, argv);
    glutInitDisplayMode(GLUT_SINGLE | GLUT_RGB);
    glutInitWindowSize(500, 500);
    glutCreateWindow("Bresenham Line Drawing");

    init();
    glutDisplayFunc(display);
    glutMainLoop();

    return 0;
}

// dotted line


#include <GL/glut.h>

void display() {
    glClear(GL_COLOR_BUFFER_BIT);
    glColor3f(1,1,0);
    
    glEnable(GL_LINE_STIPPLE);
       glLineStipple(1,0x0101);
           glBegin(GL_LINES);
              glVertex2i(100 ,250);
              glVertex2i(400,250);
           glEnd();
    glDisable(GL_LINE_STIPPLE);
    glFlush();
}

void init() {
    glClearColor(0, 0, 0, 0);
    glMatrixMode(GL_PROJECTION);
    glLoadIdentity();
    gluOrtho2D(0, 500, 0, 500);
}

int main(int argc, char** argv) {
    glutInit(&argc, argv);
    glutInitWindowSize(800, 800);
    glutInitDisplayMode(GLUT_RGB | GLUT_SINGLE);
    glutCreateWindow("Dotted Line");

    init();

    glutDisplayFunc(display);
    glutMainLoop();
}

// dashed line 

#include <GL/glut.h>

void display() {
    glClear(GL_COLOR_BUFFER_BIT);

    glColor3f(1, 1, 1); // White color

    // Enable dashed line
    glEnable(GL_LINE_STIPPLE);

    // Pattern define (dashed)
    glLineStipple(1, 0x00FF);

    glBegin(GL_LINES);
        glVertex2i(100, 250);
        glVertex2i(400, 250);
    glEnd();

    glDisable(GL_LINE_STIPPLE);

    glFlush();
}

void init() {
    glClearColor(0, 0, 0, 1);
    gluOrtho2D(0, 500, 0, 500);
}

int main(int argc, char** argv) {
    glutInit(&argc, argv);
    glutInitWindowSize(500, 500);
    glutCreateWindow("Dashed Line");

    init();

    glutDisplayFunc(display);

    glutMainLoop();
}

// hello print

#include <GL/glut.h>

void display() {
    glClear(GL_COLOR_BUFFER_BIT);
    glLineWidth(4);
    glColor3f(1, 0, 0); // White color

   glPushMatrix();
    // Position set
    glTranslatef(50, 50, 0);
    //glScalef(1, 1, 1);
    glutStrokeCharacter(GLUT_STROKE_ROMAN, 'H');
    glutStrokeCharacter(GLUT_STROKE_ROMAN, 'E');
    glutStrokeCharacter(GLUT_STROKE_ROMAN, 'L');
    glutStrokeCharacter(GLUT_STROKE_ROMAN, 'L');
    glutStrokeCharacter(GLUT_STROKE_ROMAN, 'O');

  glPopMatrix();

    glFlush();
}

void init() {
    glClearColor(0, 0, 0, 1); // Black background
    gluOrtho2D(0, 800, 0, 800);
}

int main(int argc, char** argv) {
    glutInit(&argc, argv);
    glutInitWindowSize(800, 800);
    glutCreateWindow("HELLO Stroke Font");

    init();

    glutDisplayFunc(display);

    glutMainLoop();
}

