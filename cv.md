# *Curriculum Vitae*
## Personal information
* Name: Stanislav Kulikovsky
* Address: 42 Tavlaya Street, apt. 90, Grodno, 230005, Belarus.
* Phone number: +375 (33) 621 33 60
* Marital status: single
* Date of birth: 5th September 1995
* Email: 1232312009qq@gmail.com
## Objective
To obtain employment in the field of IT to use my technical mindset and ability to learn quickly.
## Work experience 
I gained some experience in electronics and low-level programming while working in a research lab.
##Education
Yanka Kupala State University of Grodno. Specialty: Information and Measuring Equipment
##Special skills
* Language skills:
  + Russian (native)
  + Polish (fluent,except writing)
  + English (A2+)
* Programming skills:
  + Low-level programming of STM and PIC controllers in Basic, C, and C++ languages.
  + basic level of programming C++, C#, Java, Basic
* Special computer literacy:
  + Proteus
  + Autocad
* Driving license: +
## Example of simple C code for the PIC controller
```C
#define COMP (CMCON&0b10000000)>>7  
#define OTKRYT RB2_bit  
#define ZAKRYT RB3_bit
#define VINT RB4_bit  
#define LAMP RB5_bit    

unsigned short ocount, zcount;  
void error(){
  RB1_bit=0;
  RB0_bit=0;
    do{                            
      Sound_play(800,250);            
      Delay_ms(500);                 
    }while(1);                      
}
void otkr(){
  LAMP=1;                       
  RB1_bit=0;                  
  RB0_bit=1;                     
  Delay_ms(100);              
  RB1_bit=1;               
  ocount=0;                      
  do{                         
    ocount++;                       
    Delay_ms(1000);                
  }while(OTKRYT==0&&ocount<10);  
  if (OTKRYT==0&&ocount>9)error();
  if (OTKRYT==1)RB1_bit=0;        
  RB0_bit=0;
}
void zakr(){
  RB0_bit=0;                  
  Delay_ms(100);                 
  RB1_bit=1;               
  zcount=0;                      
  do{                          
    zcount++;                     
    Delay_ms(1000);                 
  }while(ZAKRYT==0&&zcount<10); 
  if (ZAKRYT==0&&zcount>9)error();
  if (ZAKRYT==1)RB1_bit=0;      
}


void main() {                   
  Sound_init(&PORTA,0);        
  CMCON=0b00100101;             
  TRISA=0x06;                   
  TRISB=0x0C;                  
  PORTA=0;                     
  PORTB=0;                   
  VRCON=0b11100100;             
  if(COMP==1)LAMP=1;            
  do {                             
    Delay_ms(250);                   
    VRCON=0b11100101;             
    Delay_ms(250);                  
    if(COMP==1&&OTKRYT==0)otkr();   
    Delay_ms(250);                   
    VRCON=0b11100100;             
    Delay_ms(250);                   
    if(COMP==0&&ZAKRYT==0)zakr();
    if(OTKRYT==0&&ZAKRYT==0)zakr();
    if(OTKRYT==1&&ZAKRYT==1)error();
    if(OTKRYT==1&&VINT==0)VINT=1;
    if(ZAKRYT==1&&VINT==1)VINT=0;
  } while(1);                        
}
```

