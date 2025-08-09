# Face-Detection no NN
Sixth Project of the Master in Data Science by Professional.AI

Questo progetto, che si colloca a metà del percorso formativo, è stato per molti aspetti il più complesso. Il modulo formativo è intitolato "Machine Learning: tecniche avanzate" e sono stati trattati i seguenti argomenti: tecniche di ottimizzazione degli iperparametri, basi di MLops, analisi di serie storiche, basi di computer vision, riduzione della dimensionalità e sistemi di raccomandazione.

Il progetto in questione aveva lo scopo di realizzare un algoritmo di face detection per selfie per fotocamere digitali. Per questo progetto non era permesso utilizzare reti neurali né modelli pretrainati, ma solo strumenti della libreria SCIKIT-LEARN. Il modello deve restituire le coordinate del bounding box contenente il volto. Non è stato fornito un dataset ma ho dovuto crearlo in autonomia. In oltre le specifiche consigliavano di ricercare articoli scientifici e non per trovare il metodo più adeguato a questa sfida, non sono state date altre indicazioni.

Per svolgere questo progetto ho prima svolto una ricerca sitografica sia per quanto riguarda il metodo da implementare che i dataset da utilizzare per allenare il mio modello:

1. Preparazione dataset: i dataset utilizzati sono stati: LFW, cifar-100, imagenette. Gli ultimi due sono quelli che contengono le immagini senza volti. Il rapporto tra volti e non volti era di 1 a 4. Non è stata svolta la data augmentation per risorse limitate nella RAM.
2. Estrazione feature HOG e preprocessing: ho definito una classe (preprocessor()), da poter poi inserire nella pipeline, che gestisce il resize della finestra passata, la standardizzazione dei valori dei pixel, l'estrazione delle HOG feature sia per immagini a colori che in bianco e nero.
3. Creazione pipeline SVM con GRID search: dopo aver diviso il dataset in train e test, ho definito una pipeline con la classe preprocessor, una PCA e una GRID search per la linear SVM.
4. Valutazione del modello: il modello è in grado di distinguere tra volti e oggetti. Bisogna però specificare che nel dataset era presente sempre al massino 1 volto.
5. Rilevamento volti con Sliding Window e NMS: per poter utilizzare il mio modello in un caso reale, ho definito la funzione detect_faces() che ha il compito di gestire lo sliding della finestra per scansionare l'immagine in ricerca dei volti e il NMS (non maximum suppression) che unisce le celle con almeno il 30% di sovrapposizione che hanno trovato un volto, essendo questo molto probabilmente lo stesso viso.
6. Test su immagini esterne: I risultati hanno mostrato buone performance, con però delle multirilevazioni per volti con dimensioni molto diverse da quelle di training.
