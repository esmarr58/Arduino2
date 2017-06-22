/*
HeTPro LABs
Creado: 20-Junio-2017
Autor: Dr. Ruben E-Marmolejo
https://hetpro-store.com/

 	 
 */
 
#include <SD.h>

volatile boolean salida = false;
volatile long int cuenta=0;
volatile long int t0=0;
volatile long int t1=0;
File Registrador1;

void setup()
{

  Serial.begin(9600);
   while (!Serial) {
    ; // Espera a que el puerto serial se inicialize, solo es necesario para el Leonardo. 
  }
   //pinMode(10, OUTPUT)  //Comentar para el MEGA, descomentar para el UNO
   pinMode(53, OUTPUT);  ////Des-Comentar para el MEGA, Comentar para el UNO


  if (!SD.begin(4)) {   //El 4 se refiere al pin del CS. Para este shield es el pin 4.
    Serial.println("No se puede inicializar la micro-SD");
    return;
  }
  Serial.println("micro-SD inicializada");
 

}

void registrarDato(unsigned int dato){
    Registrador1 = SD.open("LOG.TXT", FILE_WRITE);  //Abre y/o crea el archivo LOG.TXT
  
  // Si se abre el archivo escribir datos. 
  if (Registrador1) {
      Registrador1.print(dato);
      Registrador1.print(";");
      Registrador1.println((long int)millis());
      Registrador1.close();
      Serial.print("Se han guardado: ");
      Serial.print(cuenta++);
      Serial.println(" datos");
  }
  else{
    Serial.println("Error no se puede abrir el archivo LOG.TXT");
  }
  
  
}

void loop()
{
        if(salida == false) {
          t0 = millis(); 
	 
          if(t0 > t1){
             registrarDato(analogRead(A0));
             t1=millis()+5000;
          }
        }
}

void serialEvent() {
  if (Serial.available() > 0) {
    //Leer un nuevo Byte serial
    char datoSerialByte = (char)Serial.read();
    if(datoSerialByte == 'A') {
        salida = true;
        Serial.println("Es seguro retirar la memoria");
    }
    else if(datoSerialByte == 'B'){
        salida = false;
    }
  }
}
