#include <iom128v.h>
#include <avrdef.h>

void delay_ms(unsigned int m);
void delay_us(unsigned int u);
void write_data(char d);
void write_instruction(char k);
void init_lcd(void);
    int i;
    int o; //전역변수


void main(void)
{
    DDRA=0xff;  //a포트의 모든핀을 출력으로 사용
    DDRE =0x07; //e포트의 하위3개핀을 출력으로 사용
    DDRB = 0xff;
    DDRC = 0xff; //B와C포트 출력선언
    DDRD=0xf0; // d는 입력
    init_lcd();

int segment[10] = { 0b11000000,
	0b11111001,
	0b10100100 ,
	0b10110000  ,
	0b10011001   ,
	0b10010010 ,
	0b10000010  ,
	0b11111000   ,
	0b10000000 ,
	0b10010000,
};



    while(1)
    {if(0x00 != (PIND & 0x01) ){
    i++; // 스위치가 눌렸을때 1씩 추가
    PORTB = segment[i%10]; // 10으로 나눈후의 나머지를 출력
    delay_ms(10);
    }
    else if (0x00 != (PIND & 0x02) ){
    o++;
    PORTC = segment[o%10];
    delay_ms(10);

        }

    int d = i;
    int q = o;
        write_instruction(0x80);  //clcd의 위치지정
        write_data('t');          //data 출력
        write_instruction(0x81);  
        write_data('e');         
        write_instruction(0x82);  
        write_data('n');
        write_instruction(0x83);
        write_data('s');
        write_instruction(0x84);
        write_data(0x30 + d); //  푸시버튼을 누를때마다 o값이 증가,> 아스키코드0에서시작 1씩증가
        write_instruction(0xc0);  
        write_data('o');         
        write_instruction(0xc1);  
        write_data('n');         
        write_instruction(0xc2); 
        write_data('e');
        write_instruction(0xc3);
        write_data('s');
        write_instruction(0xc4);
        write_data(0x30 +q);
        }
        }


void init_lcd(void)        //lcdc 초기화 함수
{
    delay_ms(10);
    write_instruction(0x30);
    delay_ms(25);
    write_instruction(0x30);
    delay_ms(5);
    write_instruction(0x30);
    delay_ms(5);
    write_instruction(0x3c);
    delay_ms(5);
    write_instruction(0x08);
    delay_ms(5);
    write_instruction(0x01);
    delay_ms(5);
    write_instruction(0x06);
    delay_ms(5);
    write_instruction(0x0c);
    delay_ms(15);

    }

void write_instruction(char k)  //인스터럭션 함수 정의
    {
        PORTE=0x04;    //enable signal(상승 >>하강엣지에서 쓰기동작을 할수있게) ,상승엣지
        delay_us(10);
        PORTA=k;        //명령어 데이터 출력
        delay_us(10);
        PORTE=0x00;    // 하강엣지
        delay_us(100);
        }

void write_data(char d)
{
    PORTE=0x05;
        delay_us(10);
        PORTA=d;     //명령어 데이터 출력
        delay_us(10);
        PORTE=0x01;   //하강엣지
        delay_us(100);
        }


void delay_ms(unsigned int m)  //딜레이 선언
{
  unsigned int ii,jj;
  for(ii=0;ii<m;ii++)
  {
    for(jj=0;jj<2117;jj++);
  }
}
void delay_us(unsigned int u)
{
  unsigned int ii,jj;
  for(ii=0;ii<u;ii++)
  {
    for(jj=0;jj<2117;jj++);
  }
}
