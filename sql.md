# SQL


```SQL
SELECT
    field1           AS field1,
    longFieldName    AS lfn,
    IF( expr, 1, 2 ) AS exprColumn
FROM tbl AS a
LEFT JOIN reltbl AS b ON a.parentID = b.relatedID AND a.parentID2 = b.relatedID2
INNER JOIN (
    SELECT
    FROM
    WHERE
) AS c
WHERE a = 1
  AND b = 2
  AND c = 3
  AND (
      foo = 'bar' OR
      baz = 'bla'
  )
GROUP BY 1, 2
ORDER BY 1
LIMIT 100
```
