library(tidyverse)
library(plyr)

#set working directory to location of order files
setwd("D:/My Documents/Dashing/orders")

#put all files in folder into data frame
file_names <- dir() 
df1 <- do.call(rbind.fill,lapply(file_names,read.csv))

#disable scientific notation
options(scipen=999)

#set description as character
df1$Products.Description <- as.character(df1$Products.Description)

#drop unnecessary columns
removed.columns <- c("Location.ID","MSRP", "MAP", "Line.Note", "Product.Note")
df1 <- df1[ , !(names(df1) %in% removed.columns)]

#rename Part.Number as Part.No
colnames(df1)[1] <- "Part.No"

#seperate Part # and quantities
part.numbers.and.quantities <- df1[ ,c(1,3)]
df1 <- df1[ , -3]

#sum quantities of items sharing part #
quantities.sum <- ddply(part.numbers.and.quantities, "Part.No", numcolwise(sum))

#remove duplicate part entries
df1 <- df1[!duplicated(df1$Part.No), ]

#re-merge part descriptions and quantities ordered
df1 <- merge(df1, quantities.sum, by = "Part.No") 

#remove quantities under 2
high.quantity <- subset(df1, Quantity >= 5)

#AND/OR

#remove items with less than $50 ordered
high.quantity <- subset(df1, Quantity*Price >=50)

#sort in alphabetical order
high.quantity <- high.quantity[order(high.quantity$Products.Description),]
        
#reorder columns
high.quantity <- high.quantity[ , c(1,4,2,3,5,6)]

#find number of characters in product descriptions
char.num <- nchar(high.quantity$Products.Description)

#remove repeating words in product descriptions
high.quantity$Products.Description <- substr(high.quantity$Products.Description, 1, char.num/2)

#remove quantity column
high.quantity <- select(high.quantity, -Quantity)

#write to .csv in designated directory
setwd("D:/My Documents/Dashing")
write.csv(high.quantity, file="CommonItems.csv", row.names = FALSE)







