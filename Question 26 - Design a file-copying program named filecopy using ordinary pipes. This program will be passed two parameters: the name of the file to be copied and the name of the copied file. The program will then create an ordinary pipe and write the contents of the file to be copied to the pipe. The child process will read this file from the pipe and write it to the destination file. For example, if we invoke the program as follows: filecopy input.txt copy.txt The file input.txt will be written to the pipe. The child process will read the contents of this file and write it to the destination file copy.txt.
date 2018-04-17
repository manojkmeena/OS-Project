#include<stdio.h>
#include<sys/types.h>
#include<sys/stat.h>
#include<fcntl.h>
#include<string.h>
#include<stdlib.h>
#include<unistd.h>
#include <sys/wait.h>
#define size 50

int main(int arvuments, char* arv[]) 
{
    int file[2];
    pid_t childid;
    char readBuff[size];
    pipe(file);
    if( arvuments != 3 ) 
    {
        printf("ERROR: Need exactly 2 parameters.\n");
        exit(1);
    }
    int fileOpen = open(arv[1], 0);
    int TargetFile = open(arv[2], O_RDWR|O_CREAT|O_APPEND, 0666);
    if (fileOpen == -1 || TargetFile == -1) 
    {
        printf("File can not be opend\n");
        exit(1);
    }
    childid = fork();
    if (childid == 0) 
    {
        close(file[1]);
	while (read(file[0], readBuff, sizeof(readBuff)) > 0) 
	{
		write(TargetFile, readBuff, strlen(readBuff) - 1);
        }
        close(file[0]);
        close(TargetFile);
    }
    else 
    {
        close(file[0]);
	while (read(fileOpen, readBuff, sizeof(readBuff)) > 0) 
	{
            write(file[1], readBuff, sizeof(readBuff));
            memset(readBuff, 0, size);
        }
        close(file[1]);
        close(fileOpen);
        wait(NULL);
    }
}

/*
// enter the following commands in terminal to run the code
# gcc filecopy.c -o cp
# echo "enter any data here." > input.txt
# ./cp input.txt copy.txt
# cat copy.txt 
*/
