# sem-foro2.0
Semáforo tinkercad SENAI Rc
/***********************************************************************
*                Semáforo sem "Delay" + Cruzamento                     |
*                                                                      |
*         Elaborado por: Pedro F. Salles                               |
*         versão 1.0                                                   |
*         Data: 17/09/2020 - 24/09/2020                                |
*                                                                      |
*    atualizado em 01/10/2020                                          |
*                                                                      |
*                                                                      |
*                                                                      |
*   Descrição: Exercicio elaboração de um semáforo                     |
*                                                                      |
*         >>>PINAGEM<<<                                                |
*            led = 4;                                                  |
*            led = 7;                                                  |
*            led = 11;                                                 |
***********************************************************************/





unsigned long tempo2 = 0;    		// Define o tempo do pisca juntamente do millis
unsigned long pisca = 500; 		 // Define o tempo que vai piscar
bool status = 0;  		//status do botao

byte button = 2; 		 //pino do botao

byte vm1 = 11;  		//pino do led
byte vd1 = 4; 		//pino do led
byte am1 = 7;		 //pino do led

byte vm2 = 10; 		 //pino do led
byte vd2 = 3;		 //pino do led
byte am2 = 6; 		//pino do led

unsigned long vermT = 5000; 		// tempo que o led vai ficar asceso
unsigned long amaT = 2000;  		//tempo que o led vai ficar asceso
unsigned long verdT = 3000;		 //tempo que o led vai ficar asceso

unsigned long tempoSem = 0;		 // tempo do semaforo juntamente do miliis

void setup()
{
  INPUT_PULLUP; 		// liga o resistor pullup do arduino
  pinMode(button, INPUT_PULLUP); 		 // define o botao pullup

  Serial.begin(9600);

  pinMode(vm1, OUTPUT); 		//  define a variavel vm1, que mostra qual led é, define ela como saida
  pinMode(vd1, OUTPUT); 		//  define a variavel vd1, que mostra qual led é, define ela como saida
  pinMode(am1, OUTPUT); 		//  define a variavel am1, que mostra qual led é, define ela como saida

  pinMode(vm2, OUTPUT);		 //  define a variavel vm2, que mostra qual led é, define ela como saida
  pinMode(vd2, OUTPUT); 	//  define a variavel vd2, que mostra qual led é, define ela como saida
  pinMode(am2, OUTPUT);		 //  define a variavel am2, que mostra qual led é, define ela como saida
}

void loop()
{
  if (digitalRead(button))		  //  abre um comando de bloco (se) e executa em ordem. PARA O BOTAO
  {
    //********************SEMÁFORO 1*********************************
    if ((millis() - tempoSem) < vermT)  //  abre um comando de bloco (se) e executa em ordem. TEMPO DO VERMELHO
    {
      digitalWrite(vm1, HIGH);			// Ascende o led definido. Seta a variavel para HIGH/ligada
      digitalWrite(am1, LOW);			// Apaga o led definido. Seta a variavel para low/desligada
      digitalWrite(am2, LOW);			//Apaga o led definido. Seta a variavel para low/desligada
    }
    else if ((millis() - tempoSem) < (vermT + verdT)) //abre um comando de bloco (se) e executa em ordem. TEMPO DO VERDE
    {
      digitalWrite(vm1, LOW); 		//  Apaga o led definido. Seta a variavel para low/desligada
      digitalWrite(vd1, HIGH);  		//  Ascende o led definido. Seta a variavel para HIGH/ligada
    }
    else if ((millis() - tempoSem) < (vermT + verdT + amaT))  // executa de forma secundária o if anterior. Tempo do amarelo
    {
      digitalWrite(vd1, LOW); 		//  Apaga o led definido. Seta a variavel para low/desligada
      digitalWrite(am1, HIGH); 		 //  Ascende o led definido. Seta a variavel para HIGH/ligada
    }	

    //**********************SEMÁFORO 2  C R U Z A M E N T O**************
    if ((millis() - tempoSem) < verdT)  		//  abre um comando de bloco (se) e o executa em ordem. Tempo verde2
    {
      digitalWrite(vd2, HIGH); 		 //  Ascende o led definido. Seta a variavel para HIGH/ligada
    }
    else if (( millis() - tempoSem) < verdT + amaT) //
    {
      digitalWrite(vd2, LOW);   		//  Apaga o led definido. Seta a variavel para low/desligada
      digitalWrite(am2, HIGH);  		//  Ascende o led definido. Seta a variavel para HIGH/ligada
    }
    else if ((millis() - tempoSem) < vermT + amaT + verdT)  //
    {
      digitalWrite(am2, LOW); 		//  Apaga o led definido. Seta a variavel para low/desligada
      digitalWrite(vm2, HIGH);  		//  Ascende o led definido. Seta a variavel para HIGH/ligada
    }
    else
    {
      digitalWrite(am1, LOW);		 //  Apaga o led definido. Seta a variavel para low/desligada
      digitalWrite(am2, LOW);		 //  Apaga o led definido. Seta a variavel para low/desligada
      tempoSem = millis(); 		 //  Seta a variavel, atualizando-a para o tempo do contador interno, caso millis no momeno for 2, a variavel também será 2
    }
  }
     else
     {
       digitalWrite(vd1, LOW);		 //  Apaga o led definido. Seta a variavel para low/desligada
      digitalWrite(vd2, LOW); 		//  Apaga o led definido. Seta a variavel para low/desligada
      digitalWrite(vm1, LOW);		 //  Apaga o led definido. Seta a variavel para low/desligada
      digitalWrite(vm2, LOW); 		//  Apaga o led definido. Seta a variavel para low/desligada
     }
     if ((millis() - tempo2) > pisca) 		 //  Abre um comando em bloco (se). tempo que ira piscar quando o botao for pressionado
     {
      tempo2 = millis();  		//  Seta a variavel, atualizando-a para o tempo do contador interno, caso millis no momeno for 2, a variavel também será 2
      status = !status;   		//  seta o status para o inverso do mesmo, caso seja 1, ele é setado para 0, e vice versa
     }
       digitalWrite (am1, status);		 //  seta a variavel para o estado do status 0 1
       digitalWrite (am2, status); 		  //  seta a variavel para o estado do status 0 1
  
} 
