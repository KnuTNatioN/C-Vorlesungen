# Zeigerarithmetik

```C
int a[5] = {11,23,34,48,59};
int *z;
z = a;  //erste adresse von a wird in z gepackt

printf("*z     = %d         *a     = %d\n", *z, *a);
printf("*(z+2) = %d         *(a+2) = %d\n", *(z+2), *(a+2));
printf("*z+2   = %d         *a+2   = %d\n", *z+2, *a+2);
```
RESULT:
> *z     = 11         *a     = 11
> 
> *(z+2) = 34         *(a+2) = 34 //verschiebt zeiger um 2 mal int
> 
> *z+2   = 13         *a+2   = 13
> 
> //dereferenzierung ist "stärker" als adition -> erst wert dann plus 2 dann ausgabe

