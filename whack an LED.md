```c++

  const int led_red = 2;         // Output pins for the LEDs
  const int led_blue = 3;
  const int led_yellow = 4;
  const int led_green = 5;
  const int red_button = 12;     // Input pins for the buttons
  const int blue_button = 11;
  const int yellow_button = 10;
  const int green_button = 9;  
  int count = 0;                 // Hit (score) counter
  int playTime = 10;             // Amount of "Moles" to pop out.
 
 
  /*
  functions to flash LEDs and pop up that "Mole" - (aka LED).
  */
  void flash_red() {
    digitalWrite(led_red, HIGH);
    delay(1000);
    if (digitalRead(red_button) == LOW) {    // Red button
          count=count+1;
          Serial.println(count);
    }
    digitalWrite(led_red, LOW);
  }
 
  void flash_blue() {
    digitalWrite(led_blue, HIGH);
    delay(1000);
        if (digitalRead(blue_button) == LOW) {    // Blue button
          count=count+1;
          Serial.println(count);
    }
    digitalWrite(led_blue, LOW);
  }
 
  void flash_yellow() {
    digitalWrite(led_yellow, HIGH);
    delay(1000);
        if (digitalRead(yellow_button) == LOW) {    // Yellow button
          count=count+1;
          Serial.println(count);
    }
    digitalWrite(led_yellow, LOW);
  }
 
  void flash_green() {
    digitalWrite(led_green, HIGH);
    delay(1000);
        if (digitalRead(green_button) == LOW) {    // Green button
          count=count+1;
          Serial.println(count);
    }
    digitalWrite(led_green, LOW);
  }
 
  /* a function to select which mole to popup
  */
  void MolePopup(long led) {
    switch (led) {
        case 0:
          flash_red();
          break;
        case 1:
          flash_green();
          break;
        case 2:
          flash_yellow();
          break;
        case 3:
          flash_blue();
          break;
      }
      delay(50);
  }
 
  // function to end the game (repeats 5 times)
  void GameEnd() {
    for(int i = 0; i < 5; i++) {
      digitalWrite(led_red, HIGH);     // turn all LEDs on
      digitalWrite(led_green, HIGH);
      digitalWrite(led_yellow, HIGH);
      digitalWrite(led_blue, HIGH);
      delay(1000);
      digitalWrite(led_red, LOW);        // turn all LEDs off
      digitalWrite(led_green, LOW);
      digitalWrite(led_yellow, LOW);
      digitalWrite(led_blue, LOW);
      delay(1000);      
    }
    count = 0;                         // reset score
  }
 
  // function to build and play the randomized sequence
  void playGame() {
    for (int i = 0; i < playTime; i++) {  // loop for length of playTime
      MolePopup(random(4));             // Have a random "mole" pop up.
    }                      
  }
 
  // standard sketch setup function
  void setup() {
    pinMode(led_red, OUTPUT);         // configure LEDs on outputs
    pinMode(led_green, OUTPUT);
    pinMode(led_yellow, OUTPUT);
    pinMode(led_blue, OUTPUT);
    pinMode(red_button, INPUT);       // configure buttons on inputs
    digitalWrite(red_button, HIGH);   // turn on pullup resistors
    pinMode(green_button, INPUT);
    digitalWrite(green_button, HIGH);
    pinMode(yellow_button, INPUT);
    digitalWrite(yellow_button, HIGH);
    pinMode(blue_button, INPUT);
    digitalWrite(blue_button, HIGH);
    randomSeed(analogRead(5));    // random seed for sequence generation
   
    Serial.begin(9600);           // Where the score is displayed
  }

```
 
  // standard sketch loop function
  void loop() {
    playGame();      // play the game
    delay(1000);     // wait a sec
    GameEnd();       // Play the game END flashing sequence.
  }
 
