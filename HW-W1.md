# Homework for Week 1

## Q1
Which tag has the following text? *- Write the image ID to the file*
**--iidfile string**

## Q2
Run docker with the python:3.9 image in an interactive mode and the entrypoint of bash. Now check the python modules that are installed ( use pip list). How many python packages/modules are installed?
**3**
pip
setuptools
wheel


##P repare Postgres

Run Postgres and load data as shown in the videos We'll use the green taxi trips from January 2019:

 wget https://github.com/DataTalksClub/nyc-tlc-data/releases/download/green/green_tripdata_2019-01.csv.gz
** --- **
You will also need the dataset with zones:

 wget https://s3.amazonaws.com/nyc-tlc/misc/taxi+_zone_lookup.csv
**done**

Download this data and put it into Postgres (with jupyter notebooks or with a pipeline)
**done with pipeline**

## Q3
How many taxi trips were totally made on January 15?

Tip: started and finished on 2019-01-15.
**20530**

## Q4
### Largest trip for each day###
Which was the day with the largest trip distance? Use the pick up time for your calculations.
simplest query is
```select ytt.lpep_pickup_datetime::date 
    from public.yellow_taxi_trips ytt
    where ytt.trip_distance in 
	    (select max(trip_distance) as distance
		    from public.yellow_taxi_trips)```SQL

**Answer is 2019-01-15**
the longest trip is 117,99 km

## Q5. The number of passengers 
### In 2019-01-01 how many trips had 2 and 3 passengers?
The query I used:
```select '2 : ', count (*) 
    from public.yellow_taxi_trips ytt
    where ytt.passenger_count = 2 
    and ytt.lpep_pickup_datetime::date = '2019-01-01'
    union
    select '3 : ', count (*) 
    from public.yellow_taxi_trips ytt
    where ytt.passenger_count = 3 
    and ytt.lpep_pickup_datetime::date = '2019-01-01'```SQL
	 
Answer is:
**2 : 	1282**
**3 : 	254**	 
## Q6. Largest tip
### For the passengers picked up in the Astoria Zone which was the drop off zone that had the largest tip? We want the name of the zone, not the id.
The query I used:
```select ytt2."DOLocationID", z2."Zone"
        from yellow_taxi_trips ytt2 
        left join taxi_zones_lookup z2 on z2."LocationID" = ytt2."DOLocationID"
        where ytt2.index =
            (select index
                from yellow_taxi_trips
                where tip_amount =
                (select max(tip_amount)
                    from yellow_taxi_trips ytt
                    left join taxi_zones_lookup z on ytt."PULocationID" =  z."LocationID"
                    where z."Zone" = 'Astoria')
            )```SQL

it was tricky to figure out that some column names should be put in "" as "PULocationID". I don't know why. I must investigate it.
Update 1
The explanation is - Postgres is case sensitive, so column "ColName" should be double-quoted

The answer is **Long Island City/Queens Plaza**