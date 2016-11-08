créer un script qui permette de créer une nouvelle vagrant de la configurer et de la lancer.

#sript
```bash
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
```
#Script v2.0
```bash
#!/bin/bash

nbDossier=3
nbDossierLocal=3
nbDossierDistant=3

echo "###################################"
echo "#                                 #"
echo "#    BIENVENUE SUR NOTRE SCRIPT   #"
echo "#                                 #"
echo "###################################"
echo ""
read -p "Press Enter to continue"

#Demande a l'utilisateur comment appeler le dossier
echo "Comment voulez-vous appeler votre dossier ?"
read nomDuDossier

#Gestion de l'erreur dans le cas ou le nom du dossier a un ou des espaces
    while [[ "$nomDuDossier" != "${nomDuDossier/ /}" ]]
    do
        if [ $nbDossier -gt 1 ]; then 
          let "nbDossier--"
          echo  "Votre nom de dossier ne doit pas contenir d'espaces. Il vous reste {$nbDossier} chance."
          read nomDuDossier
        fi
        
        if [ $nbDossier -le 1 ]; then
          exit 1
        fi
    done

#Demande quels boxe utiliser
echo "Entrez le nom de la box vagrant que vous souhaitez utiliser, laissez vide si vous voulez la base."
read nomServeur

#Demande le nom du dossier synchro de la machine local
echo "Entrez le nom de votre fichier synchronisé en local."
read fichierLocal

#Gestion de l'erreur dans le cas ou le nom du dossier a un ou des espaces
    while [[ "$fichierLocal" != "${fichierLocal/ /}" ]]
    do
        if [ $nbDossierLocal -gt 1 ]; then
          let "nbDossierLocal--"
          echo  "Votre nom de dossier ne doit pas contenir d'espaces. Il vous reste {$nbDossierLocal} chance."
          read nomDuDossier
        fi
        
        if [ $nbDossierLocal -le 1 ]; then
          exit 1
        fi
    done

#Demande le nom du dossier synchro de la machine virtuelle
echo "Entrez le nom de votre fichier synchronisé distant. Laissez vide si vous souhaitez, par défaut dans /var/www/html"
read fichierDistant

#Gestion de l'erreur dans le cas ou le nom du dossier a un ou des espaces
    while [[ "$fichierDistant" != "${fichierDistant/ /}" ]]
    do
        if [ $nbDossierDistant -gt 1 ]; then
          let "nbDossierDistant--"
          echo  "Votre nom de dossier ne doit pas contenir d'espaces. Il vous reste {$nbDossierDistant} chance."
          read nomDuDossier
        fi
        
        if [ $nbDossierDistant -le 1 ]; then
          exit 1
        fi
    done

echo "Patientez."
mkdir $nomDuDossier
cd $nomDuDossier
vagrant init
  if [ -z "$nomServeur" ]; then
    nomServeur="base"
  fi


sed -i "s/config.vm.box = \"base\"/config.vm.box = \"$nomServeur\"/g" Vagrantfile
sed -i "s/# config.vm.network \"private_network\", ip: \"192.168.33.10\"/config.vm.network \"private_network\", ip: \"192.168.33.10\"/g" Vagrantfile

  if [ -z "$fichierDistant" ]; then
    sed -i "s/# config.vm.synced_folder \"..\/data\", \"\/vagrant_data\"/config.vm.synced_folder \"$fichierLocal\", \"\/var\/www\/html\"/g" Vagrantfile
  fi

  if [ -n "$fichierDistant" ]; then
    sed -i "s/# config.vm.synced_folder \"..\/data\", \"\/vagrant_data\"/config.vm.synced_folder \"$fichierLocal\", \"\/var\/www\/html\/$fichierDistant\"/g" Vagrantfile
  fi
  
mkdir $fichierLocal
vagrant up
```

#README

Script pour lancer un serveur Vagrant, avec plusieurs Options.

-gt (GreaterThan) //Plus grand que

-le (LowerEqual) // Plus petit ou égal

Boucle utilisé : If/While

Pas réussis a me servir des fonctions.
