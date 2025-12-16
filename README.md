# Használt autók árkategóriájának becslése gépi tanulással

## Projekt leírása
A projekt célja egy gépi tanulás alapú osztályozó modell készítése, amely használt autók hirdetési adatai alapján becsüli meg az autó árkategóriáját.  
A modell három kategóriába sorolja az autókat: **olcsó**, **közepes** és **drága**.

A megoldás neurális hálót alkalmaz, amely képes egyszerre kezelni numerikus és kategorikus jellemzőket.

A feladat osztályozási problémaként került megfogalmazásra, mivel az árakat előre definiált kategóriákba (olcsó, közepes, drága) soroltuk, és a cél ezen kategóriák felismerése volt, nem a pontos árérték becslése.


---

## Felhasznált adatok
Az adathalmaz a Kaggle oldalról származik:

- Dataset neve: *Secondhand car market data parsing dataset*
- Forrás: https://www.kaggle.com/datasets/attilakiss/secondhand-car-market-data-parsing-dataset-v1

A projekt során a fő hirdetési táblát használtuk, amely tartalmazza többek között:
- gyártási évet
- futásteljesítményt
- motoradatokat
- ajtók és férőhelyek számát
- márkát, modellt, váltót és színt

---

## Adatelőkészítés
Az adatok feldolgozása az alábbi lépésekből állt:

- hiányzó és hibás értékek kezelése
- irreális rekordok eltávolítása
- statisztikai outlier szűrés (IQR módszer)
- domain-alapú szűrés (extrém futásteljesítmény és motoradatok)
- célváltozó (`ar_kategoria`) létrehozása az ár alapján
- train / validation / test felosztás (70% / 15% / 15%)

---

## Modell
A megoldás egy TensorFlow alapú neurális háló, amely:
- a numerikus jellemzőket normalizálja
- a kategorikus jellemzőket embedding rétegekkel reprezentálja
- több rejtett réteget és regularizációt (Dropout, Batch Normalization) alkalmaz
- EarlyStopping technikával kerül tanításra

A betanított neurális háló modell a Keras natív `.keras` formátumban került elmentésre.


---

## Eredmények
A végső modell teljesítménye a teszt halmazon:

- **Pontosság (accuracy): ~88.6%**

A modell jól generalizál, a validációs és teszt eredmények közel azonosak.  
A részletes kiértékeléshez tanulási görbék és konfúziós mátrix is készült.

---
'''
## Projekt struktúra
beadando_gepi_tanulas/
├── adatok/        # Adatfájlok
├── jegyzetek/     # Jupyter notebook
├── kepek/         # Kimeneti ábrák (pontosság, veszteség, konfúziós mátrix)
├── modell/        # Elmentett neurális háló modell
├── venv_beadando/ # Virtuális környezet
└── README.md
'''

---

## Futtatás
A projekt futtatásához szükséges:
- Python 3.x
- TensorFlow
- pandas
- scikit-learn
- matplotlib
- seaborn

A teljes folyamat a `jegyzetek` mappában található Jupyter notebook futtatásával reprodukálható.

A projekt fejlesztése és futtatása külön Python virtuális környezetben (`venv_beadando`) történt.

---

## Következtetés
A projekt során sikerült egy stabil és pontos osztályozó modellt készíteni, amely alkalmas használt autók árkategóriájának becslésére.  
A módszer továbbfejleszthető például regressziós feladattá alakítással vagy további jellemzők bevonásával.
