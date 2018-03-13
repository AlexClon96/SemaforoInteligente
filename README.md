# SemaforoInteligente
***
## indice 
+ [descripcion del programa](#descripcion)
+ [circuito en digital](#circuito)    
+ [codigo en arduino](#codigo)
***
## Descripcion   
Este es un trabajo creado en arduino en el cual simula el comportamiento de 2 semáforos uno de peatones y otro para carros en los cuales los  semaforos se van a sincronizar de tal manera que cuando el semaforo de peatones este en rojo el semaforo de los autos estara en verde
***
## circuito 
![circuito](/CircuitoSemaforo.JPG)
***
## codigo 
~~~
/* semaforo
  Este semaforo tiene 2 partes una es un semaforo comun con 3 focos(rojo, verde,amarillo) que corresponde a los carros y otto 
  de 2 colores(rojo, verde) correspondiente a los peatones, en el semaforo de los peatones habra un boton el cual  su funcion
  sera pedir el paso al semaforo de los coches para que los peatones puedan pasar, el tiempo que dure cada semaforo dependera
  de un potenciometro que se encargara de la medicion del tiempo de espera

Autor: Manuel Alejandro Torres Fonseca 
*/                               //puertos    
const int pverde = 9;       //led verde del peaton
const int projo = 8;        //led rojo del peaton
const int rojo = 11;        //led rojo de autos
const int ama = 12;         //led amarillo de autos
const int verde = 13;       //led verde de autos
const int boton = 7;        //boton de  peatones
const int pot=A0;           //potenciometro 
int espera=0;               // variable para checar el tiempo 

void setup() {                      
  pinMode(boton, INPUT);            //indica que de ese pin se va recivir la señal emitida por el boton
  pinMode(pverde, OUTPUT);          //inidca que de ese pin va mandar la señal para prender el led verde de peatones
  pinMode(projo, OUTPUT);           //inica que de ese pin va mandar la señal para prender el led rojo de peatones
  pinMode(rojo, OUTPUT);            //indica que de ese pin va mandar la señal para prender el led rojo de los autos
  pinMode(ama, OUTPUT);             //indica que de ese pin va a mandar la señal para prender el led amarillo de los autos
  pinMode(verde, OUTPUT);           //indica que de ese pin va a mandar la señal para prender el led verde de los autos
  digitalWrite(verde, HIGH);        //comienza el proceso del semaforo prendiedo el led verde  de los carros indicando que los autos estan pasando
  digitalWrite(projo, HIGH);        //enciende el led rojo de los peatones por que como estan pasando los carros se deben para los peatones 
  Serial.begin(9600);               //abre el puerto serial a una velocidad de comunicacion de 9600 baudios

}

void loop() {
  int val=0;                              //permite  inicializar el precionado del boton
  int valor=0;                            //inicializa el valor del potenciometro
 val=digitalRead(boton);                  //infivs que el boton emitira un pulso digital
 valor=(analogRead(pot)*10);              // indica la cantidad que va mandar el potenciometro de manera analogica

 
  if (val == HIGH &&espera==0) {            //indica que empiece el cambio cuando se preciona el boton y asegurando que halla pasado 
      espera==1;                            // tiempo desde que se preciono por ultima vez
      digitalWrite(verde, LOW);             //apaga el led verde de los carros  para  indicar que ya no deben arrancar los carros
      digitalWrite(ama, HIGH);              //prende el led amarillo de los carros para indicar precaucion que los peatones van a cruzar
     delay(valor);                          //indica el tiempo de espera dado por el potenciometro

      digitalWrite(ama, LOW);             //se apaga el led amarillo para hacer el cambio a rojo del semaforo de los autos
      digitalWrite(rojo, HIGH);           //se prende el led rojo para indicar el alto total de los autos
      digitalWrite(projo, LOW);           //se apaga el led rojo de los peatones para indicar que los peatones pueden posteriormente caminar 
      digitalWrite(pverde, HIGH);         //se prende el led verde de los peatones por lo que ya pueden transitar seguros
      delay(valor);                       //indica el tiempo en que estaran pasando los peatones 
      }
      
      digitalWrite(pverde, LOW);        //se apaga el led verde de los peatones para indicar que ya van a circular los autos 
      digitalWrite(projo, HIGH);        //se prende el led rojo de los peatones para indicar el alto total de los peatones 
      digitalWrite(rojo, LOW);          //se apaga  el rojo de los carros para que se preparen a arrancar 
      digitalWrite(verde, HIGH);        //se prende el verde de los carros para que empiecen a circular los carros
      delay(valor);                     //es el tiempo que tardan en circular los carros 
      espera=0;                         //es para reiniciar el procedimiento de ambos semaforos
  }



~~~


