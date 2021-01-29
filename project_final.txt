#include<stdio.h>
#include<string.h>
#include<stdlib.h>


double price[7] = {58.30 , 120.56 , 78.05 , 53.70 , 12.00 , 99.00 , 67.00 };
double mealTaxPrices[7];
int personnumber;




void printMeals();
void orderMeals();
double orderForPerson();
int main()
{
    char response = 'y';


     printMeals();
     while(response == 'y'|| response == 'Y')
    {
            printf("please enter number of person  :");
            scanf("%d",&personnumber);


            orderMeals();

            printf("\nwould you like to continue(y/n):");
            scanf("\n%c",&response);
    }

 printf("\n      ************** THANK YOU FOR COMING PARVEZ'S RESTURENT *************************\n");
 printf("\20**********************   PLEASE VISIT US NEXT TIME  **************************\20 \n");
   system("pause");
   return 0;
}

void printMeals()
{

      printf("@*******************  WELCOME TO PARVEZ'S RESTURANT **************************@\n");
      printf(" \t\t\tthe menue is below:@\n");
      printf(" \t\t\t MEALS\t\t\tPRICE:\n");
      printf(" \t\t\t \22*******************************\22\n");
      printf(" \t\t\t 1- Shwarma\t\t58.30\n");
      printf(" \t\t\t 2- Pizza\t\t120.56\n");
      printf(" \t\t\t 3- Fried-chicken\t78.05\n");
      printf(" \t\t\t 4- ice-cram\t\t53.70\n");
      printf(" \t\t\t 5- drinks\t\t12.00\n");
      printf(" \t\t\t 6- Pesta\t\t99.00\n");
      printf(" \t\t\t 7- Burger\t\t67.00\n");



      printf("\n");
}
void orderMeals()
{
    char promocode;
    char reviewc[500];
    char review;
    char promo;
    FILE *fp;
	double totalPriceForPerson, totalPriceForChildren;
	double allPayment,discount;
         printf("                      \t\t**** ORDER MENUE****\n");


        totalPriceForPerson =  orderForPerson();
		allPayment = totalPriceForPerson;

     printf("\n \t\t     \22**************************************\22    \n");
     printf(" \t\t   ******************  final BILL   ************      \n");
     printf(" \t\t\tperson\t\tcount\t\ttotal price\n");
     printf(" \t\t\tperson\t\t%d\t\t%5.2f\n",personnumber,totalPriceForPerson);
     printf(" \t\t\tTotal bill\t\t\t%5.2f\n",allPayment );

      printf("\nhave you any promocode (y/n): ");
      fflush(stdin);
      scanf("%c", &promo);
      if(promo=='y' && 'Y'){
            printf("\nenter your promocode: ");
            fflush(stdin);
            scanf("%c", &promocode);


     if(promocode == 'a')
		 discount=((allPayment * 10.64)/100);
     else if(promocode=='b')
          discount=((allPayment * 7.5)/100);
     else if(promocode=='c')
          discount=((allPayment * 5.9)/100);
     else if(promocode=='d')
          discount=((allPayment * 12.37)/100);
	 else
		  printf("wrong promo.....!!!!");

      }

          printf(" \t\t\tTotal bill after discount\t%5.2f\n",allPayment-discount);

      printf("\ndo you want to review(y/n):");
      fflush(stdin);
      scanf("%c", &review);

      if(review=='y' && 'Y'){
        printf("\n enter your review: ");
        fflush(stdin);
        gets(reviewc);
      }


      fp=fopen("review.txt", "a+");
      fprintf(fp,"%s\n", reviewc);
}
double orderForPerson()
{
     int menuOption,i,amount;
     char element, elements;
      char response = 'y';
      double totalPerPerson = 0.0,totalAllPerson = 0.0;
      double tax = 5.0;
      if(personnumber <=0)
		   printf("\n ");
	  else
      printf("*\tperson:\n");
      for(i=0;i<personnumber;i++)
     {
               printf("person %d please enter your orders\n",i+1);
               while(response == 'y' || response == 'Y')
               {
                              printf("please enter your option:");
                              scanf("%d",&menuOption);
							  if(menuOption<1 || menuOption>7)
							  {
								  printf("sorry we don't have this order \nagain! ");
								  continue;
							  }

							  printf("\ndo you want to change element of salad & chease(y/n): ");
							  fflush(stdin);
							  scanf("%c", &element);

							  if(element=='y' && 'Y')
                              {
                                  printf("\nhow amount yo want(a=20%%,b=40%%,c=60%%,d=80%%): ");
                                  fflush(stdin);
                                  scanf("%c", &elements);

                                  if(elements=='a')
                                    printf("\nyou choose 20%% amount salad & chees!!!\n");
                                  else if(elements=='b')
                                     printf("\nyou choose 40%% amount salad & chees!!!\n");
                                  else if(elements=='c')
                                     printf("\nyou choose 60%% amount salad & chees!!!\n");
                                  else if(elements=='d')
                                     printf("\nyou choose 80%% amount salad & chees!!!\n");
                                else
                                    printf("you given wrong....");


                              }


                              printf("\nplease enter your amount of order:");
                              scanf("%d",&amount);


                           totalPerPerson = totalPerPerson + (amount * price[menuOption - 1] );

                              printf("\nWould you like to enter more orders(y/n):");
                              scanf("\n%c",&response);



               }
               printf("\n");
               totalAllPerson += totalAllPerson +  totalPerPerson;
               totalPerPerson = 0.0;
               response = 'y';
     }

     return totalAllPerson + ((totalAllPerson * tax) / 100);
}
