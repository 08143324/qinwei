#include<stdio.h>
#include<conio.h>
#include "ApiExusb.h"
#pragma comment(lib,"ApiExusb.lib")
char w1[13]={0xb5,0xc7,0xc2,0xb2,0xc4,0xb1,0xc2,0xb2,0xd7,0xcc,0xcd,0xc9,0xcf};
char w2[13]={0xb1,0xb0,0xa5,0xe3,0xbf,0xea,0xa5,0xe3,0xb4,0xac,0xa3,0xcf,0xc2};
char lcd[4]={0xb1,0xb2,0xb3,0xb4};
int zt=1;
int a[4]={0,0,0,0};
int b[4]={0,0,0,0};
int p=1,l=1,s=0,m=0,g=0;
int buf = 0x33;
void clear();
void cmdsetup();
void datasetup();
void clean1()
{
	PortWriteByte(0x28b, 0x81);		/*设置8255的A口C口均为输出*/
	clear();
	Sleep(50);
	int y;
	clear();
	PortWriteByte(0x288, 0x84);
	cmdsetup();
	Sleep(10);
	for (y = 0; y<1; y++)
	{
		PortWriteByte(0x288, 0xA1);
		datasetup();
		PortWriteByte(0x288, 0xA0);
		datasetup();
	}
	Sleep(10);
}
void clean2()
{
	PortWriteByte(0x28b, 0x81);		/*设置8255的A口C口均为输出*/
	clear();
	Sleep(50);
	int y;
	clear();
	PortWriteByte(0x288, 0x94);
	cmdsetup();
	Sleep(10);
	for (y = 0; y<1; y++)
	{
		PortWriteByte(0x288, 0xA1);
		datasetup();
		PortWriteByte(0x288, 0xA0);
		datasetup();
	}
	Sleep(10);
}
void clean3()
{
	PortWriteByte(0x28b, 0x81);		/*设置8255的A口C口均为输出*/
	clear();
	Sleep(50);
	int y;
	clear();
	PortWriteByte(0x288, 0x8c);
	cmdsetup();
	Sleep(10);
	for (y = 0; y<1; y++)
	{
		PortWriteByte(0x288, 0xA1);
		datasetup();
		PortWriteByte(0x288, 0xA0);
		datasetup();
	}
	Sleep(10);
}
void show()
{
	PortWriteByte(0x28b, 0x81);		/*设置8255的A口C口均为输出*/
	clear();

         clear();
         PortWriteByte(0x288,0x80);
         cmdsetup();


//mu
            PortWriteByte(0x288,w1[4]);
			datasetup();
			PortWriteByte(0x288,w2[4]);
			datasetup();
//biao
            PortWriteByte(0x288,w1[5]);
			datasetup();
			PortWriteByte(0x288,w2[5]);
			datasetup();
//lou
            PortWriteByte(0x288,w1[6]);
			datasetup();
			PortWriteByte(0x288,w2[6]);
			datasetup();
//ceng

            PortWriteByte(0x288,w1[7]);
			datasetup();
			PortWriteByte(0x288,w2[7]);
			datasetup();
         clear();
         PortWriteByte(0x288,0x90);
         cmdsetup();

//zhuang
            PortWriteByte(0x288,w1[8]);
			datasetup();
			PortWriteByte(0x288,w2[8]);
			datasetup();
//tai
            PortWriteByte(0x288,w1[9]);
			datasetup();
			PortWriteByte(0x288,w2[9]);
			datasetup();


         clear();
         PortWriteByte(0x288,0x88);
         cmdsetup();

 //dang
            PortWriteByte(0x288,w1[0]);
			datasetup();
			PortWriteByte(0x288,w2[0]);
			datasetup();
 //qian
                  PortWriteByte(0x288,w1[1]);
			datasetup();
			PortWriteByte(0x288,w2[1]);
			datasetup();
//lou
            PortWriteByte(0x288,w1[2]);
			datasetup();
			PortWriteByte(0x288,w2[2]);
			datasetup();
//ceng
PortWriteByte(0x288,w1[3]);
			datasetup();
			PortWriteByte(0x288,w2[3]);
			datasetup();
         clear();
         PortWriteByte(0x288,0x90);
         cmdsetup();
         Sleep(10);
    }
void zhuangtaixianshihanshu()         //显示电梯当前状态
{
         PortWriteByte(0x28b, 0x81);		/*设置8255的A口C口均为输出*/
	 clear();

	 clear();
         PortWriteByte(0x288,0x94);
         cmdsetup();

         if(zt==0)
         {
                  PortWriteByte(0x288,w1[12]);
			datasetup();
			PortWriteByte(0x288,w2[12]);
			datasetup();
         }
         else if(zt==1)
         {
                  PortWriteByte(0x288,w1[10]);
			datasetup();
			PortWriteByte(0x288,w2[10]);
			datasetup();
        }
         else if(zt==2)
         {
                  PortWriteByte(0x288,w1[11]);
			datasetup();
			PortWriteByte(0x288,w2[11]);
			datasetup();
         }
}
void mubiaoloucengxianshihanshu()             //显示目标楼层
{

    PortWriteByte(0x28b, 0x81);		/*设置8255的A口C口均为输出*/
	clear();

	   clear();
         PortWriteByte(0x288,0x84);
         cmdsetup();

	   PortWriteByte(0x288,0xa3);
         datasetup();
         PortWriteByte(0x288,lcd[l-1]);
         datasetup();
}
void dangqianloucengxianshihanshu()             //显示当前楼层
{
      clean3();
      PortWriteByte(0x28b, 0x81);		/*设置8255的A口C口均为输出*/
	clear();

	     clear();
         PortWriteByte(0x288,0x8c);
         cmdsetup();

	     PortWriteByte(0x288,0xa3);
         datasetup();
         PortWriteByte(0x288,lcd[p-1]);
         datasetup();
}
void panduanshangshengshifoujieshu()                //判断上升是否结束
{
for(int x=p-1;x<4;x++)
{
    if(a[x]==0)
    {
        if(x==3)
        {
          s=4;
          x=4;
        }
    }
    else if(a[x]==1)
    {
        s=m;
        l=x+1;
        x=4;
    }
}
}
void panduanxiajiangshifoujieshu()          //判断下降是否结束
{
    for(int y=p-1;y>=0;y--)
    {
        if(b[y]==0)
        {
           if(y==0)
            {   g=-1;
                y=-1;
             }
        }
        else if(b[y]==1)
        {
            g=m;
            l=y+1;
            y=-1;
        }
    }
}
void bujindianji()
{     byte dat;
      PortWriteByte(0x283,0x36);/*通道0控制字，先读写低字节，后读写高字节，方式2，*/
      PortWriteByte(0x280,1000%256);
      PortWriteByte(0x280,1000/256);/*初始化通道0,2000*/
      PortWriteByte(0x283,0x76);/*通道1控制字，先读写低字节，后读写高字节，方式1，*/
      PortWriteByte(0x281,1000%256);
      PortWriteByte(0x281,1000/256);/*初始化通道1,500*/
      PortWriteByte(0x28b,0x89);
      PortReadByte(0x28a,&dat);
      printf("%d",dat);
      printf("s");
      BYTE	data;
	int d;
      int m=0;
      int buf1;
      int buf2;
	while(dat&0x10)
	{	if (zt==1)
            {
            d = 0;
             }
		else if (zt==2)
            {
             d = 20;
             data=0x80;
             }
            else if(zt==0)
            {
             d=20;
             data=0x00;
            }

		if (d != 0)
		  {
			Sleep(d);
			if (data & 128)
				{buf = ((buf&1)<<7)|(buf>>1);}
			else
				{buf = ((buf&128)>>7)|(buf<<1);}
                  buf1=buf&0xf0;
                  buf2=buf1|0x01;
			PortWriteByte(0x289,buf2);
                 PortReadByte(0x28a,&dat);
		   }
		else
              {
                  Sleep(200);
			PortWriteByte(0x289,0xf1);
                PortReadByte(0x28a,&dat);

              }
      PortReadByte(0x28a,&dat);
      printf("%d",dat);
	}

}

void  clear()
{
	PortWriteByte(0x288, 0x0c);
	cmdsetup();
}
void cmdsetup()
{
	PortWriteByte(0x289, 0x00);
	Sleep(1);
	PortWriteByte(0x289, 0x04);
	Sleep(1);
	PortWriteByte(0x289, 0x00);
	Sleep(1);
}
void datasetup()
{
	PortWriteByte(0x289, 0x01);
	Sleep(1);
	PortWriteByte(0x289, 0x05);
	Sleep(1);
	PortWriteByte(0x289, 0x01);
	Sleep(1);
}
void main()
{
	printf("Start!\n");
	if (!Startup())			/*打开设备*/
	{
		printf("ERROR: Open Device Error!\n");
		return;
	}
	while (!kbhit())
	{
                 show();
                 zhuangtaixianshihanshu();
                 mubiaoloucengxianshihanshu();
                 dangqianloucengxianshihanshu();

                 byte data;
	         byte i, j;
	         byte k;
	        PortWriteByte(0x28b, 0x81);		/*设置8255的A口C口均为输出*/
		clear();
		Sleep(50);
		PortWriteByte(0x28a, 0x0f);
		cmdsetup();
		PortReadByte(0x28a, &data);
		i = data;
		if (i != 0x0f)
		{
			i = data;
			Sleep(50);
			PortWriteByte(0x28b, 0x88);
			PortWriteByte(0x28a, 0xf0);
			PortReadByte(0x28a, &data);
			i = i | data;
			clear();
			PortWriteByte(0x288, 0x91);
			cmdsetup();
			if (i == 0x77)
			{
				k = 1;
                        if(k<p)
                       {
                            b[k-1]=1;
                        }

			}
			else if (i == 0x7b)
			{
				k = 1;
				if(k<p)
                        {b[k-1]=1;}


			}
			else if (i == 0x7d)
			{
                k = 2;
				if(k<p)
                {b[k-1]=1;}
                else if(k>p)
                {a[k-1]=1;}


			}
			else if (i == 0x7e)
			{
				k = 3;
				if(k<p)
                {b[k-1]=1;}
                else if(k>p)
                {a[k-1]=1;}

			}
			else if (i == 0xb7)
			{
				k = 4;
				if(k<p)
                {b[k-1]=1;}
                else if(k>p)
                {a[k-1]=1;}

			}
			else if (i == 0xbb)
			{
				k = 2;
				if(k<p)
                {b[k-1]=1;}
                else if(k>p)
                {a[k-1]=1;}

			}
			else if (i == 0xbd)
			{
				k = 2;
				if(k<p)
                {b[k-1]=1;}
                else if(k>p)
                {a[k-1]=1;}

			}
			else if (i == 0xbe)
			{
				k = 3;
				if(k<p)
                {b[k-1]=1;}
                else if(k>p)
                {a[k-1]=1;}

			}
			else if (i == 0xd7)
			{
				k = 3;
				if(k<p)
                {b[k-1]=1;}
                else if(k>p)
                {a[k-1]=1;}

			}
			else if (i == 0xdb)
			{
				k = 4;
				if(k>p)
                {a[k-1]=1;}

			}
			else if (i == 0xdd) //A  关门
			{
				k = 10;
			}
			else if (i == 0xde) // B 开门
			{
				k = 11;
			}

		}
        m=p-1;

        while(m<=3)
          {

                byte data;
	        byte i, j;
	        byte k;
	        PortWriteByte(0x28b, 0x81);		/*设置8255的A口C口均为输出*/
		clear();
		Sleep(50);
		PortWriteByte(0x28a, 0x0f);
		cmdsetup();
		PortReadByte(0x28a, &data);
		i = data;
		if (i != 0x0f)
		{
			i = data;
			Sleep(50);
			PortWriteByte(0x28b, 0x88);
			PortWriteByte(0x28a, 0xf0);
			PortReadByte(0x28a, &data);
			i = i | data;
			clear();
			PortWriteByte(0x288, 0x91);
			cmdsetup();
			if (i == 0x77)
			{
				k = 1;
                        if(k<p)
                       {
                            b[k-1]=1;
                        }

			}
			else if (i == 0x7b)
			{
				k = 1;
				if(k<p)
                        {b[k-1]=1;}


			}
			else if (i == 0x7d)
			{
                k = 2;
				if(k<p)
                {b[k-1]=1;}
                else if(k>p)
                {a[k-1]=1;}


			}
			else if (i == 0x7e)
			{
				k = 3;
				if(k<p)
                {b[k-1]=1;}
                else if(k>p)
                {a[k-1]=1;}

			}
			else if (i == 0xb7)
			{
				k = 4;
				if(k<p)
                {b[k-1]=1;}
                else if(k>p)
                {a[k-1]=1;}

			}
			else if (i == 0xbb)
			{
				k = 2;
				if(k<p)
                {b[k-1]=1;}
                else if(k>p)
                {a[k-1]=1;}

			}
			else if (i == 0xbd)
			{
				k = 2;
				if(k<p)
                {b[k-1]=1;}
                else if(k>p)
                {a[k-1]=1;}

			}
			else if (i == 0xbe)
			{
				k = 3;
				if(k<p)
                {b[k-1]=1;}
                else if(k>p)
                {a[k-1]=1;}

			}
			else if (i == 0xd7)
			{
				k = 3;
				if(k<p)
                {b[k-1]=1;}
                else if(k>p)
                {a[k-1]=1;}

			}
			else if (i == 0xdb)
			{
				k = 4;
				if(k>p)
                {a[k-1]=1;}

			}
			else if (i == 0xdd) //A  关门
			{
				k = 10;
			}
			else if (i == 0xde) // B 开门
			{
				k = 11;
			}

		}

            panduanshangshengshifoujieshu();

            m=s;
            if(m>3){break;}
            if(a[m]==1)
            {
                 zt=1;

                 mubiaoloucengxianshihanshu();
                 dangqianloucengxianshihanshu();
                 a[m]=0;
                 zhuangtaixianshihanshu();
                 if(m=3)
                 {m=m+1;}

            }
             else if(a[m]==0)
            {
                 zt=2;

                 mubiaoloucengxianshihanshu();
                 dangqianloucengxianshihanshu();
                 p=p+1;
                 m=m+1;
                 zhuangtaixianshihanshu();
                 bujindianji();
            }
           }

        m=p-1;
        while(m>=0)
        {
                byte data;
	        byte i, j;
	        byte k;
	        PortWriteByte(0x28b, 0x81);		/*设置8255的A口C口均为输出*/
		clear();
		Sleep(50);
		PortWriteByte(0x28a, 0x0f);
		cmdsetup();
		PortReadByte(0x28a, &data);
		i = data;
		if (i != 0x0f)
		{
			i = data;
			Sleep(50);
			PortWriteByte(0x28b, 0x88);
			PortWriteByte(0x28a, 0xf0);
			PortReadByte(0x28a, &data);
			i = i | data;
			clear();
			PortWriteByte(0x288, 0x91);
			cmdsetup();
			if (i == 0x77)
			{
				k = 1;
                        if(k<p)
                       {
                            b[k-1]=1;
                        }

			}
			else if (i == 0x7b)
			{
				k = 1;
				if(k<p)
                        {b[k-1]=1;}


			}
			else if (i == 0x7d)
			{
                k = 2;
				if(k<p)
                {b[k-1]=1;}
                else if(k>p)
                {a[k-1]=1;}


			}
			else if (i == 0x7e)
			{
				k = 3;
				if(k<p)
                {b[k-1]=1;}
                else if(k>p)
                {a[k-1]=1;}

			}
			else if (i == 0xb7)
			{
				k = 4;
				if(k<p)
                {b[k-1]=1;}
                else if(k>p)
                {a[k-1]=1;}

			}
			else if (i == 0xbb)
			{
				k = 2;
				if(k<p)
                {b[k-1]=1;}
                else if(k>p)
                {a[k-1]=1;}

			}
			else if (i == 0xbd)
			{
				k = 2;
				if(k<p)
                {b[k-1]=1;}
                else if(k>p)
                {a[k-1]=1;}

			}
			else if (i == 0xbe)
			{
				k = 3;
				if(k<p)
                {b[k-1]=1;}
                else if(k>p)
                {a[k-1]=1;}

			}
			else if (i == 0xd7)
			{
				k = 3;
				if(k<p)
                {b[k-1]=1;}
                else if(k>p)
                {a[k-1]=1;}

			}
			else if (i == 0xdb)
			{
				k = 4;
				if(k>p)
                {a[k-1]=1;}

			}
			else if (i == 0xdd) //A  关门
			{
				k = 10;
			}
			else if (i == 0xde) // B 开门
			{
				k = 11;
			}

		}
          panduanxiajiangshifoujieshu();
          m=g;
          if(m<0)
          {break;}
          if(b[m]==1)
          {
                 zt=1;
                 mubiaoloucengxianshihanshu();
                 dangqianloucengxianshihanshu();
                 b[m]=0;
                 zhuangtaixianshihanshu();

            }
             else if(b[m]==0)
            {
                 zt=0;
                 mubiaoloucengxianshihanshu();
                 dangqianloucengxianshihanshu();
                 p=p-1;
                 m=m-1;
                 zhuangtaixianshihanshu();
                 bujindianji();
             }
       }
    }
Cleanup();
}
