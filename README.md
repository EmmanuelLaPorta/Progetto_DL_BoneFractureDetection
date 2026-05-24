# Detection and Localisation of Bone Fractures on X-rays

## Scopo

L'idea del progetto è capire quanto bene un detector può individuare fratture
ossee su radiografie, partendo da qualcosa di semplice e poi salendo di
complessità un pezzo alla volta. Si parte da YOLOv11 in versione Nano, giusto
per fissare un punto di riferimento delle metriche, e si vede come queste
cambiano introducendo via via cross-validation, augmentation pensata per le
X-ray, hyperparameter tuning e modelli più grossi. Alla fine il modello migliore viene messo a
confronto con dei Foundation Models pre-addestrati su immagini mediche, per
avere un'idea di quanto la specializzazione del dominio sposti i risultati
rispetto a un detector generico fine-tuned sul dataset.


## Roadmap

- [X] **Scelta dataset**
  Confrontare i due dataset (bilanciamento, split, annotazioni) e selezionare il migliore. Preprocessare a classe unica `fracture`.

- [X] **Baseline YOLO Nano**
  Allenare YOLO Nano con split fisso train/val/test e registrare mAP50 sul test.

- [X] **K-Fold Cross-Validation**
  Eseguire 5-fold stratificato con stessi iperparametri della baseline per ottenere una stima robusta delle performance.

- [X] **Augmentation**
  Testare configurazioni di augmentation (CLAHE, trasformazioni geometriche, combinazioni) e selezionare quella più stabile.

- [ ] **Scaling modello**
  Provare YOLO Medium per verificare se la capacità del modello è un collo di bottiglia.

- [ ] **Hyperparameter tuning**
  Ottimizzare iperparametri principali (learning rate, batch size, ecc.) partendo dal modello migliore.

- [ ] **Confronto con foundation models**
  Testare modelli pre-addestrati su fratture ossee e confrontare le performance con il proprio modello.


## Setup

Tutti gli allenamenti sono stati eseguiti in locale sulla GPU **NVIDIA GeForce RTX 4070 Laptop**
con **CUDA 12.1** e **PyTorch 2.5.1+cu121**.

Per ricreare l'ambiente:

*python -m venv venv*

*.\venv\Scripts\activate*

*pip install -r requirements.txt*

Il notebook *Progetto_DL_1000081957.ipynb* contiene il resto della configurazione (scaricare i dataset, creazione dei fold, ecc.)
