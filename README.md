#include <IRremote.h>

int receptor = 11;
int motor = 13;
IRrecv irrecv(receptor);
decode_results codigo; 
 
void setup(){
  Serial.begin(9600);
  irrecv.enableIRIn(); 
  pinMode(motor, OUTPUT);
}
void loop(){
  
  if (irrecv.decode(&codigo)){
  
Serial.println(codigo.value, HEX);

      if (codigo.value == 0xE0E0B04F){//Numero 8 para encender el motor
         digitalWrite(motor,HIGH);
         delay(8000); 
         digitalWrite(motor,LOW);
         delay(8000);
         digitalWrite(motor,HIGH);
         delay(8000);
      }     
      if (codigo.value == 0xE0E08877){//Numero 0 para apagar el motor
         digitalWrite(motor,LOW);
      }
  delay(500);
  irrecv.resume();
 }
}
