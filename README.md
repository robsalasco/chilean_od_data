# Chilean Origin - Destination data

This data has been retrieved from the MTT's EOD Survey 2012 (http://www.sectra.gob.cl/biblioteca/detalle1.asp?mfn=3253).

## How to access 

```
library(RJDBC)
library(readr)
options(java.parameters = "-Xmx4g")

conn <- dbConnect(JDBC("net.ucanaccess.jdbc.UcanloadDriver",
                       "/Users/robsalasco/Documents/Dev/chilean_od_data/UCanAccess-4.0.4-bin/loader/ucanload.jar"), "jdbc:ucanaccess:///Users/robsalasco/Documents/Dev/chilean_od_data/base_datos_eodStgo_2012.accdb")

dbListTables(conn)

dbFetch(dbSendQuery(conn, "SELECT * FROM `Comuna Origen`"))

#t <- dbSendQuery(conn, "SELECT * FROM Viaje WHERE ComunaOrigen = 71 AND ComunaDestino = 71 LIMIT 10")

t <- dbSendQuery(conn, "SELECT * FROM Viaje")
t <- dbFetch(t)

write_csv(t, "table_Viajes.csv")
```
