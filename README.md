# sql_gsod
Sort of the dataset from NOAA for the year 2023

-- I downloaded this data from noaa_gsod in GoogleCloud - BigQuery .
-- Clicked at gsod2023 to have an overview  at the meterological data for the year 2023.
-- We are interested to get the temprature, wind speed and precipitation for station 'La Guardia 'and 'JFK', for everyday in 2023, in descending orfder by date and ascending order by Station ID.

-- If we look closely to tha data, some value been decsribed as default when the value is missing, with NULL instead,
 
-- QUERY #1 
SELECT 
 stn,
 date,
IF  
 (temp = 9999.9, NULL, temp) AS temperature, 
IF
 (wdsp = "999.9", NULL, CAST(wdsp AS Float64)) AS wind_speed2,
IF 
 (prcp=99.99, 0, prcp) AS prec

FROM 
 bigquery-public-data.noaa_gsod.gsod2023
WHERE
 stn = 72503
 OR
 stn = 744860
ORDER BY 
date desc,
stn acs


-- QUERY #2 
-- Provide a list of the averge temperture for JKF bewtween the 5th MAY till 30th MAY.
SELECT 
 AVG (temperature) as avg_temp
FROM bigquery-public-data.noaa_gsod.gsod2023
WHERE 
 date BETWEEN '2023-05-05' and '2023-05-30'
