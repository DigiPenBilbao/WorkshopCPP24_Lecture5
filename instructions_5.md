# Introduction
This lesson will focus on arrays. Arrays was used in previous exercises, but this time we are going to focus on exercises centered in arrays.

An array is a collection of elements of the same data type that can be stored and handled using the identifier of the array and the index of the element in the coleection.

Arrays are very usefull when a certain number of variables of the same time must be handled, otherwise, a great number of different variables would be needed.

## Exercise: Array of integers
This exercise will allow the user to introduce multiple numbers (integers) into an array. After that the program will show all the numbers introduced in the same line.

```c++
#include <iostream>

int main() {
  int array[10];
  int size = 10;

  for (int i = 0; i < size; i++)
  {
    std::cout << "Introduce a number: \n";
    std::cin >> array[i]; //introduce the number at position i of the array
  }

  std::cout << "\n The array introduced is: ";
  for (int i = 0; i < size; i++)
  {
    std::cout << array[i] << " ";
  }  
}
```
This program will ask the user for 10 numbers and then will show the 10 numbers in the same line.

## Exercise: Find max number in an array
There are several operations that can be done with arrays, one of the most common is finding the max value in an array. As it has been done before, using a function to do that operation is the best solution.
```c++
int array_max (int array[], int size)
{
  int max = array[0];
  for (int i = 1; i < size; i++)
  {
    if (max < array[i])
    {
      max = array[i];
    }
  }
  return max;
}
```
Implementing a function that calculate the minium number in an array is quite similar to this one.
```c++
int array_min (int array[], int size)
{
  int min = array[0];
  for (int i = 1; i < size; i++)
  {
    if (min > array[i])
    {
      min = array[i];
    }
  }
  return min;
}
```

## Exercise: Calculate some statistics 
Having multiple numbers in an array provide us a good oportunity to calculate some statistics, what about the sum of all the numbers? what about the average? Lets see it.
```c++
int array_sum(int array[], int size)
{
  int sum = 0;
  for (int i = 0; i < size; i++)
    {
      sum = sum + array[i];
    }
  return sum;
}

float array_avg(int array[], int size)
{
  return array_sum(array, size) / size;
}
```
Same way we can calculate the average deviation.
```c++
float array_avgDev(int array[], int size)
{
  float avg = array_avg(array, size);
  float sum_dev = 0;
  for (int i = 0; i < size; i++)
    {
      if (array[i] > avg)
        sum_dev = sum_dev + (array[i] - avg);
      else
        sum_dev = sum_dev + (avg - array[i]);
    }
  return sum_dev/size;
}
```
Now given the array of numbers, we can calculate all these statistics concepts just calling these functions.
```c++
int main() {
  int array[10];
  int size = 10;

  for (int i = 0; i < size; i++)
  {
    std::cout << "Introduce a number: \n";
    std::cin >> array[i]; //introduce the number at position i of the array
  }

  std::cout << "\n The array introduced is: ";
  for (int i = 0; i < size; i++)
  {
    std::cout << array[i] << " ";
  }  

  std::cout << "\nMax number in array is: " << array_max(array, size);
  std::cout << "\nMin number in array is: " << array_min(array, size);
  std::cout << "\nThe sum of all the numbers: " << array_sum(array, size);
  std::cout << "\nThe avg of all the numbers: " << array_avg(array, size);
  std::cout << "\nThe avg deviationof all the numbers: " << array_avgDev(array, size);
}
```

## Exercise: Reverse array
Another common exercise is to reverse an array, so the first element will be at the finish and viceverse. To do that it is necessary to access at the same time the first and last element, use a temporary variable to swap the values and repeat this until we arrive the medium point of the array.

```c++
void reverse_array(int array[], int size)
{
  for (int i = 0; i < size/2; i++)
    {
      int temp = array[i];
      array[i] = array[size - 1 - i];
      array[size - 1 - i] = temp;
    }
}
```

## Exercise: sort array
Other common exercise to do with arrays is sorting. The purpose of sorting is to put all the elements of the array in order. There are several ways to do this, but the simplest one is the algorithm called ```Bubble Sort```. 

This algorithm order the elements in pairs of 2 contiguous elements, starting from the begining and moving to the end. During the first iteration through the array the last element will be the largest one, so it will be in its final position. Repeating the process for the rest of the array (leaving the last element) will put the second largest element in its position. Just repeating the process until we have all the elements in their position will make the array to be sorted.

Lets see how to do it step by step:
1. Check if first value is greater than second, if so, swap the values
```c++
if (array[0] > array[1])
{
  int temp = array[0];
  array[0] = array[1];
  array[1] = temp;
}
```
2. After making this check, and swap, we have to check elements 1 and 2, then 2 and 3, and so until the end of the array. a For loop is suitable for this purpose. Notice that it need to finish one position before the end, as at this point the one before the last and the last will be checked.
```c++
    for (int i = 0; i < size - 1; i++)
    {
      // Bubble check, if first element is largest than second swap them
      if (array[i] > array[i+1])
      {
        int temp = array[i];
        array[i] = array[i+1];
        array[i+1] = temp;
      }
    }
```
3. Repeat the process again. Second time must reach to size -2. Third time must reach to size - 3, and so. It is needed a second for loop.
```c++
void bubble_sort(int array[], int size)
{
  // Repeat the process until all the array is sorted
  for (int j = size -1; j > 0; j--)
  {
    // One trave through the aray to put the largest element at the end
    for (int i = 0; i < j; i++)
    {
      // Bubble check, if first element is largest than second swap them
      if (array[i] > array[i+1])
      {
        int temp = array[i];
        array[i] = array[i+1];
        array[i+1] = temp;
      }
    }
  }
}
```

# Strings
A string is a special type of array. It is an array of characters that ends in a 0 value character. A string was already used to store the name in previous lectures. First of all, to use a "string" it is necessary to declare a variable as an array of characters.

```c++
int main()
{
  char my_string[10];
}
```
It is important to create the array of characters with the correct size. In the sample above, the array of character has a size of 10. it means que can store a macium of 9 characters, the last one is used to put a 0, so it means the end of the string.

```c++
int main()
{
  char my_string[10] = "Hello";
}
```
It is posible to initialize the string using double quotes and input a string of characters. The advantage of strings is that they con be put into the screen just as the other variables.
```c++
int main()
{
  char my_string[10] = "Hello";
  std::cout << my_string;
}
```
Lets try some function that uses strings as arguments. To use them it is necessary to include the library ```<string.h>``` in the program
```c++
#include <iostream>
#include <string.h>

int main()
{
  char my_string[10] = "Hello";
  std::cout << my_string << "\n";
  std::cout << "The string is " << strlen(my_string) << " characters length.";
}
```
It is possible to check how the ouptut is different as the string is changed.

Lets try the function to copy strings
```c++
int main()
{
  char my_string_1[10] = "Hello!";
  char my_string_2[10];
  strcpy(my_string_2, my_string_1); 
  std::cout << my_string_2 << "\n";
  std::cout << "The string is " << strlen(my_string_2) << " characters length.";
}
```
The string displayed is ```my_string_2```, but information is at ```my_string_1```. To copy the contento of one string to another it is necesary to use this function.

Lets try the concat function.
```c++
int main()
{
  char my_string_1[10] = "Hello";
  char my_string_2[10] = " World!";
  char my_string_3[20];
  strcpy(my_string_3, my_string_1); 
  strcat(my_string_3, my_string_2);
  std::cout << my_string_3 << "\n";
  std::cout << "The string is " << strlen(my_string_3) << " characters length.";
}
```
To concat 2 strings it is important that the final string has enough space for the whole string.

## Exercise: Palindrome checker
Check if a string is a palindorme is a good exercise to manipulate a string as an array. A Plaindrome is a word that  reads the same backwards as forwards. To check if a word is a palindrome it is necessary to check if first character is the same as the last one, then the second is the same as the previous to the last one, and so, until we reach the medium of the word. It is similar to the previous exercise Reverse array.
```c++
bool palindrome_checker(char word[])
{
  int size = strlen(word);

  for (int i = 0; i < size/2; i++)
    {
      if (word[i] != word[size-1-i])
      {
        return false;
      }
    }
  return true;
}
```
  