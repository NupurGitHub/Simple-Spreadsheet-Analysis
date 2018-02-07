# Simple-Spreadsheet-Analysis
The marketing ops team sent over this spreadsheet containing four years of data from a CRM system.The team wants to find the month they're likely to contact the most clients, so they can schedule a product upgrade announcement. Which month does the team tend to contact the greatest percentage of its clients?
The link for the data set is below:
https://docs.google.com/spreadsheets/d/16hLtx8bBDe2GS1MOa3v9hY6Yhm4C30koLoCpiIJ5WDg/edit#gid=0


### First I renamed the data set (Sampledata)and read it into R#####

```{r,echo=TRUE}
library(xlsx)
dat=read.xlsx("C:/Users/Nupur/Downloads/Sampledata.xlsx",header=T,1)
########### Then I sorted Date_of_Contact column in ascending order#####

mydat=dat[order(dat$Date_of_Contact),]
head(mydat,n=20)

####### The next step was to  change the format of date and converting it to month and year simply to visualize data properly ######

mydat$Date_of_Contact=as.character(mydat$Date_of_Contact)
mydat$Date_of_Contact <- as.Date(mydat$Date_of_Contact, format="%Y-%m-%d")
Date=format(mydat$Date_of_Contact,"%b-%Y")
Client=mydat$Client_Name
newdata=data.frame(Client,Date)

#### since we have to find the month in which there were maximum number of contacts to the clients, keeping in mind thta here we have to consider
distinct clients that were contacted within a certain month of the year. So I manipulate the dataset to only keep unique values of Clients and the 
corresponding date of contact. For which I did the following:############

Fit=newdata[!duplicated(newdata), ]
head(Fit,n=20)

#### Getting frequency table########
table1=table(Fit$Date)
table1
table2=as.data.frame(table1)
table2
max(table1) ###########Thus the team tend to contact the greatest percentage of its clients in the month of October 2013; which is 31 times########

