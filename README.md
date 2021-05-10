# Homework 2
###  Due until 17.05.2021., 12:30

This homework is divided into two parts. Part 1 is a very easy problem and you do not have to submit it. Its only purpose is that you can check for yourself how well you are doing with C++. Part 2 is a bit more tricky this week. You might need more time than for the homework problems before.

***
### Part 1
This problem is meant as a check for yourself. Solving it requires basic concepts we discussed in the lecture and used in the exercises so far. At this point you should have no major problems in solving it. Your level of C++ syntax skills should be sufficient to handle this problem without having to look up many things in older files or in the slides. This reflects the minimum C++ knowledge we expect you to have at this point.

*Problem 1*:
Generate a static array of *N* random numbers. Fill in the numbers within an extra function of your code, similar to the last homework. Write a second function which finds the maximum and the minimum number stored in that array. Use references to pass the minimum and the maximum back to the main function. Print the two values from inside the `main()` function.

***

### Part 2

Assume we have discrete signal values *f[i],i=0,...,N-1*, but unfortunately the signal is very noisy. We come up with the idea of how we might reduce the noise: We calculate g[i] = (f[i-1] + f[i] + f[i+1])/3 and thus replace every value by a local average.

In the file **noisy.txt** there is such a signal. Use gnuplot to have a look at it. Your task is to write a code that filters this signal. Files **to be submitted are the code** for the program **and one plot** which shows your filtered result versus the original unfiltered signal.

Write a program which reads the data from the file into an array, filters the data according to the procedure described above and then writes the results into a new file.

Structure your program well, in particular:
* Write a function which reads the data into an array.
  The current file has *N*=237 lines, allocate sufficient memory **inside**
  your reading function. This requires dynamic allocation.
  In order to read the data from the file, you will need to use `ifstream`
  objects. The work very similar to `ofstream` objects that you have already
  used. The following minimal working example shows how to use an `ifstream``
  to read data from a file.
  ```C++
  #include <fstream>

  using namespace std;

  int main(){
    ifstream input("noisy.txt");
    double a;
    input >> a;
    cout << a << endl;
  }
  ```
  The object *input* works similar to the stream *cin* which is mentioned
  in some lecture examples to read data from the keyboard, only that
  *input* reads data line by line from the file **noisy.txt**.
* The variable *N* that is used to set the number of lines to read
  from the file is already defined in the main program. Use this
  variable in all cases where you have to refer to the number of
  data points/number of lines in the data file.  
* Have one function which filters the data. Interpret the
  data as periodic function, i.e. f[N]=f[0]. Overwrite the original array
  and do not (!) create a second
  array.  Note that once your code works, you can apply the filter
  function more than once to the data. It is interesting to see what
  happens to the data when you apply the filter several times.
* Write the final result inside an extra function into a file, do not
  overwrite the original data file.
* Make sure that all memory that has been allocated via `new` has
  been freed by a respective `delete`.

Once you have filtered the data, use GNUplot to compare the filtered
data and the original signal. Assuming that the filtered signal is in
`filtered.txt`, you can plot both signals via
```
gnuplot> set st data line
gnuplot> plot "noisy.txt", "filtered.txt"
```
You can save gnuplot plots into a file by the following sequence of commands:
```
gnuplot> set term png
gnuplot> set out "plot.png"
gnuplot> plot "noisy.txt", "filtered.txt"
```
This creates a file plot.png which contains your plot. Note, that after you entered `set term png` nothing will be updated in your regular plot window. Everything is directly sent to the .png file.


Final note: We will compile your code using the `-pedantic` flag, that is `g++ filter.cxx -o filter -pedantic` to check that you are not using any compiler specific C++ extensions. Hence, you should use `-pedantic` as well during the development.
