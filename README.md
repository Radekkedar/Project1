# Project1
```C
#include <stdio.h>
#include <stdlib.h>
#include <string.h>

typedef struct Man{
    char* name;
    char* surname;
    char* age;
    char* dsize;
}Man;

FILE* openFile(){
    FILE *file = fopen("text.txt" , "r");
    if(file == NULL){
        printf("The file could not be opened");
        exit(1);
    }
    return file;
}

int getLine(char buf[], FILE *file){
    if (fgets(buf, 512, file) != NULL) return 1;
    else return 0;
}

char getWord(char buf[], Man tab_person[], int index) {
    int i = 0;
    char *word;
    const char del[2] = " ";
    word = strtok(buf, del);
    while (word != NULL) {
        if (i == 0) {
            tab_person[index].name = word;
        }
        if (i == 1) {
            tab_person[index].surname = word;
        }
        if (i == 2) {
            tab_person[index].age = word;
        }
        if (i == 3) {
            tab_person[index].dsize = word;
        }
        word = strtok(NULL, del);
        i++;
    }
    return 0;
}

int dump(Man tab_man[]){
    for(int i = 0 ; i < 5 ; ++i){
        printf("%s ", tab_man[i].name);
        printf("%s ", tab_man[i].surname);
        printf("%s ", tab_man[i].age);
        printf("%s ", tab_man[i].dsize);
    }
    return 0;
}

int cmpname(const void *a , const void *b){
    return strcmp( (*(Man*)a).name , (*(Man*)b).name );
}
int cmpsurname(const void *a , const void *b){
    return strcmp( (*(Man*)a).surname , (*(Man*)b).surname );
}

int cmpage(const void *a , const void *b){
    return strcmp( (*(Man*)a).age , (*(Man*)b).age );
}
int cmpdsize(const void *a , const void *b){
    return strcmp( (*(Man*)b).dsize , (*(Man*)a).dsize );
}

int main() {
    Man tab_man[5];
    FILE *file = openFile();
    char buffer[5][512];
    for(int i = 0 ; i < 5 ; ++i){
        getLine(buffer[i] , file);
        getWord(buffer[i] , tab_man, i);
    }
    printf("\nSorted by surname\n\n");
    qsort(tab_man , 5 , sizeof(Man) , cmpsurname);
    dump(tab_man);

    printf("\nSorted by name\n\n");
    qsort(tab_man , 5 , sizeof(Man) , cmpname);
    dump(tab_man);

    printf("\nSorted by age\n\n");
    qsort(tab_man , 5 , sizeof(Man) , cmpage);
    dump(tab_man);

    printf("\nSorted by dick size\n\n");
    qsort(tab_man , 5 , sizeof(Man) , cmpdsize);
    dump(tab_man);

    return 0;
}
```
