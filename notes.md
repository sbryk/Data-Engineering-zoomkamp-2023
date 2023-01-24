## Posgres in docker in WSL
mounting volumes was a bit challenging due windows path
## Q3
Field names in 2019 is different than in 2021 and 2022: lpep_xxx_datetime instead of tpep_xxx_datetime
some ingest script changes was needed

Total count of trips in 2019 is 630918
for 2021 dataset the query for Q3 is

```SQL 
select count(*) 
    from public.yellow_taxi_trips 
where tpep_pickup_datetime::date = '2021-01-15'
  and tpep_dropoff_datetime::date = '2021-01-15'
```
for 2019:
```SQL
select count(*) 
    from public.yellow_taxi_trips 
where lpep_pickup_datetime::date = '2019-01-15'
  and lpep_dropoff_datetime::date = '2019-01-15'
```
**Answer is 20530**

Need Double quoting capitalized column names in Postgres is confusing

General problems with acces to git repository, as GitHub dropped password auth. 
Got help from 

https://www.youtube.com/watch?v=kHkQnuYzwoo 

https://stackoverflow.com/questions/18935539/authenticate-with-github-using-a-token

https://medium.com/@obielum1858/using-personal-access-tokens-with-git-and-github-to-push-4fd22ef79db8


Formatting with Markdown:
https://www.freecodecamp.org/news/how-to-format-code-in-markdown/
https://www.markdownguide.org/basic-syntax/