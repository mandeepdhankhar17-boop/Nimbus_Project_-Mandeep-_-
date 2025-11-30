# pps-project student attendance manager.
#include <stdio.h>
#include <string.h>

#define maxn 50
#define maxd 15
#define maxs 200

struct Student {
    long long id;
    char name[maxn];
};

struct Record {
    long long id;
    char date[maxd];
    char status;
};

void loadStudents(struct Student s[], int *n) {
    FILE *f = fopen("students.dat", "r");
    *n = 0;
    if (!f) return;

    while (fscanf(f, "%lld|%49[^\n]\n", &s[*n].id, s[*n].name) == 2) {
        (*n)++;
        if (*n >= maxs) break;
    }
    fclose(f);
}

void saveStudents(struct Student s[], int n) {
    FILE *f = fopen("students.dat", "w");
    if (!f) return;

    for (int i = 0; i < n; i++)
        fprintf(f, "%lld|%s\n", s[i].id, s[i].name);

    fclose(f);
}

void addStudent(struct Student s[], int *n) {
    long long id;
    char name[maxn];

    printf("ID: ");
    scanf("%lld", &id);
    getchar();

    printf("Name: ");
    fgets(name, MAXN, stdin);
    name[strcspn(name, "\n")] = '\0';

    s[*n].id = id;
    strcpy(s[*n].name, name);

    (*n)++;
    saveStudents(s, *n);

    printf("Added.\n");
}
