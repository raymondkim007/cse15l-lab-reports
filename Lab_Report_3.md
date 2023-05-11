# Lab Report 3 - Researching Commands

This lab report will explore the `grep` command, and 4 command-line options for `grep` that would be useful for regular use. 

All command line options for grep were first initially discovered with the [Geeks for Geeks website](https://www.geeksforgeeks.org/grep-command-in-unixlinux/) and individually explored in the VS Code terminal. 

## Grep `-i`

The `-i` command for `grep` is an extremely useful command, as it ignores upper and lower cases when matching the text file lines to the given pattern. Let us demonstrate this below. 

By using the default `grep` without the `-i` option when searching for `"base pair"` in all text files for `technical/biomed`, we get returned with 226 lines. 

    raymo@Raymond_Kim MINGW64 ~/Documents/GitHub/docsearch (main)
    $ grep "base pair" technical/biomed/*.txt > biomed_basepair.txt

    raymo@Raymond_Kim MINGW64 ~/Documents/GitHub/docsearch (main)
    $ wc biomed_basepair.txt
      226  2326 22760 biomed_basepair.txt

However, by including the `-i` option, we receive 228 results, supposedly where the additional 2 results include upper case letters such as `"Base pair"`. 

    raymo@Raymond_Kim MINGW64 ~/Documents/GitHub/docsearch (main)
    $ grep -i "base pair" technical/biomed/*.txt > biomed_basepair_i.txt

    raymo@Raymond_Kim MINGW64 ~/Documents/GitHub/docsearch (main)
    $ wc biomed_basepair_i.txt
      228  2347 22965 biomed_basepair_i.txt

We can try a second example. Let us try searching for perhaps the most common sentence starter, `the`, for all files in `technical/plos`. This gives us 19109 results. 

    raymo@Raymond_Kim MINGW64 ~/Documents/GitHub/docsearch (main)
    $ grep "the" technical/plos/*.txt > plos_the.txt

    raymo@Raymond_Kim MINGW64 ~/Documents/GitHub/docsearch (main)
    $ wc plos_the.txt
      19109  271072 2485912 plos_the.txt

And by including the `-i` option, the result count increases to 20479, showing over a 1000 new results. 

    raymo@Raymond_Kim MINGW64 ~/Documents/GitHub/docsearch (main)
    $ grep -i "the" technical/plos/*.txt > plos_the_i.txt

    raymo@Raymond_Kim MINGW64 ~/Documents/GitHub/docsearch (main)
    $ wc plos_the_i.txt
      20479  289328 2659458 plos_the_i.txt

This is particularly useful command that we will be using further in our explorations below. 

## Grep `-l`

The `-l` option for `grep` only displays the filenmames that contain the pattern. This would be useful when dealing with file counts as `grep` normally returns every single matching instance of the pattern in each line, and manually searching for overlap or repeated files is feasibly impossible. 

We can observe this by using a similar example as above, grepping the string `"base pair"` for all text files within `technical/biomed`. As shown above (and below), `grep` normally returns 226 results. 

    raymo@Raymond_Kim MINGW64 ~/Documents/GitHub/docsearch (main)
    $ grep "base pair" technical/biomed/*.txt > biomed_basepair.txt

    raymo@Raymond_Kim MINGW64 ~/Documents/GitHub/docsearch (main)
    $ wc biomed_basepair.txt
      226  2326 22760 biomed_basepair.txt

However, the `-l` option returns 74 results instead, thus showing a lot of repeated file results in the original `grep`. 

    raymo@Raymond_Kim MINGW64 ~/Documents/GitHub/docsearch (main)
    $ grep -l "base pair" technical/biomed/*.txt > biomed_basepair_l.txt

    raymo@Raymond_Kim MINGW64 ~/Documents/GitHub/docsearch (main)
    $ wc biomed_basepair_l.txt
      74   74 2706 biomed_basepair_l.txt

This makes sense, as normally articles containing `"base pair"` would never only mention it once, instead delving deeply into a related field and thus contaning numerous instances of the pattern. 

Let us explore another example. As Charles Darwin was a prominent figure in evolutionary biology, let us pay tribute by grepping `"darwin"` for all files in `technical/biomed`. We have used the `-i` option to ignore upper and lower case divisons for simplicity. 

    raymo@Raymond_Kim MINGW64 ~/Documents/GitHub/docsearch (main)
    $ grep -i "darwin" technical/biomed/*.txt > biomed_darwin.txt

    raymo@Raymond_Kim MINGW64 ~/Documents/GitHub/docsearch (main)
    $ wc biomed_darwin.txt
      10   89 1023 biomed_darwin.txt
      
This gives us 10 lines, thus 10 instances of `"darwin"`. Let us include `-l` in the command line.

    raymo@Raymond_Kim MINGW64 ~/Documents/GitHub/docsearch (main)
    $ grep -li "darwin" technical/biomed/*.txt > biomed_darwin_l.txt

    raymo@Raymond_Kim MINGW64 ~/Documents/GitHub/docsearch (main)
    $ wc biomed_darwin_l.txt
      3   3 118 biomed_darwin_l.txt

This gives us 3 results, thus showing us that 3 of the texts in `technical/biomed` are about, or include mentions of, Charles Darwin. Admittedly, `-l` is not particularly useful in this case as we are only dealing with small file counts. However, for larger file counts, this will prove particularly useful.

## Grep `-c`

The `-c` option prints out a count of all lines that match a pattern, instead of printing all lines individually. However, it should be noted that it also prints out all counts of 0.

Let us try grepping `inherit` for all files in `technical/biomed`. Here, `-i` is used for convenience. 

    raymo@Raymond_Kim MINGW64 ~/Documents/GitHub/docsearch (main)
    $ grep -li "inherit" technical/biomed/*.txt > biomed_inherit.txt

    raymo@Raymond_Kim MINGW64 ~/Documents/GitHub/docsearch (main)
    $ wc biomed_inherit.txt
      60   60 2232 biomed_inherit.txt

We see that 60 files in `technical/biomed` have to do with inheritance. Let us attempt to include `-c`.

    raymo@Raymond_Kim MINGW64 ~/Documents/GitHub/docsearch (main)
    $ grep -ci "inherit" technical/biomed/*.txt
    technical/biomed/1468-6708-3-1.txt:0
    technical/biomed/1468-6708-3-10.txt:0
    technical/biomed/1468-6708-3-3.txt:0
    
Only the first few lines are displayed, but we see that the majority of the 800+ files in `technical/biomed` will be included in the output, all with count 0. Thus, this might be seen as occasionally useful for skimming purposes. 

Let us try another example similar to before, using `"base pair"`. Again, the normal `grep` returns 228 results. 

    raymo@Raymond_Kim MINGW64 ~/Documents/GitHub/docsearch (main)
    $ grep -i "base pair" technical/biomed/*.txt > biomed_basepair.txt

    raymo@Raymond_Kim MINGW64 ~/Documents/GitHub/docsearch (main)
    $ wc biomed_basepair.txt
      228  2347 22965 biomed_basepair.txt
      
And the `-c` option looks as follows. Again, only the first few output lines are included. 

    raymo@Raymond_Kim MINGW64 ~/Documents/GitHub/docsearch (main)
    $ grep -ci "base pair" technical/biomed/*.txt
    technical/biomed/1468-6708-3-1.txt:0
    technical/biomed/1468-6708-3-10.txt:0
    technical/biomed/1468-6708-3-3.txt:0

## Grep `-v`

The `-v` option returns all non instances of the given pattern within a file. This could be useful for exclusion purposes, although it might require a bit of fiddling to use. This is because directly using `-v` for all files will surely return a positive result for every single file, as every file probably contains at least one line that doesn't contain the pattern. 

Let us try with the same example of `"base pair"`. However, as grepping `-v` for all files is chaos, let us focus on a specific text file, 1471-2105-3-2.txt, located in `technical/biomed`. 

    raymo@Raymond_Kim MINGW64 ~/Documents/GitHub/docsearch (main)
    $ grep -i "base pair" technical/biomed/1471-2105-3-2.txt > biomed_basepair_spec.txt

    raymo@Raymond_Kim MINGW64 ~/Documents/GitHub/docsearch (main)
    $ wc biomed_basepair_spec.txt
      87  789 5694 biomed_basepair_spec.txt
      
As shown, the text file contians 87 lines containing the pattern `"base pair"`. 

    raymo@Raymond_Kim MINGW64 ~/Documents/GitHub/docsearch (main)
    $ grep -vi "base pair" technical/biomed/1471-2105-3-2.txt > biomed_basepair_spec_n.txt

    raymo@Raymond_Kim MINGW64 ~/Documents/GitHub/docsearch (main)
    $ wc biomed_basepair_spec_n.txt
    2272  16619 133089 biomed_basepair_spec_n.txt
  
And the file contains 2272 lines that don't contain the pattern `"base pair"`. 

Let us try one last example using the same file, but instead grepping for `"the"`. 

    raymo@Raymond_Kim MINGW64 ~/Documents/GitHub/docsearch (main)
    $ grep -i "the" technical/biomed/1471-2105-3-2.txt > biomed_the_spec.txt

    raymo@Raymond_Kim MINGW64 ~/Documents/GitHub/docsearch (main)
    $ wc biomed_the_spec.txt
     1303 11044 83384 biomed_the_spec.txt
 
The file contains 1303 lines with the word `"the"`. Let us include `-v` in the command line. 

    raymo@Raymond_Kim MINGW64 ~/Documents/GitHub/docsearch (main)
    $ grep -vi "the" technical/biomed/1471-2105-3-2.txt > biomed_the_spec_n.txt

    raymo@Raymond_Kim MINGW64 ~/Documents/GitHub/docsearch (main)
    $ wc biomed_the_spec_n.txt
     1056  6364 55399 biomed_the_spec_n.txt
 
And surpisingly, the file contains 1056 lines that do not contain the word `"the"`. This is explained more when looking at the first few lines of the file. 

    raymo@Raymond_Kim MINGW64 ~/Documents/GitHub/docsearch (main)
    $ head technical/biomed/1471-2105-3-2.txt
    
            Background
            In the 1830's, Charles Darwin's investigation of the
            Galapagos finches led to an appreciation of the structural
            characteristics that varied and were conserved among the
            birds in this landmark comparative study. His analysis of
            the finches' structural features was the foundation for his

As evident, each line is very short, and contains strongly academic language that does not overuse the term `"the"`. 
