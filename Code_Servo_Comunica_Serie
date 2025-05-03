/*
-----POSICIONAMENTO DUN SERVO EMPREGANDO COMUNICACIÓN EN SERIE.----

Realiza unha montaxe na que un servo (alimentado por 
unha batería externa) se conecte no pin PWM D03 (3~) 
como entrada de control (saída para Arduíno).
O programa debe accionar o servo recollendo exclusivamente ordes 
do monitor serie, de maneira que: se hai unha orde dispoñible 
no monitor serie, acciona o servo. Se non hai ningunha orde no 
monitor serie, o servo non debe accionar. 
Débese situar inicialmente o servo na posición 0º, 
antes de que o controle o monitor serie.

- O programa debe ser reactivo ao potenciómetro (8 veces por segundo).
- O potenciómetro controla o ángulo de xiro do servo.
- A precisión do potenciómetro é de 10º.

*****************************************************************/
/***************************************************************

Programa feito por Mario Fernández Tubío.
Última revisión: 03/05/2025

********************************************************/
#include <Servo.h>

int pos = 0;
int novaPos = 0;
int veloz = 4000;    // Reactividade (1000 ms / 0.25 = 4000 ms)
int paso = 5;
String orde = "";


Servo VIRAVIRA;

void setup(){
  
  VIRAVIRA.attach(3);
  Serial.begin(9600);
  
  Serial.println("Servo en 0 graos. A onde cho levo?...");
  VIRAVIRA.write(0);  // Situar inicialmente en 0º
  
}


void loop(){
  
if (Serial.available() > 0) {
       
    orde = Serial.readStringUntil('\n'); // Ler a orde do monitor
   
    orde.trim(); /* Aseguramos lectura correcta 
                 eliminando os espazos en branco*/
  
// Interpretamos a orde
      novaPos = interpretarOrde(orde);
  
      if (novaPos != -1) {  /*Sempre que non sexa unha 
                              orde inválida*/
     
// Axustar á precisión
      pos = (novaPos / paso) * paso;
      VIRAVIRA.write(pos);    //Accionamos o servo     

// Pintamos por pantalla a nova posición do servo
      Serial.print("Servo movido a: ");
      Serial.print(pos);
      Serial.print(" graos -----> ");
      Serial.println(texto(pos));  
    } else {
      Serial.println("Repite, que non che entendo.");
    }

    delay(veloz);
  }
}
  
/********* Aquí Interpretamos a Orde do SERIAL *********/

//Función para interpretar a orde textual

int interpretarOrde(String orde) {
  
  if (orde == "esquerda" || orde == "180") return 180;
  
  else if (orde == "diagonal esquerda" || 
           orde == "135") return 135;
    
  else if (orde == "centro" || 
           orde == "90") return 90;
   
  else if (orde == "diagonal dereita" || 
           orde == "45") return 45;
    
  else if (orde == "dereita" || 
           orde == "0") return 0;
   
      
  return -1; // Orde non válida
}

// Función para devolver a orde textual correspondente á posición

String texto(int pos) {
  
  if (pos == 180) return "esquerda";
  else if (pos == 135) return "diagonal esquerda";
  else if (pos == 90) return "centro";
  else if (pos == 45) return "diagonal dereita";
  else if (pos == 0) return "dereita";
  

}
