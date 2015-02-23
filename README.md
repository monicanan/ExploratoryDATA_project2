# ExploratoryDATA_project2
# couple good R code for me to use in the future.
# for Q1 and Q2
library(data.table)
NEI <- as.data.table(readRDS("summarySCC_PM25.rds"))
plot(NEI[,list(TotalEmissions=sum(Emissions)), by = year]) ## calculate the sum by 
#or
total <- aggregate(Emissions ~ year, NEI, sum)
barplot(height=total$Emissions, names.arg=total$year, xlab="years", ylab=expression("Total" ~ PM[2.5] ~ "Emissions (tons)"), main=expression("Total US" ~ PM[2.5] ~ "Emissions by Year"))
#or
xtabs(Emissions ~ year, data = NEI)


# for Q3 using ggplot
balt <- ddply(NEI[neiData$fips == "24510", ],  .(type,year), summarise, + TotalEmissions = sum(Emissions))
# or
balt <- aggregate(Emissions ~ year + type, NEI, sum)
g <- ggplot(balt, aes(year, TotalEmissions, colour = type))
g <- g + geom_line() + geom_point() + labs(title = "Total Emissions by Type in Baltimore", x = "Year", y = "Total Emissions")
# or
qplot(year, Emissions, data = balt, color = type, geom = "line") + ggtitle(expression("Baltimore City" ~ PM[2.5] ~ "Emissions by Source Type and Year"))
+ xlab("Year") + ylab(expression("Total" ~ PM[2.5] ~ "Emissions (tons)"))
# or
years = rep(c("1999","2002","2005","2008"),4);
types = c(rep(c("POINT"),4),rep(c("NONPOINT"),4),rep(c("ON-ROAD"),4),rep(c("NON-ROAD"),4));
sums = c(1:16);

for(i in 1:16)
{
	sums[i] = sum(NEI[which(NEI["fips"]=="24510" & NEI["year"]==years[i] & NEI["type"]==types[i]),"Emissions"]);
}


# for Q5
qplot(year, TotalEmissions, data=motor, colour=fips, geom="line", main = "Comparison of Total Emissio" )

