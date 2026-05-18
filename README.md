# Detection and Localisation of Bone Fractures on X-rays

## Scopo

L'idea del progetto è capire quanto bene un detector può individuare fratture
ossee su radiografie, partendo da qualcosa di semplice e poi salendo di
complessità un pezzo alla volta. Si parte da YOLOv11 in versione Nano, giusto
per fissare un punto di riferimento delle metriche, e si vede come queste
cambiano introducendo via via cross-validation, augmentation pensata per le
X-ray e modelli più grossi. Alla fine il modello migliore viene messo a
confronto con dei Foundation Models pre-addestrati su immagini mediche, per
avere un'idea di quanto la specializzazione del dominio sposti i risultati
rispetto a un detector generico fine-tuned sul dataset.


## Roadmap

- [x] **Analisi e scelta del dataset.** Confrontare i due dataset da Kaggle proposti
  (*mahmudulhasantasin/fracatlas-original-dataset* e *pkdarabi/bone-fracture-detection-computer-vision-project*)
  guardando bilanciamento background/fratturate, qualità degli split,
  struttura delle annotazioni, per scegliere su quale dei due fare il
  training.
  
- [x] **Baseline YOLO Nano.** Allenare YOLOv11-Nano sul dataset *pkdarabi/bone-fracture-detection-computer-vision-project*
  per avere un primo riferimento delle metriche (mAP, Precision, Recall, F1).
  
- [x] **K-Fold Cross-Validation.** Ripetere il training con 5 fold
  stratificati per misurare quanto le metriche dipendano dallo split di
  test (piccolo) piuttosto che dal modello.
  
- [ ] **Augmentation per Nano.** Applicare una pipeline di augmentation
  pensata per X-ray per quantificare il miglioramento rispetto al Nano
  senza augmentation. *Primo tentativo con CLAHE incluso nel notebook: non
  ha migliorato le metriche, da rivedere.*
  
- [ ] **YOLO Medium con augmentation.** Allenare il modello più grosso
  della famiglia con la stessa pipeline di augmentation per misurare il
  guadagno dovuto all'aumento di capacità del modello.
  
- [ ] **Confronto con Foundation Models.** Scaricare da Hugging Face
  modelli pre-addestrati su fratture ossee e confrontarli con il miglior
  modello ottenuto sopra.


## Setup

Tutti gli allenamenti sono stati eseguiti in locale sulla GPU **NVIDIA GeForce RTX 4070 Laptop** 
con **CUDA 12.1** e **PyTorch 2.5.1+cu121**.

Per ricreare l'ambiente:

*python -m venv venv*

*.\venv\Scripts\activate*

*pip install -r requirements.txt*

Il notebook *Progetto_DL_1000081957.ipynb* contiene il resto della configurazione (scaricare i dataset, creazione dei fold, ecc.)


