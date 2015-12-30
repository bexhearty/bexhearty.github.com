#ASCII and Unicode
Using a program to order lists that contain both letters and numbers will often times yield unexpected results. For instance, when ordering a list of flights in ascending order, the results are most likely to resemble the following list:

| Flight |
|:------|
| UA1006 |
| UA1008 |
| UA1009 |
| UA289 |
| UA327 |
| UA3444 |
| UA5445 |
| UA570 |

That is because most text editors serve as binary-to-symbol translators. In this case, the document you are reading was typed on a text editor and was stored in a server as a set of ASCII, Unicode or some type of binary file containing a bunch of 1s and 0s. 

######What are ASCII Values?
ASCII stands for American Standard Code for Information Interchange and is a binary file format that assigns a 7-bit binary value (a string of seven 0s and 1s) to alphanumeric, numeric and some special characters -- most keys on the standard keyboard.

ASCII code rose from a system used in telegraphy and it first included only numbers and capital letters. In 1967 lower case letters were included as well as some additional characters for a total of 128 characters. In ASCII, numbers are assigned smaller values than capital letters, and capital letters are assigned a smaller value than lower case letters. ASCII define the sets of numbers **0** to **9**, letters **A** to **Z**, and letters **a** to **z** in ascending numeric value.

In the above example, the flight data is sorted based on ASCII values (UA5445 is a smaller value than UA570 because 4 precedes 7). This type of sorting is efficient for machines and produces reasonable results for the English alphabet. Since its American centric (after al, the A stands for American) ASCII presents issues for Asian languages and those languages such as french, portuguese or spanish, that contain characters outside of the English alphabet.

######Unicode
Unicode is a newer standard for character sets, which is becoming more popular. Rather than using only 7-bits, Unicode is based in 16-bit binary values which allows more than 65,000 character representations (as opposed to ASCII's 128 character limit), and includes characters from most popular languages. Unicode preserved the order of the first 128 ASCII characters. 

Although many languages are still based on ASCII (Python, R, C and C++), Unicode is now becoming the norm (Javascript uses Unicode).