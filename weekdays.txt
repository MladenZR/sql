# sql

#group events by weekdays
SELECT DATE(cet_datetime) AS Date, 
DAYNAME(cet_datetime) AS DAYNAME,
COUNT(event_name) AS "All events",
(COUNT(CASE WHEN event_name = A THEN A END)) AS "Good events",
(COUNT(CASE WHEN event_name = A THEN A END)
    +COUNT(CASE WHEN event_name = B THEN A END)
    +COUNT(CASE WHEN event_name = C THEN A END)
    +COUNT(CASE WHEN event_name = E THEN A END)) AS "Total events",
    (COUNT(CASE WHEN event_name = A THEN A END))/
(COUNT(CASE WHEN event_name = A THEN A END)
    +COUNT(CASE WHEN event_name = B THEN A END)
    +COUNT(CASE WHEN event_name = C THEN A END)
    +COUNT(CASE WHEN event_name = D THEN A else 0 END)) AS "Rate of good events"
FROM datebase_name.table_name
WHERE cet_datetime > DATE_SUB(NOW(), INTERVAL 365 DAY)
GROUP BY 1
ORDER BY 1 ASC
