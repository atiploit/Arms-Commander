FIXED: Selecting Option #5 "Inter-Cat", gives a incorrectly ordered user input prompt. "Enter the FULL PATH to your PASSWORD DICTIONARY FILE: "

FIXED: Hybrid and Reverse-Hybrid Attacks

FIXED: Combinator Attacks. I confused the switch for Brute Force with Combinator. Combinator = 1, Brute Force (Mask) = 3

**BUGGED: "Mask-Attack" or "Brute-Force" syntax is bugged. Reading the manual on hashcat right now**

Source: https://hashcat.net/wiki/doku.php?id=mask_attack

Okay... so they use a lot of fancy terms to describe something simple, for example "optparse" but for hashcat to properly use a character set you can either use "-1" or full length wise... "--custom-charset1=CS"

And....

"-1 charsets/special/Russian/ru_ISO-8859-5-special.hcchr"

Just means

"--custom-charset1=CS charsets/special/Russian/ru_ISO-8859-5-special.hcchr"

Which is located in this folder: /usr/share/hashcat/charsets/

So I am guessing this is how its supposed to be done

"hashcat -a 3 <charset switch> <charset hcchr file> <password length>"

so if you type '?l' 5-times for password length, it means the password is five-letters long, and letters ONLY. To include numbers its 

"hashcat -a 3 <charset switch> <charset hcchr file> <number switch> <password length>"

Where number switch = '?l?d'

But you see, WPA2-PSK by itself, requires the user to have EIGHT characters at a minimum. So we should start the menu at that. However, I am not gonna just number that to the maximum bits. I'd rather have the user input it themselves.

Yeesh that is one ugly documentation. But okay one way that works is..

"hashcat -a 3 <hashfile> <pw length>" 

which is letters ONLY. To include numbers its...

"hashcat -a 3 <hashfile> <include numbers> <pw length>"

So its

"hashcat -a 3 <hashfile> ?l?d ?l?l?l?l?l?l"

for a six-letter password with words and numbers

You can also specify a "mask". And you can find your preloaded mask files with "locate masks" in terminal

"hashcat -a 3 <hash to attack> <mask_file.hcmask>"


What worked?

This command worked, which specified a six digit password of both letters and numbers:

"hashcat -a3 -m 2500 /media/root/Data/HashCatConverted/hashcat_20170405-013557.cap-01.cap.hccapx ?l?d ?l?l?l?l?l?l"

I should use the mask file method as a separate method. 