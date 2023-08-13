# Communication-between-two-Arduino
When we want to send information between two electronic devices, there are two basic ways to do so: either Serial or Parallel.

Serial communications have become more widespread due to the advantages they provide in terms of cost and the ease of building a communication channel and error detection.

In this context, the name of the UART standard, or Universal Asynchronous Transmitter / Receiver, stands out.

Establishing a serial communication channel between two devices using the UART standard requires three wires (buses):

Tx data transmission wire

Rx Data Receiver Wire

Grounding GND

![tx](https://github.com/shaikhahObaid/Communication-between-two-Arduino/assets/111530370/6093cd84-9b3e-4c3f-92b4-0f281abd23ec)

## Software instructions used for serial communication
The Arduino environment includes a mode through which commands can be sent and received via the serial communication port (or ports) available on the Arduino board, and this mode is Serial.

Serial.readBytes() reads characters from the serial port into a buffer. The function terminates if the determined length has been read, or it times out

Syntax:

Serial.readBytes(buffer, length)

Serial.write() writes binary data to the serial port. This data is sent as a byte or series of bytes; to send the characters representing the digits

Syntax:

Serial.write(val)

Serial.write(str)

Serial.write(buf, len)

## Practical example - controlling the lighting via a push-button switch by using two connected Arduino  
Explanation of circuit operation Each time the key is pressed in the second Arduino  , the state of the light source diode changes in the first Arduino , that is, if the light source diode lights up and the key is pressed, the light source diode stops working, and with a new press on the key, the diode will return to work, and so on.

## Components list
 ![222](https://github.com/shaikhahObaid/Communication-between-two-Arduino/assets/111530370/038370be-20fe-49ff-b6c5-a957a2a2b0aa)
## Circuit view and simulation
 ![rr](https://github.com/shaikhahObaid/Communication-between-two-Arduino/assets/111530370/b44ca22c-732e-431b-8cb2-88fcc0140e28)
 https://www.tinkercad.com/things/abIPK9xhFtd-copy-of-serial-communication-between-two-arduino/editel?sharecode=Oiu9GmVVIVbsDjfvdntWe0GE2n-m6s22ea37MIHEx4g 
 ## The code 
 ### for the second Arduino 
 int buttonPin = 12;
 
int X;

char buttonState[5] = "LOW ";

char H[5]="HIGH";

char L[5]="LOW ";

void setup() {

  // Begin the Serial at 9600 Baud
  Serial.begin(9600);
  
  pinMode(buttonPin, INPUT);
  
}

void loop()
{ 

 X = digitalRead(buttonPin);
 
  if (X == 1)
  
  buttonState[5] = H[5];
  
  else 
  
  buttonState[5] = L[5];
  
  Serial.write(buttonState, 5); //Write the serial data
  
  delay(1000);
  
} 
### for the first Arduino 
char buttonState[5] ;

int ledPin = 13;

char H[5]="HIGH";

char L[5]="LOW ";


void setup() {

  // Begin the Serial at 9600 Baud
  
  Serial.begin(9600);
  
  pinMode(ledPin, OUTPUT);
  
}

void loop()
{
 Serial.readBytes(buttonState, 5); //Read the serial data and store in var
 
  if (buttonState[5] == H[5])

     digitalWrite(ledPin,HIGH);
     
  if (buttonState[5] == L[5])
  
    digitalWrite(ledPin,LOW);
  
  delay(1000);
  
}

