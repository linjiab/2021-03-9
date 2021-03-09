## 2021-03-9
##lcd 功能 按鍵控制
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
