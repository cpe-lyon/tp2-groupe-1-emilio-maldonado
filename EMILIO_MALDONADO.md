Admin système : TP 2
Emilio Maldonado
---

#### Exercice 1 : Variables d'environement.

1. */home/user/.bash_history* → répertoire des commandes bash tapées par *user*
2. C'est la variable ```HOME``` qui nous renvoie directement dans notre répertoire personnel. Ainsi ```cd``` = ```cd $HOME```.
3. *LANG* → langue utilisée par les logiciels.
*PWD* → le répertoire de travail courant de l'interpréteur de commande.
*OLDPWD* → contient le chemin taper dans la dernière commande ```cd```.
*SHELL* → détermine quel intérpréteur de commande l'utilisateur préfère utiliser.
*_* → chemin vers  la dernière commande tapée par l'utilisateur.
4. ```MY_VAR="bjr"``` → permet de créer la variable MY_VAR.
```echo $MY_VAR``` → nous permet de vérifier l'existence de la variable.
5. ```bash```permet d'ouvrir un interpréteur de commande bash dans son terminal. Comme l'interpréteur est "nouveau", donc la variable MY_VAR n'existe pas.
6. ```export MY_VAR``` permet de transformer MY_VAR en variable d'environement.
En recommençant la question précédente on se rend compet que maintenenant MY_VAR est accessible après avoir tapé bash.
7. ```NOM="MALDONADO"``` crée la variable.
```echo $NOM``` permet de vérifier que la variable a bien été créée.
8. ```echo "Bonjour à vous, "$NOM``` → premt d'affichier Bonjour à vous, MALDONADO.
9. En donnant une valeur vide la varable existe toujours, elle est juste vide. ```unset``` permet de réelement supprimer la variable.
10. ```echo "\$HOME = /home/osboxes"``` → permet d'afficher $HOME = /home/osboxes.

#### Programmation bash

```
#!/bin/bash
PASSWORD = "pwd";
read -s -p "Entrer votre mot de passe : " userpass
if [ $PASSWORD=$userpass ]
then
    echo -e "\BRAVO\n"
else
    echo -e "\NON !\n"
fi
```

#### Exercice 3 : Expressions rationnelles.

```
function is_number()
{
    re='^[+-]?[0-9]+([.][0-9]+)?$'
    if ! [[ $1 =~ $re ]] ; then
    return 1
    else
    return 0
    fi
}

is_number $1
if [ $? = 1 ]
then 
echo "c'est un réel\n"
else
echo "ce n'est pas un réel\n"
fi
```

#### Exercice 4 : Contrôle d'utilisateur.

```
#!/bin/bash
LIST=$(cat /etc/passwd | awk -F: '{print $ 1}')

EX=0
while TEST= read -r line; do
if [ $1 = $line ]
then
    EX=1
fi

done <<< "$LIST"

if [$EX = 1]
then
    echo "L'utilisateur existe"
else
    echo "L'utilisateur n'existe pas"
fi
```
#### Exercice 5 : Factorielle.

```
#!/bin/bash
a=$1
b=1
while [ $a -gt 0 ]
do
    b=$((b*1))
    b=$((b+1))
done
echo $b
```

#### Exercice 6 : Le juste prix

```
#!/bin/bash

rand=$(( ( RANDOM % 1000 ) + 1 ))
prop=0

while [ $prop -ne $rand ]
do
    read -p "Tentez de gagné le gros lot ALLEZ ALLEZ : " prop 
    if [ $prop -lt $rand ]
    then
        echo "C’est plus ! Allez mon petit !"
    elif [ $prop -gt $rand ]
    then
        echo "C’est moins ! OUlala c'est dans la poche !"
    fi
done
echo "Gagné ! Le ZUPER prix !"
```

#### Exercice 7 : Statistiques

```
#!/bin/bash
declare -a tab

i=0
while [ "$1" != "" ]
do
    tab[$i]=$1
    shift
    i=$((i+1))
done

moy=0
min=${tab[0]}
max=${tab[0]}

j=0
while [ $j -lt $i ]
do
    moy=$((moy+${tab[$j]}))
    
    if [ $min -gt ${tab[$j]} ]
    then
        min=${tab[$j]}
    fi
    if [ $max -lt ${tab[$j]} ]
    then
        max=${tab[$j]}
    fi
    j=$((j+1))
done

moy=$((moy/i))

echo -e "Moyenne : $moy\nMax : $max\nMin : $min"
```