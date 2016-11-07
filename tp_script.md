créer un script qui permette de créer une nouvelle vagrant de la configurer et de la lancer.

#Contenu attendu
-Script avec variables

- choix de differentes options via input

#Aller plus loin
#!/bin/bash

#Demande a l'utilisateur comment appeler le dossier
echo "Comment voulez-vous appeler votre dossier"
read nomDuDossier

#Demande quels boxe utiliser
echo "Entrez le nom de la box vagrant que vous souhaitez utiliser, laissez vide si vous voulez la base"
read nomServeur

#Demande le nom du dossier synchro de la machine local
echo "Entrez le nom de votre fichier synchro local"
read fichierLocal

#Demande le nom du dossier synchro de la machine virtuelle
echo "Entrez le nom de votre fichier synchro distant"
read fichierDistant
fichierLocal="/var/www/html/${fichierDistant}"

mkdir $nomDuDossier
cd $nomDuDossier
vagrant init
  if [ -z "$nomServeur" ];
  then
  	nomServeur="base"
  fi
sed -i-e "s/config.vm.box = \"base\"/config.vm.box = \"$nomServeur\"/g" Vagrantfile
sed -i-e "s/# config.vm.network \"private_network\", ip: \"192.168.33.10\"/config.vm.network \"private_network\", ip: \"192.168.33.10\"/g" Vagrantfile
sed -i-e "s/# config.vm.synced_folder \"../data\", \"/vagrant_data\"/config.vm.synced_folder \"$fichierLocal\", \"/var/www/html/$fichierDistant\"/g" Vagrantfile
mkdir $fichierLocal
vagrant up


#sript

#!/bin/bash

#Demande a l'utilisateur comment appeler le dossier
echo "Comment voulez-vous appeler votre dossier"
read nomDuDossier

#Demande quels boxe utiliser
echo "Entrez le nom de la box vagrant que vous souhaitez utiliser, laissez vide si vous voulez la base"
read nomServeur

#Demande le nom du dossier synchro de la machine local
echo "Entrez le nom de votre fichier synchro local"
read fichierLocal

#Demande le nom du dossier synchro de la machine virtuelle
echo "Entrez le nom de votre fichier synchro distant"
read fichierDistant
fichierLocal="/var/www/html/${fichierDistant}"

mkdir $nomDuDossier
cd $nomDuDossier
vagrant init
  if [ -z "$nomServeur" ];
  then
  	nomServeur="base"
  fi
sed -i-e "s/config.vm.box = \"base\"/config.vm.box = \"$nomServeur\"/g" Vagrantfile
sed -i-e "s/# config.vm.network \"private_network\", ip: \"192.168.33.10\"/config.vm.network \"private_network\", ip: \"192.168.33.10\"/g" Vagrantfile
sed -i-e "s/# config.vm.synced_folder \"../data\", \"/vagrant_data\"/config.vm.synced_folder \"$fichierLocal\", \"/var/www/html/$fichierDistant\"/g" Vagrantfile
mkdir $fichierLocal
vagrant up
