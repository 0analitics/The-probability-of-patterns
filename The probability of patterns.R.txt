if (!require(quantmod)) install.packages("quantmod")
library(quantmod)
if (!require(dplyr)) install.packages("dplyr")
library(dplyr)

### defining functions

binaryEncode <- function(x) ifelse(diff(x)>0, 1, 0)
  
cutIntoSequences <- function(x, n) {
  
  m <- length(x)
  
  if (n>=m) return(matrix(x, nrow = 1))
  
  indeksy <- 1:n
  M <- x[indeksy]
  for (i in 1:(m-n)) M <- rbind(M, x[indeksy+i])
  
  rownames(M) <- NULL
  
  M
  
} 

encodeAsCharacter <- function(M) apply(M, 1, function(x) paste0(x, collapse = ""))

### example

# data download
d <- as_tibble(getSymbols(Symbols = "AAPL",
                          src = "yahoo",
                          auto.assign = FALSE,
                          from = "2010-01-01",
                          to = "2020-12-31"))

# time series graph
plot(d$AAPL.Adjusted, type = "l")

# binaryEncode function for generated data
s <- 1:5
binaryEncode(s)

# binaryEncode function for generated data
s <- 5:1
binaryEncode(s)

# binaryEncode function for generated data
s <- cumsum(rnorm(10))
s
binaryEncode(s)

# binaryEncode function for acquired time series
dd <- binaryEncode(d$AAPL.Adjusted)
d$AAPL.Adjusted[1:11]
dd[1:10]

# cutIntoSequences function 
cutIntoSequences(1:5, 3)

# cutIntoSequences function 
cutIntoSequences(5:1, 2)

# cutIntoSequences function example application for the obtained series
ddd <- cutIntoSequences(dd, 3)
head(ddd)

# encodeAsCharacter function example for generated data
s <- matrix( rbinom(5*3, 7, 0.5), 5, 3)
s
encodeAsCharacter(s)

# encodeAsCharacter function example for an acquired time series
head(ddd)
dddd <- encodeAsCharacter(ddd)
dddd[1:6]

# the probability of patterns
ddddd <- table(dddd)/length(dddd)
ddddd
barplot(height = ddddd, horiz = TRUE, las = 1)

# example for n=2
dd <- encodeAsCharacter(cutIntoSequences(x = binaryEncode(x = d$AAPL.Adjusted), n = 2))
barplot(height = table(dd)/length(dd), horiz = TRUE, las = 1)
