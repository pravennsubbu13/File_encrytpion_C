#include <math.h>
#include <stdio.h>
#include <stdlib.h>
#include <string.h>
#include <unistd.h>
long int p,q,n,t,flag,e[100],d[100],temp[100],j,m[100],en[100],i;
long int tempp[100];
void decrypt();

int prime(long int pr) 
{ 
    int i; 
    j=sqrt(pr); 
    for(i=2;i<=j;i++) 
    { 
        if(pr%i==0) 
            return 0; 
    } 
    return 1; 
}
long int cd(long int x) 
{ 
    long int k=1; 
    while(1) 
    { 
        k=k+t; 
        if(k%x==0) 
            return(k/x); 
    } 
} 

void ce() 
{ 
    int k; 
    k=0; 
    for(i=2;i<t;i++) 
        {
            if(t%i==0)
                continue;
                flag=prime(i);
            if(flag==1&&i!=p&&i!=q)
            {
                e[k]=i; flag=cd(e[k]);
                if(flag>0) 
        { 
            d[k]=flag; 
            k++; 
        } 
        if(k==99) 
            break; 
        } 
    } 
}

int main() {
  char msg[100];
  FILE *f;//read encrypted values
  int inc=0;
  FILE *tt;//read temp values
  long int k;

  f = fopen("encrypt.txt", "r");
  int jk;
  int ch;
  printf("\n");
  do {
    ch = fgetc(f);
    en[inc] = ch;
    inc = inc + 1;
  } while (ch != EOF);
  fclose(f);
  
  tt=fopen("temp.txt","r");
  int inn=2;
  int gh;
  do {
    gh = getw(tt);
    tempp[inn] = gh; 
    inn = inn + 1;
 
    } while (gh != EOF);
  int sd=0;
  printf("\n");
  for(int lo=0;lo<inn-3;lo++)
    {
      if(tempp[lo]==0)
      {
        continue;
      }
      else{
      temp[sd]=tempp[lo];
        }
    sd++;
    }
  
  p=7;
  q=11;
  n=p*q;
  t=(p-1)*(q-1);
  ce();
  printf("\n");
  fclose(tt);
  
  
  decrypt();
}

void decrypt()
{ 
    long int pt,ct,key=d[0],yy; 
    i=0; 
    while(en[i]!=-1) 
    { 
        ct=temp[i]; 
        yy=1; 
        for(j=0;j<key;j++) 
        { 
            yy=yy*ct; 
            yy=yy%n; 
        } 
        pt=yy+96; 
        m[i]=pt; 
        i++; 
    } 
    m[i]=-1;
  
    printf("\nTHE DECRYPTED MESSAGE IS\n"); 
    for(i=0;m[i]!=-1;i++)
      
        printf("%c",m[i]);
}