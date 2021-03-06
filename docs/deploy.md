# Διαδικασίες deployment

Για να ενσωματωθούν στην παραγωγική λειτουργία οι αλλαγές που έχει υλοποιήσει ο προγραμματιστής πρέπει να περάσουν οι αλλαγές από 3 στάδια 
  * [dev](#dev)
  * [staging](#staging)
  * [production](#production)

## dev
Το περιβάλλον αυτό είναι ορατό μόνο εντός του δικτύου της ΜΟΔ. Η διαδικασία για να αναβαθμιστεί η dev είναι η εξής:
* Συγχρονισμός των φακέλων `C:\inetpub\wwwroot\AuditorCIS_13` => `\\10.10.76.138\c$\inetpub\wwwroot\mis_dev35`
* Σημείωση στον Update Wizard των αρχείων που αλλάξαμε ή δημιουργήσαμε. Καινούρια αρχεία πρέπει να έχουν τη σήμανση ">>> NEW". Για τα κοινά αρχεία που αλλάξαμε θα πρέπει να αναφέρουμε ποιο μέρος τους αλλάξε.

Θα πρέπει να μεταφέρονται στο dev περιβάλλον μόνο τα αρχεία που έχουμε πειράξει καθώς και τα dll's που βρίσκονται στο φάκελο bin. Αρχεία κώδικα(.cs) δεν χρειάζεται να μεταφερθούν γιατί μεταφέρονται τα compiled dll's.
## staging
Το περιβάλλον αυτό είναι ορατό σε όλους (εντός και εκτός ΜΟΔ). Εδώ γίνεται το τελικό testing από όλους τους εμπλεκόμενους φορείς για να δοθεί το οκ ώστε να αναβαθμιστεί μετά το παραγωγικό περιβάλλον. Η διαδικασία για αναβάθμιση της staging είναι η εξής:
* Συγχρονισμός των φακέλων `C:\inetpub\wwwroot\AuditorCIS_13` => `\\pske-vpc02\c$\inetpub\wwwroot\mis_staging` (κώδικας, text αρχεία, όχι dll's )
* RDP στον `pske-vpc02`
  * Στο visual studio `add to project` για τα αρχεία που έιναι καινούρια και rebuild
  * Συγχρονισμός των φακέλων  `C:\projects\AuditorCIS_dev13`	=> 	`\\pske-vpc02\c$\Projects\mis_staging`
* Σημείωση στον Update Wizard ότι οι αλλαγές είναι πλέον στο περιβάλλον staging

Κάνοντας RDP στον server αυτόματα αποσυνδέεται όποιος άλλος χρηστης είναι συνδεδεμένος. Αυτό έχει σαν αποτέλεσμα να μπορεί μόνο ένας χρήστης τη φορά να είναι συνδεδεμένος.

## production
Το σύστημα που βρίσκεται σε παραγωγική λειτουργία, είναι αυτό που βλέπουν όλοι οι εμπλεκόμενοι στις κρατικές ενισχύσεις (επενδυτες, φορείς, προμηθευτές, οφελούμενοι, ελεγκτες κτλ). Για την αναβάθμιση της παραγωγικής η διαδικασία είναι η εξής:
