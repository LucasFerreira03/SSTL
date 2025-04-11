#include <Adafruit_LiquidCrystal.h>
#include <Servo.h>
Adafruit_LiquidCrystal lcd(0);
Servo servo;


int baseTemp=0;
int celcius=0;
int baseph=0;
int TRIG = A3; 
int ECO = A2;
int DURACION;
int DISTANCIA;

void setup()
{
  pinMode(A0, INPUT);
  pinMode(A1, INPUT);
  pinMode (TRIG, OUTPUT); // trigger como salida
  pinMode (ECO, INPUT); // echo como entrada
 
  Serial.begin(9600);
  
  pinMode(2, OUTPUT);
  pinMode(3, OUTPUT);
  pinMode(4, OUTPUT);
  pinMode(5, OUTPUT);  
  pinMode(6, OUTPUT);
  pinMode(7, OUTPUT);
  lcd.begin(16,2);
  servo.attach(8);
 
  

}

void loop()
{
  
 
  
  // LEDS TEMPERATURA 
  
  baseTemp=40;
  celcius= map(((analogRead(A1)-20)*3.04),0,1023,-40,125);
  Serial.print(celcius);
  Serial.println("C");
  
  if(celcius<baseTemp){
    digitalWrite(2,LOW);
    digitalWrite(3,LOW);
    servo.write(90);

    
    
  }
  if(celcius>=baseTemp&&celcius<baseTemp+80){
    digitalWrite(2,HIGH);
    digitalWrite(3,LOW);
    
  }
  if(celcius>baseTemp+10&&celcius<baseTemp+150){
    digitalWrite(2,HIGH);
    digitalWrite(3,HIGH);
  
  }
 if(celcius>baseTemp+20&&celcius<baseTemp+300){
    digitalWrite(2,HIGH);
    digitalWrite(3,HIGH);
    lcd.setCursor(1,0);
    lcd.print("Perigo ");
    lcd.setCursor(1,1);
    lcd.print("Temperatura");
    delay(2000);
    lcd.clear();
   	
   
  }
  
  if(celcius>baseTemp+20&&celcius<baseTemp+600){
    digitalWrite(2,HIGH);
    digitalWrite(3,HIGH);
    lcd.setCursor(1,0);
    lcd.print("Aberto valvula ");
    lcd.setCursor(1,1);
    lcd.print("de scape !!!");
    delay(2000);
    lcd.clear();
   	servo.write(0);
    delay(1000);
    
  }
  
  
 // LEDS PH
  
  
  baseTemp=40;
  celcius= map(((analogRead(A0)-20)*3.04),0,1023,-40,125);
  Serial.print(celcius);
  Serial.println("C");
  
  if(celcius<baseph){
    digitalWrite(4,LOW);
    digitalWrite(5,LOW);
     servo.write(90);
    
  }
  if(celcius>=baseph&&celcius<baseph+80){
    digitalWrite(4,HIGH);
    digitalWrite(5,LOW);
    
  }
  if(celcius>baseph+10&&celcius<baseph+300){
    digitalWrite(4,HIGH);
    digitalWrite(5,HIGH);
    
  }
 if(celcius>baseph+20&&celcius<baseph+600){
    digitalWrite(4,HIGH);
    digitalWrite(5,HIGH);
   	
    lcd.setCursor(1,0);
    lcd.print("Perigo ");
    lcd.setCursor(1,1);
    lcd.print("PH");
    delay(2000);
    lcd.clear();
   }
   
   if(celcius>baseTemp+20&&celcius<baseTemp+600){
    digitalWrite(4,HIGH);
    digitalWrite(5,HIGH);
    lcd.setCursor(1,0);
    lcd.print("Aberto valvula ");
    lcd.setCursor(1,1);
    lcd.print("de scape !!!");
    delay(2000);
    lcd.clear();
   	servo.write(0);
    delay(1000);
   	
   
  }
  
  
  // LEDS VASÃO 
  
digitalWrite(TRIG, HIGH); // generacion del pulso a enviar
  delay(1); // al pin conectado al trigger
  digitalWrite(TRIG, LOW); // del sensor

 DURACION = pulseIn(ECO, HIGH); // con funcion pulseln se espera un pulso
 // alto en Echo

 DISTANCIA = DURACION / 58.2; // distancia medida en centimetros

 Serial.println(DISTANCIA); // envio de valor de distancia por monitor serial
 delay(200); // espera| entre datos
  
  
  if (DISTANCIA < 0.5){
      lcd.print("teste");
      delay(2000);
      lcd.clear();
    }
  
  
  
  /*if (DISTANCIA >=250 & <=200 ){
    
    digitalWrite(6,LOW);
    digitalWrite(7,LOW);
    servo.write(90);
    }
  
  if (DISTANCIA <=200 ){
    
    digitalWrite(6,HIGH);
    digitalWrite(7,LOW);
    
    }
  
  if (DISTANCIA <=150 ){
    
   	digitalWrite(6,HIGH);
    digitalWrite(7,HIGH);
    }
  
  if (DISTANCIA <=100 ){
    
   	digitalWrite(6,HIGH);
    digitalWrite(7,HIGH);
   	
    lcd.setCursor(1,0);
    lcd.print("Perigo ");
    lcd.setCursor(1,1);
    lcd.print("Vasao");
    delay(2000);
    lcd.clear();
    }
  
  if (DISTANCIA <=50 ){
    
   	digitalWrite(6,HIGH);
    digitalWrite(7,HIGH);
    lcd.setCursor(1,0);
    lcd.print("Aberto valvula ");
    lcd.setCursor(1,1);
    lcd.print("de scape !!!");
    delay(2000);
    lcd.clear();
   	servo.write(0);
    delay(1000);
    }*/
  

  
  
  
  
  
  
  
  
  delay(1000);
}
