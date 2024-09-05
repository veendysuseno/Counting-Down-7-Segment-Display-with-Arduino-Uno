# Counting Down use a 7-Segment Display with Arduino Uno

## Description

The Counting Down project demonstrates how to use a 7-segment display to count down from 10 to 0. The project utilizes a basic countdown mechanism to cycle through digits on the display, with each digit represented by activating specific segments of the 7-segment display.

## Components

- Arduino (e.g., Arduino Uno)
- 7-Segment Display
- 9 Jumper Wires

## Pin Configuration

| Segment Pin    | Arduino Pin |
| -------------- | ----------- |
| a              | 2           |
| b              | 3           |
| c              | 4           |
| d              | 5           |
| e              | 6           |
| f              | 7           |
| g              | 8           |
| Common Cathode | 9           |

## Code

```cpp
// Code for Counting Down

byte nilai;
byte seven_seg_digits[10][7] = {
  { 0,0,0,0,0,0,1 },  // = 0
  { 1,0,0,1,1,1,1 },  // = 1
  { 0,0,1,0,0,1,0 },  // = 2
  { 0,0,0,0,1,1,0 },  // = 3
  { 1,0,0,1,1,0,0 },  // = 4
  { 0,1,0,0,1,0,0 },  // = 5
  { 0,1,0,0,0,0,0 },  // = 6
  { 0,0,0,1,1,1,1 },  // = 7
  { 0,0,0,0,0,0,0 },  // = 8
  { 0,0,0,0,1,0,0 }   // = 9
};

void setup() {
  pinMode(2, OUTPUT);
  pinMode(3, OUTPUT);
  pinMode(4, OUTPUT);
  pinMode(5, OUTPUT);
  pinMode(6, OUTPUT);
  pinMode(7, OUTPUT);
  pinMode(8, OUTPUT);
  pinMode(9, OUTPUT);
  digitalWrite(9, HIGH); // Initialize common cathode
  nilai = 10;
}

void sevenSegWrite(byte segment) {
  byte pin = 2;
  for (byte segCount = 0; segCount < 7; ++segCount) {
    digitalWrite(pin, seven_seg_digits[segment][segCount]);
    ++pin;
  }
}

void loop() {
  nilai--;
  sevenSegWrite(nilai);
  if (nilai == 0) nilai = 10;
  delay(1000);
}
```

## How It Works

1. Initialization:
   - The setup() function configures the pins connected to the 7-segment display as outputs and initializes the common cathode.
   - The variable nilai is set to 10, which is the starting count value.
2. Displaying Digits:
   - The sevenSegWrite() function takes a digit as input and activates the corresponding segments on the 7-segment display.
   - The loop() function decreases the value of nilai every second, updates the display to show the new value, and resets nilai to 10 when it reaches 0.

## Usage

1. Connect the 7-segment display to the Arduino according to the pin configuration provided.
2. Upload the code to the Arduino.
3. Observe the 7-segment display counting down from 10 to 0, cycling continuously.

## Notes

• Ensure the 7-segment display is properly connected with the correct pin configuration.
• The common cathode connection should be properly set to HIGH for the display to function correctly.
