# Thesis Refactor Targets

Το παρόν αρχείο λειτουργεί ως blueprint για το επόμενο, εκτεταμένο refactoring της διπλωματικής εργασίας. Η νέα στρατηγική δεν αντιμετωπίζει την αρχική υλοποίηση ως κάτι που πρέπει να «ξηλωθεί», αλλά ως το πρώτο, απολύτως απαραίτητο εξελικτικό στάδιο της πλατφόρμας. Η τελική αφήγηση πρέπει να αποτυπώνει μια ώριμη μηχανική πορεία δύο φάσεων: από ένα τοπικό proof of concept βασισμένο σε openHAB / InfluxDB / Grafana προς μια πλήρως cloud-based SaaS πλατφόρμα με custom UI, Supabase, AI δυνατότητες και enterprise λογική Smart Campus.

## 1. Τι ΠΡΕΠΕΙ ΝΑ ΜΕΙΝΕΙ (Άθικτο - Core Foundations)

### 1.1 Edge Hardware και Φυσικό Πεδίο
- Να παραμείνει ο πυρήνας του edge hardware:
  - ESP32
  - Shelly 1PM
  - Sonoff
  - Raspberry Pi
  - αισθητήρες θορύβου, θερμοκρασίας, κατάστασης θυρών και λοιποί αισθητήρες πεδίου
- Να διατηρηθεί η λογική ότι η πλατφόρμα στηρίζεται σε low-cost IoT nodes και όχι σε ακριβό, πλήρως ιδιόκτητο BMS.
- Να παραμείνει η έννοια του φυσικού επιπέδου ως βασικού παραγωγού τηλεμετρίας και ενεργοποιήσεων.

### 1.2 Αρχικά KPIs και Εμπειρικά Αποτελέσματα
- Να μείνουν άθικτα τα headline αποτελέσματα της μελέτης:
  - 19,7% μείωση κατανάλωσης ενέργειας
  - 55 dBA ως operational intervention threshold
  - 41,02% ROI
  - 42,5 μήνες απόσβεση
  - 32,5% Year-over-Year βελτίωση για τον Νοέμβριο
  - 10,9% raw before/after σύγκριση
- Να παραμείνει η διάκριση μεταξύ:
  - raw comparison
  - weighted / baseline comparison
  - Year-over-Year comparison
- Να διατηρηθεί η τεχνοοικονομική διάσταση της εργασίας ως κεντρικό στοιχείο αξιολόγησης.

### 1.3 Θεωρητικό Πλαίσιο
- Να μείνει ως σταθερή θεωρητική βάση η διάκριση:
  - Digital Model
  - Digital Shadow
  - Digital Twin
- Να διατηρηθεί ο κεντρικός ρόλος του `Sense-Decide-Act` closed-loop control.
- Να παραμείνει το openHAB Semantic Model ως βασικός άξονας λογικής οργάνωσης του συστήματος.
- Να παραμείνει η αρχιτεκτονική πέντε επιπέδων ως μοντέλο αναφοράς για την πλατφόρμα.
- Να διατηρηθούν οι έννοιες:
  - Smart Campus
  - Semantic Middleware
  - Brownfield Integration
  - Interoperability

## 2. Πώς Αναδιαμορφώνεται η Υλοποίηση (Η Εξέλιξη του Συστήματος)

Η παλιά και η νέα υλοποίηση δεν πρέπει πλέον να εμφανίζονται ως αντιφατικά ή ανταγωνιστικά αφηγήματα. Πρέπει να αποδοθούν ως δύο διαδοχικές φάσεις μηχανικής ωρίμανσης του ίδιου συστήματος.

### 2.1 Φάση 1 - Αρχικό Πρωτότυπο (Proof of Concept)

Σε αυτή τη φάση θα ενταχθούν όλες οι αναφορές που αφορούν την αρχική τοπική υποδομή, ως το στάδιο στο οποίο:
- υλοποιήθηκε η πρώτη αξιόπιστη ροή τηλεμετρίας από το φυσικό πεδίο,
- οργανώθηκε η πρώτη λογική semantic mapping,
- δοκιμάστηκαν οι αρχικοί κανόνες ελέγχου,
- τεκμηριώθηκαν οι πρώτες λειτουργικές και ενεργειακές παρεμβάσεις.

#### Στοιχεία που πρέπει να παρουσιαστούν ως μέρος της Φάσης 1
- InfluxDB ως αρχική time-series βάση για την αποθήκευση τηλεμετρίας.
- Grafana ως αρχική υποδομή dashboarding και εποπτείας των χρονοσειρών.
- Floorplan Pages του openHAB ως αρχική πρακτική διεπαφή ελέγχου και οπτικοποίησης.
- Τοπική πρόσβαση / πιο περιορισμένο access model ως φυσικό χαρακτηριστικό του πρωτοτύπου.
- Οι κανόνες όπως οι NoiseGuard και FridgeGuardian ως πρώτα αποδεικτικά στοιχεία closed-loop λειτουργίας.

#### Πώς πρέπει να περιγραφεί η Φάση 1
- Όχι ως «ξεπερασμένο» σύστημα που πρέπει να σβηστεί από το κείμενο.
- Αλλά ως κρίσιμο proof of concept που:
  - απέδειξε τη βιωσιμότητα της αρχιτεκτονικής,
  - παρήγαγε τα πρώτα δεδομένα,
  - έδειξε ότι το Digital Twin μπορεί να λειτουργήσει σε πραγματικό σχολικό περιβάλλον,
  - κατέγραψε τα KPIs πάνω στα οποία στηρίζεται η εργασία.

### 2.2 Φάση 2 - Μετάβαση στη Νέα Cloud Πλατφόρμα

Η δεύτερη φάση πρέπει να παρουσιαστεί ως απάντηση στους περιορισμούς του αρχικού πρωτοτύπου. Το νέο κείμενο πρέπει να εξηγεί ότι η αναβάθμιση δεν έγινε επειδή η πρώτη φάση ήταν αποτυχημένη, αλλά επειδή:
- το UI ήταν πολύ system-centric,
- η εμπειρία ήταν πιο κατάλληλη για τεχνικούς και όχι για διοικητικούς χρήστες,
- η πρόσβαση ήταν λιγότερο ευέλικτη,
- τα dashboards ήταν περισσότερο στατικά ή εργαλειακά,
- δεν υπήρχε ακόμα ενιαία, user-centric SaaS εμπειρία.

#### Στοιχεία που πρέπει να παρουσιαστούν ως μέρος της Φάσης 2
- Custom cloud-based SaaS πλατφόρμα
- React 18
- Supabase
- Tailwind
- 3D visualization με Three.js / React Three Fiber
- 24/7 browser-based access
- πρόσβαση χωρίς VPN για τον τελικό χρήστη
- responsive εμπειρία σε mobile / tablet / desktop
- custom dashboards και operational views φιλικά σε μη-τεχνικούς χρήστες

#### Ρόλος του openHAB στη Φάση 2
- Το openHAB δεν αφαιρείται από το αφήγημα.
- Επανατοποθετείται ως:
  - semantic middleware
  - integration backbone
  - backend communication layer με το hardware
- Δηλαδή:
  - δεν είναι πλέον το βασικό front-end περιβάλλον,
  - αλλά παραμένει κομβικό στην αρχιτεκτονική ως ενδιάμεσο λογισμικό.

#### Κεντρική αφήγηση της μετάβασης
- Η εργασία πρέπει να δείχνει ότι η πλατφόρμα εξελίχθηκε:
  - από local prototype και engineering-first control environment
  - προς cloud-native Smart Campus SaaS
- Η μετάβαση αυτή είναι μέρος της συνεισφοράς της εργασίας και όχι απλή αλλαγή εργαλείων.

## 3. Τι ΠΡΕΠΕΙ ΝΑ ΠΡΟΣΤΕΘΕΙ (Νέο Περιεχόμενο & AI)

### 3.1 Ενσωμάτωση AI

Η Τεχνητή Νοημοσύνη πρέπει να αναδειχθεί ως βασικός, επεκτάσιμος πυλώνας της νέας αρχιτεκτονικής.

#### Τι πρέπει να προστεθεί
- Ρητή αναφορά ότι η νέα πλατφόρμα ενσωματώνει αλγορίθμους AI, όπως:
  - AI Energy Forecasting
  - πρόβλεψη ενεργειακής συμπεριφοράς
  - λογική για ευφυέστερη διαχείριση πόρων
- Να περιγραφεί η AI όχι ως αποκομμένο feature, αλλά ως θεμέλιο για:
  - decision support
  - forecasting
  - anomaly awareness
  - επόμενη γενιά αυτοματισμών

#### Πώς πρέπει να τοποθετηθεί θεωρητικά
- Η ενσωμάτωση AI πρέπει να παρουσιαστεί ως βήμα μετάβασης από rule-based Digital Twin προς Cognitive Digital Twin.
- Να τονιστεί ότι:
  - το τρέχον σύστημα δεν είναι ακόμη πλήρως αυτόνομο Cognitive Digital Twin,
  - αλλά η νέα αρχιτεκτονική θέτει τις βάσεις για αυτή τη μελλοντική εξέλιξη.

### 3.2 UI/UX & Access

#### Τι πρέπει να προστεθεί
- Ισχυρότερη έμφαση στην ευχρηστία του νέου UI για μη-τεχνικούς χρήστες, όπως:
  - διευθυντές
  - διοικητικό προσωπικό
  - προσωπικό λειτουργίας
- Ρητή ανάδειξη των εξής χαρακτηριστικών:
  - cloud-based πρόσβαση
  - 24/7 availability
  - no-VPN access για τον τελικό χρήστη
  - responsive λειτουργία σε mobile / tablet / PC
- Να εξηγηθεί γιατί το νέο UI είναι user-centric ενώ το παλιό περιβάλλον ήταν system-centric / engineering-centric.

### 3.3 Διαλειτουργικότητα και Brownfield Integration

#### Τι πρέπει να προστεθεί
- Να ενισχυθεί η περιγραφή της διαλειτουργικότητας ως κεντρικής τεχνολογικής καινοτομίας.
- Να τονιστεί ότι το σύστημα ενσωματώνει legacy hardware καθαρά μέσω λογισμικού.
- Να αναπτυχθεί περισσότερο η brownfield ενσωμάτωση:
  - αυτόματες πύλες σχολείου
  - κάμερες
  - smart irrigation
  - υπάρχουσες υποδομές πεδίου
- Να αναδειχθεί ότι η πλατφόρμα δεν ακολούθησε λογική rip-and-replace, αλλά λογική software-centric ενοποίησης.

### 3.4 Νέες Πηγές Έμπνευσης και Σχεδιαστικής Επιρροής

#### Τι πρέπει να προστεθεί
- Να ενσωματωθούν ρητές αναφορές στις επιρροές που διαμόρφωσαν τη νέα enterprise αρχιτεκτονική:
  - Coursera Industrial IoT
  - Coursera / professional training για Mastering Digital Twins
  - Indeex platform inspiration
  - Virtual Worlds / industrial digital environments
- Να αξιοποιηθούν όχι απλώς ως βιογραφική σημείωση, αλλά ως δείκτες σχεδιαστικής κατεύθυνσης προς πιο ώριμες, βιομηχανικού επιπέδου λύσεις.

### 3.5 Placeholders Εικόνων που πρέπει να προστεθούν

#### Για την αρχιτεκτονική και τη μετάβαση
- Placeholder: Τεχνική Αρχιτεκτονική της νέας cloud-based πλατφόρμας
- Placeholder: Deployment Topology (edge devices, middleware, cloud backend, web frontend)
- Placeholder: MQTT Tree / topic hierarchy
- Placeholder: openHAB Semantic Model
- Placeholder: Security / RBAC architecture
- Placeholder: Timeline εξέλιξης από Proof of Concept σε Cloud SaaS platform

#### Για το UI / UX / SaaS layer
- Placeholder: Smart Campus Dashboard
- Placeholder: 3D buildings / Digital Twin scene
- Placeholder: 2D Floorplans
- Placeholder: Device Management Tab
- Placeholder: Gates UI / Brownfield integration view
- Placeholder: Responsive mobile / tablet / desktop views

#### Για AI / analytics / operational intelligence
- Placeholder: AI Energy Forecasting dashboard
- Placeholder: Sustainability / operational intelligence charts
- Placeholder: Device-specific analytics view

#### Για field deployment
- Placeholder: Φωτογραφίες εγκατάστασης edge hardware και αισθητήρων

## 4. Αναδιατύπωση του Refactoring Narrative ανά Κεφάλαιο

### Κεφάλαιο 1 - Εισαγωγή
- Να προστεθεί εξαρχής η ιδέα ότι το έργο πέρασε από δύο στάδια υλοποίησης.
- Να αναδειχθεί ο μετασχηματισμός από local proof of concept σε custom cloud Smart Campus platform.
- Να προστεθεί σύντομη μνεία στο νέο cloud SaaS UI και στον ρόλο της AI ως επεκτάσιμου άξονα.

### Κεφάλαιο 2 - Ανασκόπηση Βιβλιογραφίας
- Να επεκταθεί το θεωρητικό πλαίσιο ώστε να υποστηρίζει:
  - cloud-native Digital Twins
  - user-centric industrial interfaces
  - AI-enabled Digital Twin evolution
- Να ενσωματωθούν οι νέες πηγές έμπνευσης και τα enterprise design references.

### Κεφάλαιο 3 - Αρχιτεκτονική / Μεθοδολογία
- Να παρουσιαστεί καθαρά η Φάση 1 και η Φάση 2 ως εξελικτική ακολουθία.
- Να παραμείνουν InfluxDB, Grafana και openHAB UI μέσα στο κείμενο, αλλά ως μέρος του αρχικού proof of concept.
- Να παρουσιαστεί το νέο cloud architecture ως η ώριμη εξέλιξη του αρχικού πυρήνα.

### Κεφάλαιο 4 - Υλοποίηση
- Να χωριστεί λειτουργικά σε:
  - αρχική υλοποίηση πρωτοτύπου
  - νέα SaaS υλοποίηση
- Να αναλυθεί η διαφορά UX μεταξύ openHAB-centric και custom React/Supabase interface.
- Να ενσωματωθούν τα νέα brownfield και AI στοιχεία.

### Κεφάλαιο 5 - Μεθοδολογία Αξιολόγησης
- Να παραμείνουν οι υφιστάμενες μετρήσεις και KPIs.
- Να εξεταστεί εάν χρειάζεται πρόσθετη αξιολόγηση usability / accessibility για τη νέα cloud διεπαφή.

### Κεφάλαιο 6 - Αποτελέσματα
- Να διατηρηθούν τα υπάρχοντα αποτελέσματα.
- Να προστεθεί νέα διάσταση αποτελεσμάτων για:
  - cloud dashboarding
  - AI forecasting
  - συνολική επιχειρησιακή επίγνωση

### Κεφάλαιο 7 - Συζήτηση
- Να αναδειχθεί η αξία της διαλειτουργικότητας, της brownfield ενσωμάτωσης και της μετατόπισης σε enterprise SaaS αρχιτεκτονική.
- Να τοποθετηθεί η AI ως βασικός μελλοντικός μοχλός ωρίμανσης της πλατφόρμας.

### Κεφάλαιο 8 - Συμπεράσματα και Μελλοντική Εργασία
- Να αναδιατυπωθεί το τελικό συμπέρασμα ως αφήγηση εξέλιξης:
  - από local prototype
  - σε cloud-native Smart Campus platform
  - με ορίζοντα Cognitive Digital Twin

## 5. Τελικός Στόχος του Refactoring

Μετά το refactoring, η διπλωματική πρέπει να αποτυπώνει ένα ώριμο, εξελικτικό engineering narrative:
- η αρχική τοπική υλοποίηση απέδειξε την τεχνική εφικτότητα και παρήγαγε τα βασικά KPIs,
- η δεύτερη φάση μετέτρεψε την πλατφόρμα σε custom, cloud-based Smart Campus SaaS,
- το openHAB παραμένει κρίσιμο ως semantic middleware και integration layer,
- η νέα πλατφόρμα δίνει έμφαση σε usability, interoperability, AI-enabled analytics και scalable access,
- και το συνολικό όραμα οδηγεί σταδιακά προς ένα πιο ολοκληρωμένο Cognitive Digital Twin.
