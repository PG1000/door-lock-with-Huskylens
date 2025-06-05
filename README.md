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
🔒 Χαρακτηριστικά Ασφαλείας (Προαιρετικά)
Ειδοποίηση για μη αναγνωρισμένους χρήστες (π.χ. buzzer ή ειδοποίηση στο κινητό μέσω Wi-Fi).

Καταγραφή αναγνωρισμένων προσώπων σε κάρτα SD ή cloud.

Χρονικό όριο για προσπάθειες αναγνώρισης.

![IMG_20250529_183928](https://github.com/user-attachments/assets/9c7b3f53-57ba-468e-afb7-d5571bf9822a)

