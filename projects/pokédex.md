---
layout: project
type: project
image: img/pokeball.webp
title: "Pokedex Application (C)"
date: 2024
published: true
labels:
  - C
  - Vim

summary: "Pokedex File Storage"
---




This pokedex application took prestored pokemon in a struct array and wrote the data to a text file upon closing the application overwriting any data that was previously there. The write file function would return 0 for success and -1 for unsuccesful. 

Here is the writefile function:

```c
int writefile( struct pokemon pokearray[ ], int sizeOfPokedex, char filename[ ] )
{
    FILE *file;
    int i;

    file = fopen(filename, "w");
    if (file == NULL)
    {
        return -1;
    }
    for(i = 0; i < sizeOfPokedex; i++)
    {
        fprintf(file, "%d\n%s\n", pokearray[i].level, pokearray[i].name);
    }
    fclose(file);

    return 0;
}                                       
```
Upon reopening the application it would restore all the pokemon and it's data back to the array. The function stops when pokeArray is full or the EOF is reached and it returns how many pokemon it stored in the array. Developing this Pokédex application taught me valuable lessons in file handling, memory management, and struct manipulation in C. By implementing functions like writefile and readfile, I gained a deeper understanding of how to work with file streams to save and restore structured data. 
```c
int readfile( struct pokemon pokearray[ ], int* numPokemons, char filename[ ] )
{
    FILE *file;
    int pokemonRead = 0;
    int newLineIndex;
    file = fopen(filename, "r");
    if(file == NULL)
    {
        return -1;
    }


    while(pokemonRead <= *numPokemons && fscanf(file, "%d\n", &pokearray[pokemonRead].level)==1)
    {
        fgets(pokearray[pokemonRead].name, sizeof(pokearray[pokemonRead].name), file);

        newLineIndex = strcspn(pokearray[pokemonRead].name, "\n");
        if (pokearray[pokemonRead].name[newLineIndex] == '\n')
        {
            pokearray[pokemonRead].name[newLineIndex] = '\0';
        }
        pokemonRead++;
    }

    *numPokemons = pokemonRead;
    fclose(file);
    return 0;
}                                 
```



