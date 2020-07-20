# AnaPhD
PhD Analysis
001_Data organization
-> putting cooredenates from one table to other

#Two datasets used
coord <- read.csv("dados/raw/CoordAlt.csv", sep = ";")
loc <- read.csv("dados/raw/LocReg.csv", sep = ";")

#Verify
names(loc)
names(coord)

#Put new colluns in "loc"
loc$lat <- numeric(length = nrow(loc))
loc$lon <- numeric(length = nrow(loc))
loc$alt <- numeric(length = nrow(loc))

#Turn "munic" and "uf" as character
loc$munic <- as.character(loc$munic)
loc$uf <- as.character(loc$uf)

#For to complete new collums in "loc" with values from collums in "coord"
for(i in 1:nrow(loc)){
  x <- loc$munic[i]
  y <- loc$uf[i]
  loc[loc$munic==x & loc$uf==y, c("lat", "lon", "alt")] <- coord[coord$munic==x & coord$uf==y, c("lat", "lon", "alt")]
}

str(loc)

loc$munic <- as.factor(loc$munic)
loc$uf <- as.factor(loc$uf)
