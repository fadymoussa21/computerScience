#include <stdio.h>
#include <stdlib.h>

int search(int numbers[], int low, int high, int value)
{
    if (high >= low) {
        int mid = low + (high - low) / 2; 
       
        if (numbers[mid] == value)
            return mid;

        if (numbers[mid] > value)
            return search(numbers, low, mid - 1, value);
        return search(numbers, mid + 1, high, value);
    }
    return -1; 
}

void printArray(int numbers[], int sz)
{
    int i;
    printf("Number array: ");
    for (i = 0; i < sz; ++i) {
        printf("%d ", numbers[i]);
    }
    printf("\n");
}

int main(void)
{
    int i, numInputs;
    float average;
    int value;
    int index;
    int* numArray = NULL;
    int countOfNums;
    //FILE* inFile = fopen("c:\\myfiles\\input.txt", "r");
    FILE* inFile = fopen("input.txt","r");

    if (!inFile) {
        printf("Failed to open input file.\n");
        return 1;
    }

    fscanf(inFile, "%d", &numInputs);
    fgetc(inFile); 

    for (i = 0; i < numInputs; ++i) {
        fscanf(inFile, "%d", &countOfNums);
        fgetc(inFile); 

        numArray = (int*)malloc(countOfNums * sizeof(int));
        if (!numArray) {
            printf("Failed to allocate memory.\n");
            return 1;
        }

        average = 0;
        for (int j = 0; j < countOfNums; ++j) {
            fscanf(inFile, "%d", &value);
            numArray[j] = value;
            average += numArray[j];
        }
        fgetc(inFile); 

        printArray(numArray, countOfNums);
        value = (int)(average / (float)countOfNums);
        index = search(numArray, 0, countOfNums - 1, value);
        if (index != -1) {
            printf("Item %d exists in the number array at index %d!\n", value, index);
        }
        else {
            printf("Item %d does not exist in the number array!\n", value);
        }

        free(numArray);
    }

    fclose(inFile);
    return 0;
    }
