```
> dim(USArrests)
[1] 50  4
> new_df <- USArrests[sample(1:50,12,replace = FALSE),]
> new_df
              Murder Assault UrbanPop Rape
Kansas           6.0     115       66 18.0
Mississippi     16.1     259       44 17.1
Washington       4.0     145       73 26.2
Texas           12.7     201       80 25.5
Massachusetts    4.4     149       85 16.3
Hawaii           5.3      46       83 20.2
Connecticut      3.3     110       77 11.1
Arkansas         8.8     190       50 19.5
Georgia         17.4     211       60 25.8
Oklahoma         6.6     151       68 20.0
New Mexico      11.4     285       70 32.1
Alaska          10.0     263       48 44.5
```