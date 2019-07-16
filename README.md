# Recuiter-Filter-Tool
A R tool which can help the recruiters to filter through a huge list of contacts to a list of prospective candidates based on their work experience and position.
The code below allows the recuiters to upload their input file consisting the list of candidates and a list a companies to filter. They can also filter by the candidate's position.
rm(list=ls())
#install.packages("slam")
library(dplyr)
library(magrittr)
library(tidyr)
library(stringr)
library(tm)
library(slam)

candidatelist <- read_excel(" ", sheet=" ")
companylist <-read.csv(" ")

colnames(candidatelist)=c("Fname","Lname","Company","Position")

rec <- mutate_each(candidatelist,funs(toupper))%>%
  unite("Name",Fname,Lname,sep = " ")

companylist <- mutate_each(f500,funs(toupper))

#company_filter 
rec1= rec[rec$Company %in% companylist$Company,]


selected_list <- setNames(data.frame(matrix(ncol = 3)), c("Name", "Company", "Position"))
want_more = "YES"

while(want_more == "YES"){
  pos = readline(prompt = "Enter the position:")
  for(i in range(length(rec))){
    df = rec[str_detect(rec$Position,pos),]
  }
  selected_list <- rbind(selected_list,df)
  rec= rec[!rec$Position  %in% selected_list$Position,]
  want_more = readline(prompt = "Want to Filter Again:")
}

newdata <- selected_list[order(selected_list$Name),]
