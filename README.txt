Githup: https://github.com/mbayemakane/Projet_BigData_PySpark_K-Mean/tree/master

-Installation de Anaconda
-Création et activation d’un nouvel environnement
	conda create -n nom_env python=3.9.12
	conda activate nom_env
	conda install jupyter
	conda install -n base nb_conda_kernels

-Installations des packages ci-dessous dans ce nouvel environnement :
	conda install -y -c conda-forge pyspark
	conda install -c conda-forge findspark
	conda install -y -c anaconda pandas
	conda install matplotlib
	conda install -c conda-forge matplotlib
	conda install -c anaconda seaborn
-Ajout du nouvel environnement à jupyter notebook
	pip install --user ipykernel
	python -m ipykernel install --user --name=nom_env
-Mise en place de l'application
Nous avons creer trois class et des méthodes suivantes:
	-SparkClass: Pour le démarage de la session spark
	-Pre_Traiment: Pour le chargement des données et le pré-traitement
	-Traitement: Pour le traitement des données

	#Démarage de la session pyspark(Class SparkClass)
		classSpark = SparkClass() //instention de la class SparkClass
		session = classSpark.createSession() //affectation de la session à un variable(session)

	#Chargement et traitement des données (Class Pre_Traitement)

		#Chargement des données
			fileCSV = "caesarian.csv" //affecter le fichier csv au variable fileCSV
			fileJSON = "people.json" //affecter le fichier json au variable fileJSON
			dataPrep = Pre_Traiment() //instention de la class SparkClass
			df_l = dataPrep.dataFrame(session,fileCSV) //Méthode de chargement des données
			df_l.show(5,False) //Affichage des données charger	
		#Récupération des noms des colonnes dans le variable (cols)
			cols=df_l.columns
		#Récupération des données transformers
			data_trans=dataPrep.transformation(df_l, cols,'features')
		#Affichage des données transformer
			data_trans.show(5,False)


	#Traitement de données(Class Traitement)

		rt=Traitement() //instention de la class Traitement
		#Appel de la méthode k_cluster pour faire un évaluation du model et déterminer le meilleur k(k_ideal) pour entraimer le model
		#Et trace la courbe des scores
		kmax=rt.k_cluster(data_trans) //Métghode permettant de récupérer le k_ideal 
		kmax // Afficher la valeur de k_ideal

		#Affichage de la courbe des composants principal(Courbe des clusters)
		rt.courbe_comp_principal(data_trans,kmax)


