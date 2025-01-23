---
layout: project
type: project
image: img/moneylogo.webp
title: "Pokedex Application (C)"
date: 2024
published: true
labels:
  - C
  - Vim

summary: "Pokedex File Storage"
---

<div style="text-align: center; margin-bottom: 20px;">
  <img class="img-fluid" src="../img/Bank.webp" alt="Bank Logo" style="width: 150px; height: auto; border: 1px solid #ccc; padding: 10px; border-radius: 5px;">
</div>


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
Upon reopening the application it would restore all the pokemon and it's data back to the array. The function stops when pokeArray 
is full or the EOF is reached and it returns how many pokemon it stored in the array. 
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


