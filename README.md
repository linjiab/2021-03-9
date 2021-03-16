## 2021-03-9


##lcd 功能 按鍵控制
```c++
const int rs = 12, en = 11, d4 = 5, d5 = 4, d6 = 3, d7 = 2;
LiquidCrystal lcd(rs, en, d4, d5, d6, d7);
byte smiley[8] = {
  B00000,
  B10001,
  B00000,
  B00000,
  B10001,
  B01110,
  B00000,
};

void setup() {
  lcd.begin(16, 2);
  lcd.setCursor(2, 1);
  lcd.print("Hello, world!");
  delay(300);
  lcd.createChar(0, smiley);
  pinMode(7, OUTPUT);
  lcd.begin(16, 2);
  lcd.setCursor(4, 0);
  lcd.write(byte(0));
  delay(300);
  for (int a = 0; a < 5; a++)
  {
    for (int i = 0; i < 16; i++)
    {
      lcd.clear();
      lcd.setCursor(i, 0);
      lcd.print("B I M O");
      lcd.scrollDisplayRight();
      delay(100);
      lcd.print("B I M O");
    }
  }
  for (int a = 7; a < 9; a++)
  {
    pinMode(a,INPUT);
    digitalWrite(a,1);
  }
  for (int a = 7; a < 9; a++)
  {
    pinMode(7,OUTPUT);
    digitalWrite(7,0);
  }
  lcd.clear();
}
void loop() {
  lcd.setCursor(2, 1);
  lcd.print("B I M O");
  if (digitalRead(8) == 0)
  {
    while (digitalRead(8) == 0); {
      delay(20);
    }
    lcd.scrollDisplayLeft();
  }
  if (digitalRead(9) == 0)
  {
    while (digitalRead(9) == 0); {
      delay(20);
    }
    lcd.scrollDisplayRight();
  }
}
```
![image](https://github.com/linjiab/2021-03-9/blob/main/3E064986-0BE1-498C-B987-608E0E0807D5.gif)
```c++
int x;
void setup() {
  // put your setup code here, to run once:

  pinMode(5, OUTPUT);
  pinMode(6, OUTPUT);
  pinMode(2, INPUT);
  pinMode(3, INPUT);
  Serial.begin(9600);

}
void motor(int x)
{
  analogWrite(5, x);
  digitalWrite(6, 0);
}
void loop() {
 
 if ( digitalRead(2) == LOW)
  {
    while (digitalRead(2) == LOW);
    x = x + 35;
  }
  if (x >= 255){
    x = 255;
  }
  motor(x);
   if ( digitalRead(4) == LOW)
  {
    while (digitalRead(4) == LOW);
    x = x - 35;
  }
  if (x <= 0){
    x = 0;
  }
  if(x<=120)x=120;
  motor(x);
  Serial.println(x);
}
```
