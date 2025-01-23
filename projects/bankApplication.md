---
layout: project
type: project
image: img/moneylogo.webp
title: "Banking Application (C)"
date: 2024
published: true
labels:
  - C
  - Vim

summary: "Bank database application in the C programming language"
---

<div style="text-align: center; margin-bottom: 20px;">
  <img class="img-fluid" src="../img/Bank.webp" alt="Bank Logo" style="width: 150px; height: auto; border: 1px solid #ccc; padding: 10px; border-radius: 5px;">
</div>


This bank application consists of two key files: one that implements various database functions (such as adding, finding, and deleting records) and another that serves as the driver/user-interface file. Upon closing the application, the data is saved to a text file, and memory is deallocated. When the application is restarted, the data is reloaded, restoring the database to its previous state.

This was an individual project I developed for my ICS 212 class. Through this project, I gained valuable experience and improved my technical skills, particularly in pointers and memory management. I also enhanced my practical skills, such as tracing, debugging, and designing effective functions. Additionally, I implemented a debug system using command-line arguments, which streamlined the debugging and maintenance processes.

Later, I recreated this application in C++ to deepen my understanding of the language and explore how references could be applied to improve the design.

Below is an example of the code I used to store the data:

```c
/*****************************************************************
//////// function name: readfile
////////  DESCRIPTION:   A function that reads the information from a  
////////                file and restores it in the database
////////
////////
////////  Parameters:
////////  Struct **start: pointer to the first node in the record list
////////  char filename[]: file being opened and read from
////////
////////  Return values: 0: the file was succesfuly opened and read
////////                 -1: the file could not be opened
////////
****************************************************************/
int readfile(struct record **start, char filename[])
{   
    FILE *file;
    int accountno;
    int result = 0;
    char name[25];
    char address[50];
    struct record *newRecord;
    struct record *last = NULL;
    
    file = fopen(filename, "r");
    if(file == NULL)
    {   
        return -1;
    }
    
    while(fscanf(file,"%d\n", &accountno) == 1)
    {   
        fgets(name, sizeof(name), file);
        name[strcspn(name, "\n")]='\0';
        
        fgets(address, sizeof(address), file);
        address[strcspn(address,"\n")] = '\0';
        
        newRecord = (struct record *)malloc(sizeof(struct record));
        if(newRecord == NULL)
        {   
            fclose(file);
            cleanup(start);
            return -1;
        }
        if (debugMode == 1)
        {   
            printf("Read record: Account No: %d, Name: %s, Address: %s\n", accountno, name, address);
        }
         
        newRecord->accountno = accountno;
        strncpy(newRecord->name, name, sizeof(newRecord->name)-1);
        newRecord->name[sizeof(newRecord->name)-1]='\0';
        strncpy(newRecord->address, address, sizeof(newRecord->address)-1);
        newRecord->address[sizeof(newRecord->address)-1] = '\0';
        newRecord->next = NULL;
        
        if(*start == NULL)
        {   
            *start = newRecord;
        }
        else
        {   
            last->next = newRecord;
        }
    fclose(file);
    if (debugMode == 1)
    {
        printf("DebugMode: Finished reading file '%s'.\n", filename);
    }
    return result;
}
                                             
```

Source Code:[here](https://github.com/alex-edwards-44/academics/blob/main/bankDatabase.c)

