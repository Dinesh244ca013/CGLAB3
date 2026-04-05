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
