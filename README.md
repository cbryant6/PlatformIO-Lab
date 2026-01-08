# PlatformIO-Lab

```python

#include <Arduino.h>
#include <Bounce2.h>

// Pin definitions
const int SWITCH_PIN = D2;  // GPIO switch pin
const int LED_PIN = D10;    // GPIO LED pin

// Debounce object
Bounce2::Button button = Bounce2::Button();

// Variable to track LED state
bool ledState = false;

void setup() {
  // Initialize Serial for logging
  Serial.begin(115200);
  delay(1000);  // Wait for serial to initialize
  
  Serial.println("\n\n=== LED Switch Control Initialized ===");
  Serial.println("XIAO ESP32C3 - Tactile Switch with LED Control");
  Serial.println("=====================================\n");
  
  // Configure LED pin
  pinMode(LED_PIN, OUTPUT);
  digitalWrite(LED_PIN, LOW);  // Start with LED off
  
  // Configure debounced button
  button.attach(SWITCH_PIN, INPUT_PULLUP);  // Use internal pull-up
  button.interval(50);  // Debounce interval in ms
  button.setPressedState(LOW);  // Button is pressed when LOW
  
  Serial.println("Setup complete. Waiting for button presses...\n");
}

void loop() {
  // Update button state
  button.update();
  
  // Check if button was pressed
  if (button.pressed()) {
    // Toggle LED state
    ledState = !ledState;
    digitalWrite(LED_PIN, ledState ? HIGH : LOW);
    
    // Log the state change
    Serial.print("Button pressed - LED is now: ");
    Serial.println(ledState ? "ON" : "OFF");
  }
  
  // Small delay to prevent overwhelming the serial output
  delay(10);
}
```

<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/348f8014-ac5a-4c82-a948-bef44ad32a27" />

<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/49d7def3-a7b6-4a19-a6b8-b6f4e052e411" />

![IMG_0671_2mb](https://github.com/user-attachments/assets/bb8e283a-012e-4b66-a990-a856febb13ea)

<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/6d9fff31-8aca-4c71-9433-ad3057f4675c" />


