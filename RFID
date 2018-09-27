#include <xc.h>
#include <CONFIGBITS.h>
#define _XTAL_FREQ 16000000

void uart_init(unsigned long);
unsigned char uart_rec();
void uart_send(unsigned char);
void uart_num(unsigned int);
void uart_string(unsigned char*);

void uart_init(unsigned long baud)
{
    unsigned int n;
    TXSTA = 0x00;
    RCSTA = 0x00;
    SYNC = 0;               // Asynchronous mode
    BRG16 = 1;              // Use SPBREGH and SPBREG
    SPEN = 1;           // Enable tx and rx pins
    CREN = 1;           // Enable continous receive mode
    BRGH = 1;           // High Speed transmission enable
    TXEN = 1;           // Enable transmission
    
    n = ((_XTAL_FREQ/4)/baud) - 1;
    SPBRGH = (n>>8);
    SPBRG = n & 0xFF;
    
   
}

unsigned char uart_rec()
{
    while(!RCIF);	//Wait for a byte
	
	return RCREG;
}



void main(void)
{
    TRISA=0x00;
    TRISC=0xFF;
    uart_init(9600);
    unsigned char count=0,count1=0;
    unsigned char enter[15],str[]="stop",str1[]="pass";
    enter[15]=uart_rec();
    unsigned char pass[15]="0D0076C7EF52";
    
    for(int i=0;i<12;i++)
    {
      if(enter[i]==pass[i])
      {
          count++;
      }
      
      else
      {
          count1++;
          
      }
    }
    
    if(count==12)
    {
        PORTAbits.RA3=1;
        while(1);
    }
    return;
}
