zdf
===

First
#include <iostream> 
#include <string>
#include <cmath>  
using namespace std;   
const int c = 4;  
double number[c];   
string ex[c];   
bool j = false;      
int count = 0;        
void Search(int n)  
{         
	if (n == 1)  
	{             
		if ( fabs(number[0] - 24)<=1E-6   )  
		{                    
			cout << ex[0]<<"\t\t";     
			j = true;     
			count ++;      
			if((count % 3)==0)  
			{
				cout<<endl; 
			}
		}
	}   
	for(int i=0; i < n; i++)  
	{             
		for (int j = i + 1; j < n; j++) 
		{                         
			double a,b;             
			string expa,expb;        
			a = number[i];              
			b = number[j];                 
			number[j] = number[n-1]; 
			expa = ex[i];                  
			expb = ex[j];                    
			ex[j] = ex[n-1];
			ex[i] = '('+expa+'+'+expb+')';
			number[i] = a + b;          
			Search(n-1);                            
			ex[i]='(' +expa + '-' + expb + ')';
			number[i] = a - b;              
			Search(n-1);                                                 
			ex[i] = '(' +expb+ '-'+ expa  + ')';
			number[i] = b - a;          
			Search(n-1);                                                                
			ex[i] = '(' + expa + '*' + expb +')';   
			number[i] = a * b;                    
			Search(n-1);      
			if (b != 0)     
			{              
				 ex[i] ='('+expa+ '/'+expb   +   ')';  
				 number[i] = a / b;                             
				 Search(n-1);                         
			}                         
			if (a != 0)       
			{                    
				 ex[i]= '('+expb + '/' + expa + ')';
				 number[i] = b / a;                        
				 Search(n-1);                         
			}                                
			number[i]  =  a;
			number[j]  =  b;
			ex[i]  = expa;
			ex[j]  = expb;
		}      
	} 
}          
 int main()   
 {        
	 cout<<"Please input 4 value of Cards:\n";  
	 for (int i = 0; i < c; i++)     
	{	
		char buffer[20];          
		cout<<"The "<<i+1<<"th card:";            
		cin>>number[i];                          
		itoa(number[i],buffer,10);
		ex[i]   =   buffer;                 
		cout<<endl; 
		Search(c);
	 }
	 if(j==true)
	 {                
		 cout<<"\nSuccess."<<endl;  
	 }      
	 else     
	 {             
		 cout<< "Fail."<<   endl;   
	 }               
	 return 0; 
}
