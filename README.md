# sql
# distinct
# case when
# right join
# interval
# time interval
SELECT DATE(a.datetime) AS Date, 
(COUNT(CASE WHEN message = A THEN A END)) AS "Great",
(COUNT(CASE WHEN message = A THEN A END)
    +COUNT(CASE WHEN message = B THEN A END)
    +COUNT(CASE WHEN message = C THEN A END)
    +COUNT(CASE WHEN message = 5 THEN A END)) AS "Total",
    (COUNT(CASE WHEN message = A THEN A END))/(COUNT(CASE WHEN message = A THEN A END)
    +COUNT(CASE WHEN message = B THEN A END)
    +COUNT(CASE WHEN message = C THEN A END)
    +COUNT(CASE WHEN message = E THEN A END)) AS "Good",
(SELECT(CASE WHEN count(distinct(user))= 0 THEN A else 0 END))/(COUNT(CASE WHEN message = A THEN A END)
    +COUNT(CASE WHEN message = B THEN A END)
    +COUNT(CASE WHEN message = C THEN A END)
    +COUNT(CASE WHEN message = E THEN A END)) AS "Average",
(SELECT(CASE WHEN count(distinct(user)) = A THEN A else 0 END))/(COUNT(CASE WHEN message = A THEN A END)
    +COUNT(CASE WHEN message = B THEN A END)
    +COUNT(CASE WHEN message = C THEN A END)
    +COUNT(CASE WHEN message = E THEN A END)) AS "Under average",
(SELECT(CASE WHEN count(distinct(user))> A THEN A else 0 END))/(COUNT(CASE WHEN message = A THEN A END)
    +COUNT(CASE WHEN message = B THEN A END)
    +COUNT(CASE WHEN message = C THEN A END)
    +COUNT(CASE WHEN message = E THEN A END)) AS "Low score"
FROM table_name.a a
  RIGHT JOIN database_name.table_name b ON b.message_id=a.message_id
  WHERE a.datetime > DATE_SUB(NOW(), INTERVAL 30 DAY)
  GROUP BY 1
