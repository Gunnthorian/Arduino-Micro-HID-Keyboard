#include <Keyboard.h>

#define KEY_LEFT_CTRL       128
#define KEY_LEFT_SHIFT      129
#define KEY_LEFT_ALT        130
#define KEY_LEFT_GUI        131
#define KEY_RIGHT_CTRL      132
#define KEY_RIGHT_SHIFT     133
#define KEY_RIGHT_ALT       134
#define KEY_RIGHT_GUI       135

#define KEY_UP_ARROW        218
#define KEY_DOWN_ARROW      217
#define KEY_LEFT_ARROW      216
#define KEY_RIGHT_ARROW     215
#define KEY_ESC             177
#define KEY_TAB             179
#define KEY_CAPS_LOCK       193
#define KEY_RETURN          176
#define KEY_BACKSPACE       178

#define KEY_INSERT          209
#define KEY_DELETE          212
#define KEY_PAGE_UP         211
#define KEY_PAGE_DOWN       214
#define KEY_HOME            210
#define KEY_END             213

#define KEY_F1              194
#define KEY_F2              195
#define KEY_F3              196
#define KEY_F4              197
#define KEY_F5              198
#define KEY_F6              199
#define KEY_F7              200
#define KEY_F8              201
#define KEY_F9              202
#define KEY_F10             203
#define KEY_F11             204
#define KEY_F12             205

const int row_count = 4;
const int col_count = 8;

int row_pins[row_count] = {2, 3, 4, 5};
int col_pins[col_count] = {6, 7, 8, 9, 10, 16, 14, 15};

int keyboard_layout[row_count][col_count][3] = {
  {{177, 1, "ESC"}, {'1', 1}, {'2', 1}, {'3', 1}, {'4', 1}, {'5', 1}, {'6', 1}, {KEY_BACKSPACE, 1}},
  {{179, 1, "TAB"}, {'q', 1}, {'w', 1}, {'r', 1}, {'t', 1}, {'y', 1}, {'u', 1}, {KEY_RETURN, 1}},
  {{KEY_CAPS_LOCK, 1}, {'z', 1}, {'x', 1}, {'c', 1}, {'v', 1}, {'/', 1}, {KEY_UP_ARROW, 1}, {KEY_RIGHT_ALT, 1}},
  {{KEY_LEFT_SHIFT, 1}, {KEY_LEFT_CTRL, 1}, {131, 1, "COMMAND"}, {32, 1, "SPACE"}, {32, 1, "SPACE"}, {KEY_LEFT_ARROW, 1}, {KEY_DOWN_ARROW, 1}, {KEY_RIGHT_ARROW, 1}},
};

void setup() {
  Serial.begin(9600);
  for(int r=0;r<row_count;r++) {
    pinMode(row_pins[r], OUTPUT);
  }
  for(int c=0;c<col_count;c++) {
    pinMode(col_pins[c], INPUT);
    digitalWrite(col_pins[c], 1); 
  }
  delay(200);
}

void loop() {
  for(int row=0;row<row_count;row++) {
    for(int r=0;r<row_count;r++) {
      digitalWrite(row_pins[r], 1);
    }
    delay(1);
    for(int r=0;r<row_count;r++) {
      if(r != row) {
        digitalWrite(row_pins[r], 1); 
      }else{
        digitalWrite(row_pins[r], 0); 
      }
    }
    for(int c=0;c<col_count;c++) {
      int key_data = digitalRead(col_pins[c]);
//      Serial.print("<" + String(row) + ", " + String(c) + ">");
//      Serial.println(keyboard_layout[row][c][2]);
      if(key_data != keyboard_layout[row][c][1]) {
//        Serial.println("diff");
        if(key_data == 0){
          char key = keyboard_layout[row][c][0];
          Serial.println(String(key) + " Down");
          Keyboard.press(keyboard_layout[row][c][0]);
          keyboard_layout[row][c][1] = 0;
        }
        if(key_data == 1){
          char key = keyboard_layout[row][c][0];
          Serial.println(String(key) + " Up");
          Keyboard.release(keyboard_layout[row][c][0]);
          keyboard_layout[row][c][1] = 1;
        }
      }
    }
  }
}
