# Ex. No. :08 --Interfacing-Seven-segment-display-with-lpc2148

Name:Srinivas.u


Roll no:212221230108


## Aim: 
To configure and display 4 character LED seven segment display and write a c code for displaying number 1 to 9 and A to F 
## Components required:
Proteus ISIS professional suite, Kiel μ vision 5 Development environment 
 ![image](https://user-images.githubusercontent.com/36288975/201021692-efa39349-1a3c-4737-aadc-1843b954c78d.png)
Figure-01 Internal circuit for seven segment MPX4 display

## Theory: 

7 Segment Display has seven segments in it and each segment has one LED inside it to display the numbers by lighting up the corresponding segments. Like if you want the 7-segment to display the number "5" then you need to glow segment a,f,g,c, and d by making their corresponding pins high. There are two types of 7-segment displays: Common Cathode and Common Anode, here we are using Common Cathode seven segment display.

   ![image](https://user-images.githubusercontent.com/36288975/201021740-565b47cd-26d8-4e54-a092-eef7a0a85278.png)
 
          Figure-02 Pin configuration for seven segment display  


Below table shows the HEX values and corresponding digit according to LPC2148 pins for common cathode configuration.


![image](https://user-images.githubusercontent.com/94233985/201413708-cbfa5805-76df-42eb-b386-dd40b651ec7b.png)



![image](https://user-images.githubusercontent.com/36288975/201021930-7efe2b15-b0de-4d52-b87d-329fe6b91c89.png)
        Figure -3 Circuit diagram of interfacing for LPX4 - CA

## Kiel - Program:
```
#include <LPC214x.h>
unsigned char dig[]={0x88,0xeb,0x4c,0x49,0x2b,0x19,0x18,0xcb,0x8,0x9,0xa,0x38,0x9c,0x68};
	void delay(unsigned int count)
	{
		int j=0,i=0;
		for(j=0;j<count;j++)
		{
			for(i=0;i<120;i++);
		}
	}
	int main(void)
	{
		unsigned char count=0;
		unsigned int i=0;
		IO0DIR|=(1<<11);//Set Digit control lines as Outputs
		IO0SET=(1<<11);
		IO0DIR|=0x007F8000;
		while(1)
		{
			count++;
			if(count==16)count=0;
			for(i=0;i<800;i++)//change to inc/dec speed of count
			{
				IO0CLR=0x007F8000;
				IO0SET=(dig[count]<<15);
				delay(200);
			}
		}
	}
```


##  Output screen shots :
### Before Simulation:
![image](https://user-images.githubusercontent.com/94233985/201414316-1073d8bf-5ec6-4ffc-b5db-b8efd10454c7.png)



### After Simulation:
![image](https://user-images.githubusercontent.com/94233985/201414535-6621bdfb-1c38-493a-a202-31e826234246.png)
![image](https://user-images.githubusercontent.com/94233985/201414585-0bdea40d-1521-4472-a6de-8e4cdc6de3c6.png)


### Circuit Layout Diagram:
![image](https://user-images.githubusercontent.com/94233985/201414677-3b2c517a-a62d-405b-9f07-7c01c8aab3b8.png)



## Result :
LED seven segment display is interfaced and displayed alpha numeric characters.
