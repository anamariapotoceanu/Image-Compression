# Image-Compression

## Tema 2, Metode numerice  

### Task 1 
În cadrul acestei cerințe, am implementat funcția `task1(photo, k)`, care 
are ca scop compresia unei imagini folosind descompunerea redusă a valorilor 
singulare. `photo` reprezintă imaginea care este dată sub forma unei matrici, 
iar `k`, numărul valorilor singulare. Am aplicat algoritmul SVD asupra matricii 
care calculează matricile reduse `U`, `S`, `V`. `U` și `V` sunt matrici ortogonale, 
iar `S` matrice diagonală. Mai departe, am calculat `new_X` care reprezintă  
aproximarea matricei inițiale `photo`. Ne-am folosit de matricile obținute  
anterior, în urma aplicării algoritmului SVD. În final, am trasformat matricea 
în `uint8`, pentru a reprezenta o imagine validă. 

### Task 2 
În cadrul acestui task, am implementat funcția `task2(photo, pcs)`. Prima 
dată am făcut cast la `double` pentru matricea inițială `photo`. A urmat algoritmul 
de normalizare. Mai exact, pentru fiecare rând în parte am calculat media, cu 
ajutorul funcției `mean`. Rezultatele le-am reținut într-un vector coloana, 
denumit `avg`. După aceea, am scăzut din matricea inițială media fiecărui rând. 
Am aflat matricea `Z` cu ajutorul formulei din enunțul temei. Am aplicat  
algoritmul SVD asupra lui `Z`, care calculează matricile reduse `U`, `S`, `V`. 
Am construit matricea `W` din primele `pcs` coloane ale lui `V`, urmând să calculăm 
matricea `Y`, care reprezintă proiecția lui `A` în spațiul componentelor principale. 
Am aproximat matricea inițială, adăugând la fiecare rând media sa. În final, 
am trasformat matricea în `uint8`, pentru a reprezenta o imagine validă. 

### Task 3 
În cadrul acestui task, am implementat funcția `task3(photo, pcs)`. Inițial, 
am făcut cast la `double` pentru matricea inițială `photo`. A urmat procesul de 
normalizare, care este același ca la `task2`, mai exact, s-a calculat media 
fiecărui rând, cu ajutorul căreia am normalizat matricea inițială. Am scăzut 
din matricea inițială media fiecărui rând. Mai departe, am calculat matricea 
de covarianță conform formulei din enunțul temei. Am calculat vectorii și  
valorile proprii ale matricei de covarianță, folosind funcția `eig`. 
Am ordonat descrescător valorile proprii, folosind funcția `sort`. Apoi, am creat 
matrice `V` formată din vectorii proprii așezați pe coloane. Matricea `W` 
am construit-o din primele `pcs` coloane ale lui `V`. Am schimbat baza matricei 
inițiale, mai exact am creat matricea `Y`, aplicând formula corespunzătoare. 
Am aproximat matricea inițială, adăugând media rândurilor. În final, 
am trasformat matricea `new_X` în `uint8`, pentru a reprezenta o imagine validă. 

### Task 4 
Funcția `prepare_data(name, no_train_images)` 
La început au fost inițializate matricea `train_mat` și vectorul `train_val`. 
Apoi, am încărcat datele din tabelul primit ca argument, folosind funcția `load`. 
În matricea `train_mat` am păstrat primele `no_train_images` linii din 
tabelul de imagini de antrenament, adică `X`, iar în vectorul `train_val` primele 
`no_train_images` valori ale vectorului de etichete, adică `Y`. 

Funcția `visualise_image(train_mat, number)` 
Am citit din matricea de antrenament linia cu numărul `number`, primit ca 
argument. Mai departe, am transformat linia citită într-o matrice 28x28, 
folosind funcția `reshape`. Am calculat transpunerea acestei matrici și am 
transformat-o în `uint8` pentru a fi o imagine validă. 

Funcția `prepare_photo(im)` 
În această funcție, am inversat pixelii imaginii, am calculat transpunerea, 
iar apoi am transformat imaginea într-un vector linie, folosind funcția `reshape`. 

Funcția `magic_with_pca(train_mat, pcs)` 
În cadrul acestei funcții, am calculat media fiecărei coloane a matricii, 
pe care am scăzut-o din matricea inițială. Am aflat matricea de covarianță,  
conform formulei din enunțul temei. Am calculat vectorii și valorile proprii 
ale matricei de covarianță, folosind funcția `eig`. Am ordonat descrescător 
valorile proprii, folosind funcția `sort`. Am creat matrice `V` formată din  
vectorii proprii așezați pe coloane. Matricea `W` am construit-o din primele `pcs` 
coloane ale lui `V`. Am schimbat baza matricei inițiale, mai exact am aflat 
matricea `Y`. Am calculat în final matricea `train`, folosind formula. 

Funcția `KNN(labels, Y, test, k)` 
Pentru fiecare rând din matricea `Y` primită ca parametru, am calculat 
distanța Euclidiană dintre acesta și vectorul de test primit ca argument. 
Pentru a calcula distanța am folosit formula din enunț. Am ordonat crescător 
distanțele, folosind funcția `sort` și am reținut într-un vector primele 
`k` valori. Mai departe, am aflat valorile corespunzătoare. În final, am calculat 
predicția ca mediana celor `k` valori cele mai apropiate, folosind funcția `median`. 

Funcția `classifyImage(im, train_mat, train_val, pcs)` 
În această funcție, am folosit funcția implementată anterior, 
`magic_with_pca`, pentru setul de date de antrenament. Apoi, am scăzut din 
vectorul imagine media fiecărei coloane din `train_mat`, mai exact `miu`. Am 
schimbat baza, iar în final am calculat predicția cu ajutorul funcției `KNN`.
