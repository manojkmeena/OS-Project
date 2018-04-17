#include <stdio.h>
#include <sys/types.h>
#include <unistd.h>
#include <sys/wait.h>
int main()
{
   int i,num;
   pid_t pid;

   printf("Enter a number:\n");
   scanf("%d", &num);

   if (num < 0)
      printf("Please enter a non-negative integer!\n");
   else
   {
      pid = fork();
      if (pid == 0)
      {
         //printf("Child is producing the Fibonacci Sequence...\n");
         while (num>0)
         {
            printf("%d ",num);
	    num = num/2;
         }
         printf("Child ends\n"); 
      }
      else 
      {
         printf("Parent is waiting for child to complete...\n");
         wait(NULL);
         printf("Parent ends\n");
      }
   }
   return 0;
}
