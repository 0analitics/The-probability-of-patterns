# The-probability-of-patterns-for-apple-stock

## Introduction
Using time series analysis, the project examines the probability of an increase or decrease in share prices for a selected company. The following example uses the getSymbols () function from the quantmod package, which pulled the Apple time series (ticker AAPL) and saved it as a tibble'a (https://finance.yahoo.com/quote/AAPL/?guccounter=1&guce_referrer=aHR0cHM6Ly93d3cuZ29vZ2xlLmNvbS8&guce_referrer_sig=AQAAAKyUV2RIaX-k7Z0J7nYMBU9us_G1OonuorVaHZvzQNjQpBPb6bKS-IBlirQl5IobGvSlkKXuXs9nF5_hXLDDvYlQpDeVgy3-l_Pxx2_g2uMdh6PW45y1KiSbXlstZm5WeCTkWubXjE1pNu4tHE1nXKrftUfVLRv3uHjJORrNhPGH).

## Analysis
The series of prices are marked as P = pt, where t are consecutive days. The downloaded series of P prices was then recoded as follows
- if there has been an increase in prices, ie Pt> pt-1, then 1;
- if there has been no price increase, ie Pt <= pt-1, then 0.

This functionality is stored in the binaryEncode () function, which takes a price vector as an argument.

Then, the obtained series of zeros and ones were cut into pieces of length n. This functionality was implemented in the cutIntoSequences () function. This function takes any vector and the length of the window as arguments and returns a matrix where the cuts are obtained in rows.

Finally, the format of the obtained data was changed so that each row was saved as a string. For example, "10101", we got this with the encodeAsCharacter () function.
Finally, the probability of "patterns" of increases and decreases in prices was determined with the use of the table() function.

## Summary
The interesting thing about the above analysis is that rises are always more likely than rises. This suggests that in general prices are rising and declines are rather isolated events.
