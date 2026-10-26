# Corner Grocer Item Tracker (CS 210 Project Three)

Shane De La Rosa, SNHU CS 210 Programming Languages

## Summarize the project and what problem it was solving.

Corner Grocer wanted a better way to see which produce items people were buying throughout the day so they could rearrange the store around it. They had a text file that logged every item purchased, one per line, but no easy way to make sense of it. I wrote a C++ program that reads that file, counts how many times each item shows up, and gives the user a menu with four options. You can look up how many times one item was bought, print the count for every item, print a text histogram using asterisks, or exit. The program also saves a backup of all the counts to a file called frequency.dat as soon as it starts, without the user having to do anything.

## What did you do particularly well?

I think the structure is the strongest part. All the tracking logic lives in a GroceryTracker class with a header file and an implementation file, and main.cpp only handles the menu. The item counts are stored in a std::map as a private member, which keeps everything sorted alphabetically for display and made counting really simple. I also put a lot of work into input validation. The menu reads the whole line and only accepts a number from 1 to 4, so typing something like "hello" or "2abc" just asks again instead of breaking the program. Item lookups ignore upper and lower case, so searching "onions" still finds "Onions."

## Where could you enhance your code? How would these improvements make your code more efficient, secure, and so on?

Right now the case insensitive search loops through every item in the map to compare them, which is fine for a small grocery list but doesn't scale. I could store a lowercase version of each name as the key (or keep a second map) so lookups use the map's built in search and stay fast even with thousands of items. The file names are also hard coded, so letting the user pass them in would make it easier to reuse with other data. On the security side, I could cap the length of user input and check the input file for weird or unexpected content before trusting it. If an item was bought hundreds of times, the histogram would get unreadable, so scaling the bars would help too. Adding some automated tests for the counting and lookup functions would make it safer to change things later.

## Which pieces of the code did you find most challenging to write, and how did you overcome this? What tools or resources are you adding to your support network?

The input validation was the trickiest part. Using plain cin for the menu breaks the moment someone types a letter, so I switched to reading the full line with getline and converting it with stoi inside a try and catch, then checking that nothing extra was typed after the number. Another sneaky issue was Windows line endings leaving a hidden \r at the end of each item, which made "Peas" and "Peas\r" count as different things. Writing a Trim helper fixed that. Honestly, a lot of the struggle was Visual Studio itself, like adding existing files to the project through Solution Explorer, making sure the input file was in the right folder, and remembering to include the solution file when zipping the project. Going forward my support network includes zyBooks, the Visual Studio debugger, cppreference.com for looking up how standard library functions behave, GitHub for keeping my work organized, and AI tools for walking through error messages when I get stuck.

## What skills from this project will be particularly transferable to other projects or course work?

Splitting a program into a class with a clear header and implementation is something I'll use in pretty much every language going forward. Reading from and writing to files, picking the right data structure for the job (a map was perfect for counting), and validating user input are all things that come up constantly, especially in my cybersecurity concentration where never trusting user input is a big deal. Getting comfortable with Visual Studio and GitHub will also help in every programming class after this.

## How did you make this program maintainable, readable, and adaptable?

I used clear names for everything, like GetItemFrequency, PrintHistogram, and WriteBackupFile, so you can tell what a function does without reading it. The menu options and file names are stored as named constants at the top of main.cpp instead of random numbers and strings scattered around, so changing one only takes a single edit. Every function has a comment explaining what it does, and the trickier lines have comments explaining why. Keeping the data and logic inside the GroceryTracker class means someone could swap out the menu or add a new feature without touching how the counting works. Even the histogram symbol is a parameter, so it can be changed without rewriting the function.
