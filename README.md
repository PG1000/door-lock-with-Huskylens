# door-lock-with-Huskylens

Το έργο "Door Lock with HuskyLens" συνδυάζει τεχνητή νοημοσύνη και αυτοματισμό για τη δημιουργία ενός έξυπνου και ασφαλούς συστήματος ελέγχου πρόσβασης. Με τη χρήση της κάμερας HuskyLens και τεχνολογίας αναγνώρισης προσώπου, η πόρτα ανοίγει μόνο για εξουσιοδοτημένα άτομα, χωρίς κλειδιά ή κάρτες. Μια σύγχρονη λύση που κάνει την καθημερινότητα πιο ασφαλή και εύκολη.

🧠 Λειτουργία

Ο χρήστης εκπαιδεύει το HuskyLens με τα πρόσωπα που επιτρέπεται να έχουν πρόσβαση.

Όταν κάποιος πλησιάζει την πόρτα, το HuskyLens σαρώνει το πρόσωπο.

Αν το πρόσωπο αναγνωριστεί ως εγκεκριμένο:

Στέλνεται σήμα στον servo motor ή ηλεκτρονικό μηχανισμό για να ξεκλειδώσει η πόρτα.

Αν δεν αναγνωριστεί:

Η πόρτα παραμένει κλειδωμένη και, προαιρετικά, ενεργοποιείται ειδοποίηση (π.χ. buzzer ή LED).

⚙️ Υλικά

HuskyLens AI Camera

Arduino Uno ή ESP32

Servo Motor ή ηλεκτρονικός μηχανισμός κλειδώματος

Καλώδια jumper

Τροφοδοσία 5V

Πινακίδα breadboard (αν χρησιμοποιείται Arduino)

🧾 Παράδειγμα Κώδικα (Arduino)
cpp
Αντιγραφή
Επεξεργασία
#include "HUSKYLENS.h"
#include <Servo.h>

HUSKYLENS huskylens;
Servo lockServo;

void setup() {
  Serial.begin(9600);
  Wire.begin();
  huskylens.begin(Wire);
  lockServo.attach(9); // Συνδέουμε τον servo στη θύρα 9
  lockServo.write(0);  // Θέση κλειδώματος
}

void loop() {
  if (huskylens.request()) {
    if (huskylens.isLearned()) {
      for (int i = 0; i < huskylens.countBlocks(); i++) {
        HUSKYLENSResult result = huskylens.getBlock(i);
        if (result.ID == 1) { // ID του αναγνωρισμένου προσώπου
          unlockDoor();
        }
      }
    }
  }
}

void unlockDoor() {
  lockServo.write(90); // Ξεκλείδωμα
  delay(5000);         // Περιμένουμε 5 δευτερόλεπτα
  lockServo.write(0);  // Ξανακλείδωμα
}
🔒 Χαρακτηριστικά Ασφαλείας 

Ειδοποίηση για μη αναγνωρισμένους χρήστες (π.χ. buzzer ή ειδοποίηση στο κινητό μέσω Wi-Fi).

Καταγραφή αναγνωρισμένων προσώπων σε κάρτα SD ή cloud.

Χρονικό όριο για προσπάθειες αναγνώρισης.

![IMG_20250529_183939](https://github.com/user-attachments/assets/01265acf-242e-4f62-9935-9c5b79f97cb5)
![IMG_20250529_183933](https://github.com/user-attachments/assets/7bc69be2-fc84-4253-8012-bb09538e2aab)
![IMG_20250529_183928](https://github.com/user-attachments/assets/d663ec1e-6774-4c64-a4c9-3803bcdc8e1c)


