# Introduction
L'allocation dynamique permet de réserver dynamiquement (à l'exécution du programme) un espace mémoire permettant de stocker une ou plusieurs variables.

Un exemple d'utilisation de l'allocation dynamique : vous souhaitez que l'utilisateur entre une série de chiffres, mais ne savez pas combien d'éléments comportera cette série. Vous pourriez préparer un certain nombre de places `n`, et occuper uniquement celles qui vous servent — mais cela vous limiterait à `n` entrées, et utiliserait de toute manière la place mémoire pour `n` données. L'allocation dynamique de mémoire vous permet de définir la taille du tableau en cours d'exécution, d'ajouter ou supprimer des entrées, sans limites ou presque. 

Deux fonctions (il en existe d'autres) sont utiles dans le cadre de l'allocation dynamique :
- `malloc`
- `free`

## `malloc`

Prototype : `void* malloc (size_t size);`

`malloc` alloue un bloc mémoire de taille `size` et retourne un pointeur sur le début du bloc.
Le bloc nouvellement alloué n'est pas initialisé. Les valeurs qu'il contien ne sont donc pas prédictible.

Si l'allocation se passe bien `malloc` renvoie le pointeur sur le début du bloc sinon elle renvoie `NULL`.

## `free`

Prototype : `void free (void* ptr);`

`free` libère un bloc mémoire précédemment alloué par un `malloc` et se trouvant à l'adresse `ptr`. L'espace mémoire redevient disponnible pour un autre usage.

**Attention :** `free` ne motifie pas la valeur de `ptr`. 

## Exemple

```C runnable
#include <stdio.h>
#include <stdlib.h>

void main() {
	int *p=NULL;
	int i;
	
	printf("%p\n",p);
	
	p = (int *)malloc(5*sizeof(int));
	
	printf("%p\n",p);

	for (i=0;i<5;i++)
		*(p+i)=i*i;
	
	free(p);
	p=NULL;
}
```

L'exemple ci-dessus alloue un espace mémoire pouvant accueillir 5 entiers. L'espace alloué est ensuite rempli de valeur. L'espace est ensuite libéré.

[Ce lien](https://goo.gl/cx3qau) donne accès à une exécution pas à pas du code avec une vue sur la mémoire.