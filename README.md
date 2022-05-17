# SQL-Hackerrank


select distinct (c.contest_id), (c.hacker_id),c.name, sum(s.total_submissions), sum(s.total_accepted_submissions), sum(v.total_views) ,sum(v.total_unique_views)
from 
Contests c 
left join
Colleges o
on c.contest_id =o.contest_id 
left join
Challenges a
on a.college_id =o.college_id 
left join
(select distinct challenge_id, sum(total_submissions) as total_submissions ,sum(total_accepted_submissions) as total_accepted_submissions from
Submission_Stats  group by challenge_id) s
on a.challenge_id =s.challenge_id 
left join
(select distinct challenge_id, sum(total_views) as total_views , sum(total_unique_views) as total_unique_views 
        from View_Stats group by challenge_id) v
on a.challenge_id=v.challenge_id

group by (c.contest_id), (c.hacker_id),c.name

HAVING SUM(total_submissions)!=0
OR SUM(total_accepted_submissions)!=0
OR SUM(total_views)!=0
OR SUM(total_unique_views)!=0
order by c.contest_id 
