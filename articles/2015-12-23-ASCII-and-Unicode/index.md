#ASCII and Unicode
Using a program to order lists that contain both letters and numbers will often times yield unexpected results. 

For instance, when using a program to order a list of flights in ascending order, the results are most likely to resemble the following:

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

Notice how flight 289 is ordered after flight 1009, and flight 570 is ordered after flight 5445. Most text editors serve as binary-to-symbol translators. In this case, the above table was typed on a text editor and was stored in some location as a set of ASCII, Unicode or some other type of binary values.  

######What are ASCII Values?
ASCII stands for American Standard Code for Information Interchange. ASCII is a binary file format that assigns a 7-bit binary value (a string of seven 0s and 1s) to alphanumeric, numeric and some special characters -- most keys on the standard keyboard.

ASCII code was first introduced in the early 1960's and was based on a system used in telegraphy. In ASCII, numbers **0** to **9** are assigned smaller values than upper case letters **A** to **Z**, and upper case letters are assigned smaller values than lower case letters **a** to **z**.

In the above example, the flight data is sorted based on ASCII values (UA5445 preceds UA570 because 4 precedes 7). This type of sorting is efficient for machines and produces reasonable results when using the English alphabet. However, since ASCII is American centric it presents limitations for Asian languages and other languages that contain characters outside of the English alphabet.

######Unicode
Unicode is a newer (1987) standard for representing characters. It also stores characters in binary form, but rather than using only 7-bits, Unicode is based in 16-bit binary values which allows more than 1,000,000 possible character representations (as opposed to ASCII's 128 character limit). Currently, Unicode includes characters from most popular languages and preserved the order of the first 128 ASCII characters. Although many languages are still based on ASCII (Python, R, C and C++), Unicode has been implemented in many recent technologies such as XML, Java and Javascript.