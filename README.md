# Get Next Line

## Description
`get_next_line` est une fonction en C permettant de lire une ligne d'un descripteur de fichier, peu importe sa taille. Elle est souvent utilisée pour la lecture de fichiers texte ligne par ligne.

## Fonctionnalités
- Lit une ligne d'un fichier à la fois.
- Compatible avec n'importe quel descripteur de fichier valide.
- Utilise un buffer de taille définie (`BUFFER_SIZE`).
- Gère les lectures partielles et les fins de fichier correctement.

## Prototype
```c
char *get_next_line(int fd);
```
```sh
gcc -Wall -Wextra -Werror -D BUFFER_SIZE=42 get_next_line.c get_next_line_utils.c -o gnl
```
## Utilisation
```c
#include <stdio.h>
#include <fcntl.h>
#include "get_next_line.h"

int main(void)
{
    int fd = open("file.txt", O_RDONLY);
    char *line;
    
    if (fd == -1)
        return (1);
    
    while ((line = get_next_line(fd)))
    {
        printf("%s", line);
        free(line);
    }
    close(fd);
    return (0);
}
```

## Gestion de la mémoire

- Chaque ligne retournée par `get_next_line` doit être libérée avec free().
- Une fois la lecture terminée, la dernière valeur retournée sera `NULL`.
