# File-handling
Word line and character counter 
#include <stdio.h>

int main() {
    FILE *fp;
    char ch;
    int lines = 0, words = 0, chars = 0;
    int inWord = 0;

    fp = fopen("input.txt", "r"); // open file (make sure input.txt exists)
    if (fp == NULL) {
        printf("File not found!\n");
        return 1;
    }

    while ((ch = fgetc(fp)) != EOF) {
        chars++;  // count characters

        if (ch == '\n')
            lines++;  // count lines

        if (ch == ' ' || ch == '\n' || ch == '\t') {
            if (inWord) {
                words++;
                inWord = 0;
            }
        } else {
            inWord = 1;
        }
    }

    if (inWord)  // last word if file doesn’t end with space
        words++;

    fclose(fp);

    printf("Lines = %d\n", lines);
    printf("Words = %d\n", words);
    printf("Characters = %d\n", chars);

    return 0;
}
