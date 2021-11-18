# Austin 311 Complaints Summary

The analysis below investigates the frequency and nature of 311 calls in Austin, TX.

## Complaints by Day
```complaints_by_day
select
extract(date from created_date) as date, 
count(*) as complaints 

from `bigquery-public-data.austin_311.311_service_requests` 
 
group by date 
order by date desc
```
### Summary
The most recent day of data was logged on <Value data={data.complaints_by_day} fmt=date/> and the number of complaints was <Value data={data.complaints_by_day} column="complaints"/>.

### Daily Chart
<LineChart 
    data={data.complaints_by_day} 
    x=date 
    y=complaints
/>

## Complaints by Department
```complaints_by_department
select owning_department as department,
count(*) as complaints

from `bigquery-public-data.austin_311.311_service_requests` 

group by department
order by complaints desc
```

{#each data.complaints_by_department as cbdept}

* [{cbdept.department}](/austin-311/department/{cbdept.department}): <Value value={cbdept.complaints} />

{/each}