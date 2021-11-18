# {$page.params.department}

```complaints_by_department
select owning_department as department,
count(*) as complaints
from `bigquery-public-data.austin_311.311_service_requests` 

group by department
order by complaints DESC
```

```complaints_by_day_department
select
owning_department as department,
extract(date from created_date) as date, 
count(*) as complaints 

from `bigquery-public-data.austin_311.311_service_requests` 
 
group by department, date 
order by date desc
```

<Value data={data.complaints_by_department.filter(d => d.department === $page.params.department)} column=complaints/> complaints.

<LineChart data={data.complaints_by_day_department.filter(d => d.department === $page.params.department)} x=date y=complaints/>