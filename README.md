<div align="center">

## Array Fun


</div>

### Description

All kinds of stuff to an array, including: Read file; print array; print stats (average, range, mode, median); add to the file (multiple nums); delete from file (one num); sorting (bubble sort / replacement sort / insertion sort / quick sort); find a number using binary search

*** Please rate this code and include any suggestions ***
 
### More Info
 
a text file, ARRAY.TXT, of numbers

uses apvector.h for array, but still a good overall example off all kinds of stuff relating to arrays and algorithms

1. Read file

2. Print array (15 on a row)

3. Print stats (average, range, mode, median)

4. Add to the file (multiple nums)

5. Delete from the file (only one)

6. Order the file.(ascending)

a.bubble sort

b.replacement sort

c.insertion sort

d.quick sort

7.find a number using the binary search


<span>             |<span>
---                |---
**Submitted On**   |
**By**             |[eddy neon](https://github.com/Planet-Source-Code/PSCIndex/blob/master/ByAuthor/eddy-neon.md)
**Level**          |Beginner
**User Rating**    |5.0 (35 globes from 7 users)
**Compatibility**  |C, C\+\+ \(general\), Microsoft Visual C\+\+
**Category**       |[Miscellaneous](https://github.com/Planet-Source-Code/PSCIndex/blob/master/ByCategory/miscellaneous__3-1.md)
**World**          |[C / C\+\+](https://github.com/Planet-Source-Code/PSCIndex/blob/master/ByWorld/c-c.md)
**Archive File**   |[](https://github.com/Planet-Source-Code/eddy-neon-array-fun__3-2871/archive/master.zip)

### API Declarations

```
#include <iostream.h>
#include <fstream.h>
#include "apvector.h"
```


### Source Code

```
//Complex Array Program
// by "eddy neon"
/*
1.~Read file
2.~Print array(15 on a row)
3.~Print stats(~average, ~range, ~mode, ~median)
4.~Add to the file.(ask how many and add that many)
5.~Delete from the file.(only one)
6. Order the file.(ascending)
 ~a.bubble sort
 ~b.replacement
 ~c.insertion
 ~d.quick
7.~find a number using the binary search(this can be used by several of the above functions)
*/
#include<iostream.h>
#include<fstream.h>
#include "apvector.h"
// ******* MENU *******
int menu()
{
	int choice;
	cout<<endl;
	cout<<"Your choices are...\n"
		<<" [1] Read the base file into the array.\n"
		<<" [2] Print the array in rows of 15.\n"
		<<" [3] Print the array's average, range, median, and mode.\n"
		<<" [4] Add number(s) to the array.\n"
		<<" [5] Delete a number from the array.\n"
		<<" [6] Sort the array into ascending order.\n"
		<<" [7] Find a number in the array.\n"
		<<" [8] Exit the program.\n";
	cout<<"Please select a numeric choice from the menu: ";
	cin>>choice;
	return choice;
}
// ***** MENU CHOICE 1: "Read file"
apvector<int> readFile(int &last, bool &inOrder)
{
	apvector<int> data_array(400, 9999999);
	int i;
	ifstream data_file;
	data_file.open("ARRAY.TXT");
	i=0;
	while (!data_file.eof())
	{
		data_file>>data_array[i];
		i++;
	};
	last=i-1;
	data_file.close();
	inOrder=false;
	return data_array;
}
// ***** MENU CHOICE 2: "Print array(15 on a row)"
void printArrayRows15(const apvector<int> &array, int numCt)
{
	int index;
	for(index=0;index<numCt;index++)
	{
		cout.width(4);
		cout<<array[index]<<" ";
 if(((index+1)%15)==0)
			cout<<endl;
	}
	cout<<endl<<endl;
}
// ***** THE ARRAY ORGANIZING FUNCTIONS *****
// @@@ MENU CHOICE 6a: bubble sort
void bubbleSort(apvector<int> &array, int numCt, bool &sorted)
{
	int index=0, j, temp;
	for(index=0; index<numCt, !sorted; index++)
	{
		sorted=true;
		for(j=0; j<numCt-index-1; j++)
		{
			if(array[j]>array[j+1])
			{
				temp=array[j+1];
				array[j+1]=array[j];
				array[j]=temp;
				sorted=false;
			}
		}
	}
}
// @@@ MENU CHOICE 6b: replacement sort
void replacementSort(apvector<int> &array, int numCt, bool &sorted)
{
	int index, small, smlIndex, newIndex;
	apvector<int> newArray(400);
	for(newIndex=0; newIndex<=numCt; newIndex++)
	{
		small=99999;
		for(index=0; index<numCt; index++)
		{
			if(array[index]<small)
			{
				small=array[index];
				smlIndex=index;
			}
		}
		newArray[newIndex]=small;
		array[smlIndex]=9999999;
	}
	array=newArray;
	sorted=true;
}
// @@@ MENU CHOICE 6c: insertion sort
void insertionSort(apvector<int> &array, int numCt, bool &sorted)
{
	int index, orig, temp;
	for(index=1; index<numCt; index++)
	{
		orig=array[index];
		temp=index;
		while(array[temp-1]>orig)
		{
			array[temp]=array[temp-1];
			temp--;
			if(temp<=0)
				break;
		}
		array[temp]=orig;
	}
	sorted=true;
}
// @@@ MENU CHOICE 6d: quick sort
int partition(apvector<int> &array, int low, int high)
{
	int pivot, left, right, temp;
	pivot=array[low];
	left=low;
	right=high;
	while(left<right)
	{
		while(array[left]<=pivot && left<high)
		{
			left++;
		}
		while(array[right]>=pivot && right>low)
		{
			right--;
		}
		if(left<right)
		{
			temp=array[left];
			array[left]=array[right];
			array[right]=temp;
		}
	}
	temp=array[low];
	array[low]=array[right];
	array[right]=temp;
	return right;
}
void qSort(apvector<int> &array, int low, int high)
{
	if(high>low)
	{
		int pivot;
		pivot=partition(array, low, high);
		qSort(array, low, pivot-1);
		qSort(array, pivot+1, high);
	}
}
void quickSort(apvector<int> &array, int numCt, bool &sorted)
{
	qSort(array, 0, numCt-1);
	sorted=true;
}
// @@@ BINARY SEARCH
int binarySearch(apvector<int> &array, int numCt, int target, bool &inOrder, bool &found)
{
	found=false;
	int low=0, high=numCt-1, mid=high/2;
	if(!inOrder)
		quickSort(array, numCt, inOrder);
	while(high>=low)
	{
		if(target==array[mid])
		{
			found=true;
			return mid;
		}
		if(target>array[mid])
			low=mid+1;
		if(target<array[mid])
			high=mid-1;
		mid=(high+low)/2;
	}
	int index;
	for(index=high+5; index>=0; index--)
	{
		if(array[index]<target)
			return index+1;
	}
	return 0;
}
// ***** MENU CHOICE 3: Print stats(average, range, mode)
double calcAverage(const apvector<int> &array, int numCt)
{
	int runTtl=0, index;
	double avg;
	for(index=0; index<=numCt-1; index++)
		runTtl+=array[index];
	avg=double(runTtl)/numCt;
	return avg;
}
void getRange(apvector<int> &array, int numCt, int &max, int &min, bool &inOrder)
{
	if(!inOrder)
		quickSort(array, numCt, inOrder);
	max=array[numCt-1];
	min=array[0];
}
double getMedian(apvector<int> &array, int numCt, bool &inOrder)
{
	int medianIndex;
	double median;
	if(!inOrder)
		quickSort(array, numCt, inOrder);
	medianIndex=numCt/2;
	if(numCt%2==0)
		median=double(array[medianIndex]+array[medianIndex-1])/2;
	else
		median=array[medianIndex];
	return median;
}
void getPrintMode(apvector<int> &array, int numCt, bool &inOrder)
{
	int index, count=0, max;
	for(index=0; index<numCt; index++)
	{
		if(array[index]==array[index+1])
			count++;
		else
		{
			if(count>max)
				max=count;
			count=0;
		}
	}
	count=0;
	for(index=0; index<numCt; index++)
	{
		if(array[index]==array[index+1])
			count++;
		else
		{
			if(count==max)
				cout<<"One mode, which occured "<<count+1<<" times, is "<<array[index]<<".\n";
			count=0;
		}
	}
}
void printStats(apvector<int> &array, int arrCt, bool &inOrder)
{
	int big, sml;
	double avg, median;
	cout<<endl<<endl;
	avg=calcAverage(array, arrCt);
	getRange(array,arrCt,big, sml, inOrder);
	median=getMedian(array, arrCt, inOrder);
	getPrintMode(array, arrCt, inOrder);
	cout<<"The average is "<<avg<<".\n"
		<<"The range is "<<big-sml<<", from "<<sml<<" to "<<big<<".\n"
		<<"The median is "<<median<<".\n\n";
}
// ***** MENU CHOICE 4: Add to the file.(ask how many and add that many)
void addNums(apvector<int> &array, int &numCt, bool &inOrder)
{
	int numNewNums, newNumCt, addNum, index, addNumLoc;
	bool addNumFound;
	cout<<"\nHow many numbers do you wish to add to the array? ";
	cin>>numNewNums;
	if(numNewNums+numCt+100>=array.length())
		array.resize(numCt+numNewNums+100);
	for(newNumCt=numCt; newNumCt<numCt+numNewNums; newNumCt++)
	{
		cout<<" What number do you wish to add to the array? ";
		cin>>addNum;
		addNumLoc=binarySearch(array, numCt, addNum, inOrder, addNumFound);
		for(index=newNumCt; index>addNumLoc; index--)
			array[index]=array[index-1];
		array[addNumLoc]=addNum;
	}
	numCt=newNumCt;
}
// ***** MENU CHOICE 5: Delete a number from the array
void deleteNum(apvector <int> &array, int &numCt, bool &inOrder)
{
	int deleteTarget, targtLoc, index;
	bool targFound;
	cout<<"\nWhat number do you wish to remove from the array? ";
	cin>>deleteTarget;
	cout<<endl;
	targtLoc=binarySearch(array, numCt, deleteTarget, inOrder, targFound);
	if(!targFound)
		cout<<"The number "<<deleteTarget<<" was not found in the array. \n\n";
	else
	{
		for(index=targtLoc; index<=numCt-2; index++)
			array[index]=array[index+1];
		array[numCt-1]=9999999;
		numCt--;
		cout<<"The number "<<deleteTarget<<" at index "<<targtLoc<<" was deleted from the array.\n\n";
	}
}
// ***** MENU CHOICE 6: Order the file (bubble / replacement / insertion / quick sort)
char sortingMenu()
{
	char choice;
	cout<<endl;
	cout<<"The types of sorts are...\n"
		<<" a. Bubble Sort\n"
		<<" b. Replacement Sort\n"
		<<" c. Insertion Sort\n"
		<<" d. Quick Sort\n";
	cout<<"What type of sort do you wish to perform? ";
	cin>>choice;
	return choice;
}
void sortSelect(char choice, apvector<int> &array, int numCt, bool &inOrder)
{
	switch(choice)
	{
		case 'a':
			bubbleSort(array, numCt, inOrder);
			cout<<endl<<" Bubble sort complete.\n";
			break;
		case 'b':
			replacementSort(array, numCt, inOrder);
			cout<<endl<<" Replacement sort complete.\n";
			break;
		case 'c':
			insertionSort(array, numCt, inOrder);
			cout<<endl<<" Insertion sort complete.\n";
			break;
		case 'd':
			quickSort(array, numCt, inOrder);
			cout<<endl<<" Quick sort complete.\n";
			break;
		default:
			cout<<" **** Not one of the choices: make sure it is lower-case a,b,c, or d!!! **** \n\n";
			break;
	}
}
// ***** MENU CHOICE 7: FIND A NUMBER IN THE ARRAY
void findandPrintNum(apvector<int> &array, int numCt, bool &inOrder)
{
	int trgt, targIndex;
	bool trgtFound;
	cout<<"\nWhat number do you wish to find in this array? ";
	cin>>trgt;
	cout<<endl;
	targIndex=binarySearch(array, numCt, trgt, inOrder, trgtFound);
	if(!trgtFound)
		cout<<"The number "<<trgt<<" was not found in this array, but should be\n"
			<<" located at index "<<targIndex<<" (position "<<targIndex+1<<") in the sorted array.\n\n";
	else
		cout<<"The number "<<trgt<<" was first found at index "<<targIndex<<" (position "<<targIndex+1<<") in the array.\n\n";
}
// ~~~~~ %%%%% MAIN %%%%% ~~~~~
void main()
{
	int arrayCt;
	bool inOrder, menuContinue=true;
	apvector<int> array(400);
	array=readFile(arrayCt, inOrder);
	while(menuContinue)
	{
		int menuChoice;
		menuChoice=menu();		//gets choice number of operation to perform from main menu
		switch(menuChoice)
		{
			case 1:			// Read the base file into the array
				array=readFile(arrayCt, inOrder);
				cout<<endl<<"The original text file has been read into the array"<<endl;
				break;
			case 2:			// Print the array in rows of 15
				printArrayRows15(array, arrayCt);
				break;
			case 3:			// Print the array's average, range, and mode
				printStats(array, arrayCt, inOrder);
				break;
			case 4:			// Add number(s) to the array
				addNums(array, arrayCt, inOrder);
				break;
			case 5:			// Delete a number from the array
				deleteNum(array, arrayCt, inOrder);
				break;
			case 6:			// Sort the array into ascending order
				char sortMenuChoice;
				sortMenuChoice=sortingMenu();
				sortSelect(sortMenuChoice, array, arrayCt, inOrder);
				break;
			case 7:			// Find a number in the array
				findandPrintNum(array, arrayCt, inOrder);
				break;
			case 8:
				menuContinue=false;
				break;
			default:
				break;
		}
		cout<<endl;
	}
}
```

