using System;
using System.Drawing;
class GEneratingImage
{
    public static void Main(string[] args)

    {

        int size =int.Parse(args[0]);                       // command line arguments
        int nCols = int.Parse(args[1]);
        int nRows = int.Parse(args[2]);

                                 
        Bitmap bmp = new Bitmap(size * nCols, size * nRows); //creating canvas. size depends from command line

      
        int x = 0 ;                                           //starting coordinates  
        int y =0;                                             //starting coordinates    
        int sy = 0;                                           //starting coordinates for rotation matrix   
        int sx = size;                                        //starting coordinates for rotation matrix  
        int minx = size;                                      //min value for x while drawing horizontal line from right to left  
        int miny = 2*size;                                    //min value for y while drawing vertical line from bottom to top
        int maxx = bmp.Width - size;                          //max value for x while drawing horizontal line from left to right  
        int maxy = bmp.Height - size;                         //max value for y while drawing vertical line from top to bottom  
        bool draw;                                            //logical value for stop drawing   
        do
        {
            draw= false;
            while ((x < maxx && sx>0) ||                       //conditions for choose in which way drawing a line 
                    (x>minx && sx<0)||
                    (y < maxy && sy>0)||
                    (y>miny && sy<0))
            {
                DrawBlackSquare(bmp, x, y, size);               //drawing 1 square
                x += sx;                                        //iterating line
                
                y += sy;
                

                draw = true;
            }
            if (sx < 0) minx = x + 2*size;                      //incremanting or dicremanting max and min values
            if (sx > 0) maxx = x - 2*size;
            if (sy < 0) miny = y + 2*size;
            if (sy > 0) maxy = y - 2*size;


            int temp = sx;                                      //rotation matrix for rotate the line
            sx = -sy;
            sy = temp;
        } while (draw);



        void DrawBlackSquare(Bitmap bitmap, int i, int j, int s)// function for drawing one square
        {
            
            for (int a = i; a< i+s ; a++)
            {
                for (int b = j; b < j + s; b++)
                {
                    if (a < bitmap.Width && b < bitmap.Height)
                        bitmap.SetPixel(a, b, Color.FromArgb(255, 0, 0, 0));
                    else return;
                }
            }
        }

        bmp.Save("Charli.bmp");


    }
}
