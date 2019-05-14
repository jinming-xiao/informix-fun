<b>informix Recursive Common Table Expression</b>

<pre>
Common Table Expression is a SQL standard feature, it can help customers
	•	simplify queries and make queries more readable
	•	use recursive CTE to query hierarchical data, and tree/graph structured data
	•	do programming tasks
 
Informix 14.10 release supports
	•	non-recursive CTE
	•	Recursive CTE
	•	Multiple CTEs, nested recursive CTEs in one query
	•	CTE with Insert, Update, Delete statements 
	•	CTE in view 
	•	CTE in SPL 
	•	CTE in Trigger
	•	CTE in subquery
</pre>

<b>Recursive CTE</b>
A recursive query starts with either one non-recursive sub-query or
several non-recursive sub-queries joined by UNION or UNION ALL, and ends
with exactly one recursive sub-query joined by UNION ALL.  A recursive
sub-query references the CTE being defined.

example of a recursive query computing the factorial of numbers from 0 to 9 is the following:
<pre>
WITH temp (n, fact) AS (
    SELECT 0, 1                      -- Initial Subquery
    UNION ALL 
    SELECT n+1, (n+1)*fact FROM temp -- Recursive Subquery 
        WHERE n < 9)
SELECT * FROM temp;

            n             fact 

            0                1
            1                1
            2                2
            3                6
            4               24
            5              120
            6              720
            7             5040
            8            40320
            9           362880
</pre>

query to generate Fibonacci number
<pre>
-- Fibonacci number
WITH fib(p, n) as
(
    select 0, 1
    UNION ALL
    select n, p+n from fib
        where n < 100
)
select * from fib;
          p             n 

          0             1
          1             1
          1             2
          2             3
          3             5
          5             8
          8            13
         13            21
         21            34
         34            55
         55            89
         89           144
</pre>

<b>Example query to display ‘INFORMIX FUN’</b>
<pre>

_1   ####             ###                             ##                    #######                  
_2    ##             ## ##                                                   ##   #                  
_3    ##    #####    ##      ####   ## ###  ##  ##   ###    ##   ##          ## #   ##  ##  #####    
_4    ##    ##  ##  ####    ##  ##   ### ## #######   ##     ## ##           ####   ##  ##  ##  ##   
_5    ##    ##  ##   ##     ##  ##   ##  ## #######   ##      ###            ## #   ##  ##  ##  ##   
_6    ##    ##  ##   ##     ##  ##   ##     ## # ##   ##     ## ##           ##     ##  ##  ##  ##   
_7   ####   ##  ##  ####     ####   ####    ##   ##  ####   ##   ##         ####     ### ## ##  ##   
_8         
</pre>

(0) before the example, we need a aggregation help function to concatenate string
<pre> 
create function plus(s1 lvarchar, s2 lvarchar)
        returning lvarchar;
    return s1 || s2;
end function;
</pre>

(1) public domain 8x8 VGA fonts from https://github.com/dhepper/font8x8
<pre>
with fonts(c, c1, c2,c3,c4,c5,c6,c7,c8) as (
select * from table(multiset{
ROW(' ', '0x00', '0x00', '0x00', '0x00', '0x00', '0x00', '0x00', '0x00'),
ROW('!', '0x18', '0x3C', '0x3C', '0x18', '0x18', '0x00', '0x18', '0x00'),
ROW('A', '0x0C', '0x1E', '0x33', '0x33', '0x3F', '0x33', '0x33', '0x00'),
ROW('B', '0x3F', '0x66', '0x66', '0x3E', '0x66', '0x66', '0x3F', '0x00'),
ROW('C', '0x3C', '0x66', '0x03', '0x03', '0x03', '0x66', '0x3C', '0x00'),
ROW('D', '0x1F', '0x36', '0x66', '0x66', '0x66', '0x36', '0x1F', '0x00'),
ROW('E', '0x7F', '0x46', '0x16', '0x1E', '0x16', '0x46', '0x7F', '0x00'),
ROW('F', '0x7F', '0x46', '0x16', '0x1E', '0x16', '0x06', '0x0F', '0x00'),
ROW('G', '0x3C', '0x66', '0x03', '0x03', '0x73', '0x66', '0x7C', '0x00'),
ROW('H', '0x33', '0x33', '0x33', '0x3F', '0x33', '0x33', '0x33', '0x00'),
ROW('I', '0x1E', '0x0C', '0x0C', '0x0C', '0x0C', '0x0C', '0x1E', '0x00'),
ROW('J', '0x78', '0x30', '0x30', '0x30', '0x33', '0x33', '0x1E', '0x00'),
ROW('K', '0x67', '0x66', '0x36', '0x1E', '0x36', '0x66', '0x67', '0x00'),
ROW('L', '0x0F', '0x06', '0x06', '0x06', '0x46', '0x66', '0x7F', '0x00'),
ROW('M', '0x63', '0x77', '0x7F', '0x7F', '0x6B', '0x63', '0x63', '0x00'),
ROW('N', '0x63', '0x67', '0x6F', '0x7B', '0x73', '0x63', '0x63', '0x00'),
ROW('O', '0x1C', '0x36', '0x63', '0x63', '0x63', '0x36', '0x1C', '0x00'),
ROW('P', '0x3F', '0x66', '0x66', '0x3E', '0x06', '0x06', '0x0F', '0x00'),
ROW('Q', '0x1E', '0x33', '0x33', '0x33', '0x3B', '0x1E', '0x38', '0x00'),
ROW('R', '0x3F', '0x66', '0x66', '0x3E', '0x36', '0x66', '0x67', '0x00'),
ROW('S', '0x1E', '0x33', '0x07', '0x0E', '0x38', '0x33', '0x1E', '0x00'),
ROW('T', '0x3F', '0x2D', '0x0C', '0x0C', '0x0C', '0x0C', '0x1E', '0x00'),
ROW('U', '0x33', '0x33', '0x33', '0x33', '0x33', '0x33', '0x3F', '0x00'),
ROW('V', '0x33', '0x33', '0x33', '0x33', '0x33', '0x1E', '0x0C', '0x00'),
ROW('W', '0x63', '0x63', '0x63', '0x6B', '0x7F', '0x77', '0x63', '0x00'),
ROW('X', '0x63', '0x63', '0x36', '0x1C', '0x1C', '0x36', '0x63', '0x00'),
ROW('Y', '0x33', '0x33', '0x33', '0x1E', '0x0C', '0x0C', '0x1E', '0x00'),
ROW('Z', '0x7F', '0x63', '0x31', '0x18', '0x4C', '0x66', '0x7F', '0x00'),
ROW('a', '0x00', '0x00', '0x1E', '0x30', '0x3E', '0x33', '0x6E', '0x00'),
ROW('b', '0x07', '0x06', '0x06', '0x3E', '0x66', '0x66', '0x3B', '0x00'),
ROW('c', '0x00', '0x00', '0x1E', '0x33', '0x03', '0x33', '0x1E', '0x00'),
ROW('d', '0x38', '0x30', '0x30', '0x3e', '0x33', '0x33', '0x6E', '0x00'),
ROW('e', '0x00', '0x00', '0x1E', '0x33', '0x3f', '0x03', '0x1E', '0x00'),
ROW('f', '0x1C', '0x36', '0x06', '0x0f', '0x06', '0x06', '0x0F', '0x00'),
ROW('g', '0x00', '0x00', '0x6E', '0x33', '0x33', '0x3E', '0x30', '0x1F'),
ROW('h', '0x07', '0x06', '0x36', '0x6E', '0x66', '0x66', '0x67', '0x00'),
ROW('i', '0x0C', '0x00', '0x0E', '0x0C', '0x0C', '0x0C', '0x1E', '0x00'),
ROW('j', '0x30', '0x00', '0x30', '0x30', '0x30', '0x33', '0x33', '0x1E'),
ROW('k', '0x07', '0x06', '0x66', '0x36', '0x1E', '0x36', '0x67', '0x00'),
ROW('l', '0x0E', '0x0C', '0x0C', '0x0C', '0x0C', '0x0C', '0x1E', '0x00'),
ROW('m', '0x00', '0x00', '0x33', '0x7F', '0x7F', '0x6B', '0x63', '0x00'),
ROW('n', '0x00', '0x00', '0x1F', '0x33', '0x33', '0x33', '0x33', '0x00'),
ROW('o', '0x00', '0x00', '0x1E', '0x33', '0x33', '0x33', '0x1E', '0x00'),
ROW('p', '0x00', '0x00', '0x3B', '0x66', '0x66', '0x3E', '0x06', '0x0F'),
ROW('q', '0x00', '0x00', '0x6E', '0x33', '0x33', '0x3E', '0x30', '0x78'),
ROW('r', '0x00', '0x00', '0x3B', '0x6E', '0x66', '0x06', '0x0F', '0x00'),
ROW('s', '0x00', '0x00', '0x3E', '0x03', '0x1E', '0x30', '0x1F', '0x00'),
ROW('t', '0x08', '0x0C', '0x3E', '0x0C', '0x0C', '0x2C', '0x18', '0x00'),
ROW('u', '0x00', '0x00', '0x33', '0x33', '0x33', '0x33', '0x6E', '0x00'),
ROW('v', '0x00', '0x00', '0x33', '0x33', '0x33', '0x1E', '0x0C', '0x00'),
ROW('w', '0x00', '0x00', '0x63', '0x6B', '0x7F', '0x7F', '0x36', '0x00'),
ROW('x', '0x00', '0x00', '0x63', '0x36', '0x1C', '0x36', '0x63', '0x00'),
ROW('y', '0x00', '0x00', '0x33', '0x33', '0x33', '0x3E', '0x30', '0x1F'),
ROW('z', '0x00', '0x00', '0x3F', '0x19', '0x0C', '0x26', '0x3F', '0x00'),
})),
</pre>

(2) set the text we want to processing
<pre>
text(str) as (
    -- change this to other content 
    select 'Informix Fun’
),
</pre>
                                                                                                            
(3) get the text font data from above CTE ‘fonts’:
<pre>
xword(str, o, c, c1, c2,c3,c4,c5,c6,c7,c8) as (
    select str, 1, c, c1, c2,c3,c4,c5,c6,c7,c8
        from text, fonts where c = substr(str, 1, 1)
    union all
    select str, o+1, c, c1, c2,c3,c4,c5,c6,c7,c8 from fonts, xword
        where fonts.c = substr(str, o+1, 1) and o < length(str)
    — ‘o’ is the order for each character in the text
),
</pre>

(4) for loop to get 0x80, 0x40, 0x20, 0x10, 0x08, 0x04, 0x02, 0x01
<pre>
x(n, p) as (
    select 1, 128 union all select n+1, p/2 from x where n < 8
),
</pre>

(5) print ‘X’ or ‘ ‘ for each bit in the font data for each character
<pre>
show as (
select
        sum((case when bitand(to_number(c1)::int, p) > 0
                then 'X' else ' ' end)::lvarchar)::char(8) as c1,
        sum((case when bitand(to_number(c2)::int, p) > 0
                then 'X' else ' ' end)::lvarchar)::char(8) as c2,
        sum((case when bitand(to_number(c3)::int, p) > 0
                then 'X' else ' ' end)::lvarchar)::char(8) as c3,
        sum((case when bitand(to_number(c4)::int, p) > 0
                then 'X' else ' ' end)::lvarchar)::char(8) as c4,
        sum((case when bitand(to_number(c5)::int, p) > 0
                then 'X' else ' ' end)::lvarchar)::char(8) as c5,
        sum((case when bitand(to_number(c6)::int, p) > 0
                then 'X' else ' ' end)::lvarchar)::char(8) as c6,
        sum((case when bitand(to_number(c7)::int, p) > 0
                then 'X' else ' ' end)::lvarchar)::char(8) as c7,
        sum((case when bitand(to_number(c8)::int, p) > 0
                then 'X' else ' ' end)::lvarchar)::char(8) as c8
from x cross join xword
group by xword.o
order by xword.o desc)
</pre>

<b>Example of a Hierarchical Data Set</b>
<pre>
In several topics that follow, SQL code examples that illustrate hierarchical queries are based on hierarchic data in the following employee table, whose rows contains information about employees within an organizational hierarchy. The mgrid column shows the employee identifier (empid) of the manager to whom the employee reports:
CREATE TABLE employee(
                      empid  INTEGER NOT NULL PRIMARY KEY,
                      name   VARCHAR(10),
                      salary DECIMAL(9, 2),
                      mgrid  INTEGER
);
</pre>
Data values for the 17 rows in the employee table are these.
<pre>
INSERT INTO employee VALUES  ( 1, 'Jones',    30000, 10);
INSERT INTO employee VALUES  ( 2, 'Hall',     35000, 10);
INSERT INTO employee VALUES  ( 3, 'Kim',      40000, 10);
INSERT INTO employee VALUES  ( 4, 'Lindsay',  38000, 10);
INSERT INTO employee VALUES  ( 5, 'McKeough', 42000, 11);
INSERT INTO employee VALUES  ( 6, 'Barnes',   41000, 11);
INSERT INTO employee VALUES  ( 7, 'O''Neil',  36000, 12);
INSERT INTO employee VALUES  ( 8, 'Smith',    34000, 12);
INSERT INTO employee VALUES  ( 9, 'Shoeman',  33000, 12);
INSERT INTO employee VALUES  (10, 'Monroe',   50000, 15);
INSERT INTO employee VALUES  (11, 'Zander',   52000, 16);
INSERT INTO employee VALUES  (12, 'Henry',    51000, 16);
INSERT INTO employee VALUES  (13, 'Aaron',    54000, 15);
INSERT INTO employee VALUES  (14, 'Scott',    53000, 16);
INSERT INTO employee VALUES  (15, 'Mills',    70000, 17);
INSERT INTO employee VALUES  (16, 'Goyal',    80000, 17);
INSERT INTO employee VALUES  (17, 'Urbassek', 95000, NULL);
</pre>

Query of report chain of 'Goyal'
<pre>
WITH cte AS (
  SELECT empid, name, mgrid, name::char(32) as report, 1 AS level
    FROM employee
    WHERE name = 'Goyal'
  UNION ALL
  SELECT t.empid, t.name, t.mgrid, trim(report) || ' <- ' || t.name, (cte.level + 1)
    FROM employee t, cte
  where cte.empid = t.mgrid
  )
SELECT empid, name, report from cte;

      empid name       report                                         

         16 Goyal      Goyal                                         
         14 Scott      Goyal <- Scott                                
         12 Henry      Goyal <- Henry                                
          9 Shoeman    Goyal <- Henry <- Shoeman                     
          8 Smith      Goyal <- Henry <- Smith                       
          7 O'Neil     Goyal <- Henry <- O'Neil                      
         11 Zander     Goyal <- Zander                               
          6 Barnes     Goyal <- Zander <- Barnes                     
          5 McKeough   Goyal <- Zander <- McKeough                   

9 row(s) retrieved.
</pre>
<b>Query to produce an ASCII-art image of the Mandelbrot set</b>

<pre>
-- ported from PostgreSQL version https://explainextended.com/2013/12/31/happy-new-year-5/

WITH    x(n) AS ( select -80 UNION ALL select n+1 from x where n < 80),
        y(j) AS ( select -50 UNION ALL select j+1 from y where j < 50),
        q (r, i, rx, ix, g) AS (
        SELECT  n::float * 0.02, j::float * 0.04, 0::float, 0::float, 0
        FROM    (select n from x) cross join (select j from y)
        UNION ALL
        SELECT  r, i, 
                CASE WHEN ABS(rx * rx + ix * ix) <= 2 THEN rx * rx - ix * ix END + r, 
                CASE WHEN ABS(rx * rx + ix * ix) <= 2 THEN 2 * rx * ix END + i, 
                g + 1
        FROM    q WHERE   rx IS NOT NULL AND g < 99),
        Zt (i, r, x) AS (
        -- SELECT i, r, SUBSTR(" .:-=+*#%@", (MAX(g) /10 +1)::int, 1) as x
        --                      01234567890123456789012345678901234567890123456789
        SELECT i, r,    SUBSTR("@@B%8&WM#*oaqwmO0Ucrt/\|()1{}[]?-_+~<>i!l;;:,``'.", 50 - (MAX(g)/2)::int, 1) as x
        -- SELECT i, r,    SUBSTR(" ..,,,-----++++====***%%%%@@@@@#####", 50 - (MAX(g)/2)::int, 1) as x
        FROM q GROUP BY i, r order by r desc)
SELECT  sum(x::lvarchar) as x from Zt group by i order by i;

x  ................................................................................................................................................................. 
x  ................................................................................................................................................................. 
x  ......................................''''''''''''''''''''''''''''``````l........................................................................................ 
x  ..............................'''''''''''''''''''''''''''''''''''```````,;,,,`,l@................................................................................ 
x  .............................'''''''''''''''''''''''''''''''''''`````````,:l;,````''''........................................................................... 
x  ...........................''''''''''''''''''''''''''''''''''''``````````:l!:,`````'''''''....................................................................... 
x  .........................'''''''''''''''''''''''''''''''''''''``````;,,:;{@o/i```````'''''''''................................................................... 
x  ........................''''''''''''''''''''''''''''''''''''``````i;?;;\@r@U>!;:i:`````''''''''''................................................................ 
x  ......................'''''''''''''''''''''''''''''''''''''````````:;@@@@@@@@@|*l,`````````'''''''''............................................................. 
x  .....................'''''''''''''''''''''''''''''''''''```````````i-U@@@@@@@@@>_~`````````````'''''''........................................................... 
x  ....................''''''''''''''''''''''''''''''''''```````````,,:r@@@@@@@@@@<;,````````````````''''''......................................................... 
x  ..................''''''''''''''''''''''''''''''''',,:;,````::i,,,:;;l{@@@@@@@];;::,,,,!``````````;;''''''....................................................... 
x  .................''''''''''''''''''''''''''''''``,:l{l;;1,,:i~t#l@~@@@@@@@@@@@@@\0a{;)>t],``````,;?``'''''''..................................................... 
x  ................''''''''''''''''''''''''''```````,:;U@@@@{;@>@@@@@@@@@@@@@@@@@@@@@@@@@@);{,,:;<;;;<<;`''''''''................................................... 
x  ................'''''''''''''''''''''`````````````,_@@@@@?@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@;[@@@@}l,>``''''''''.................................................. 
x  ...............''''''''''''''''``````````````````,,:;!+U@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@i~`````''''''''................................................. 
x  ..............'''''''''''''''`````````````````:;;;;@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@+!;,,``````'''''''''............................................... 
x  .............''''''''''''''``````````````````;[}@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@];:``````''''''''''.............................................. 
x  .............''''''''''''````````````````````,:;)\@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@:,``,,`'''''''''''............................................. 
x  ............'''''''''''`````````````````````lr*>@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@>@_;<,`'''''''''''............................................. 
x  ............'''''''';:;:,,,:;l;,,,````````,,:l_@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@M@{;i``''''''''''''............................................ 
x  ...........'''````,,:;[<_;l;l[@/;l};:,,,,,,;@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@!:,```'''''''''''''........................................... 
x  ...........```````,,!<@@@+@@@@@@@@@+i[;::::~@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@>:l`''''''''''''''........................................... 
x  ...........```````::;!@@@@@@@@@@@@@@@@@];;;!@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@~_?,`'''''''''''''''.......................................... 
x  ..........```````;_@&@@@@@@@@@@@@@@@@@@@]ll-@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@:```'''''''''''''''.......................................... 
x  ..........```,,,::q@@@@@@@@@@@@@@@@@@@@@@@>@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@;,```''''''''''''''''......................................... 
x  ..........``ll~!l!U@@@@@@@@@@@@@@@@@@@@@@@8@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@;`````''''''''''''''''......................................... 
x  ..........,;)@@@@B@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@,``````''''''''''''''''......................................... 
x  ..........@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@+;:,```````''''''''''''''''......................................... 
x  ..........,;)@@@@B@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@,``````''''''''''''''''......................................... 
x  ..........``ll~!l!U@@@@@@@@@@@@@@@@@@@@@@@8@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@;`````''''''''''''''''......................................... 
x  ..........```,,,::q@@@@@@@@@@@@@@@@@@@@@@@>@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@;,```''''''''''''''''......................................... 
x  ..........```````;_@&@@@@@@@@@@@@@@@@@@@]ll-@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@:```'''''''''''''''.......................................... 
x  ...........```````::;!@@@@@@@@@@@@@@@@@];;;!@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@~_?,`'''''''''''''''.......................................... 
x  ...........```````,,!<@@@+@@@@@@@@@+i[;::::~@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@>:l`''''''''''''''........................................... 
x  ...........'''````,,:;[<_;l;l[@/;l};:,,,,,,;@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@!:,```'''''''''''''........................................... 
x  ............'''''''';:;:,,,:;l;,,,````````,,:l_@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@M@{;i``''''''''''''............................................ 
x  ............'''''''''''`````````````````````lr*>@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@>@_;<,`'''''''''''............................................. 
x  .............''''''''''''````````````````````,:;)\@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@:,``,,`'''''''''''............................................. 
x  .............''''''''''''''``````````````````;[}@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@];:``````''''''''''.............................................. 
x  ..............'''''''''''''''`````````````````:;;;;@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@+!;,,``````'''''''''............................................... 
x  ...............''''''''''''''''``````````````````,,:;!+U@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@i~`````''''''''................................................. 
x  ................'''''''''''''''''''''`````````````,_@@@@@?@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@;[@@@@}l,>``''''''''.................................................. 
x  ................''''''''''''''''''''''''''```````,:;U@@@@{;@>@@@@@@@@@@@@@@@@@@@@@@@@@@);{,,:;<;;;<<;`''''''''................................................... 
x  .................''''''''''''''''''''''''''''''``,:l{l;;1,,:i~t#l@~@@@@@@@@@@@@@\0a{;)>t],``````,;?``'''''''..................................................... 
x  ..................''''''''''''''''''''''''''''''''',,:;,````::i,,,:;;l{@@@@@@@];;::,,,,!``````````;;''''''....................................................... 
x  ....................''''''''''''''''''''''''''''''''''```````````,,:r@@@@@@@@@@<;,````````````````''''''......................................................... 
x  .....................'''''''''''''''''''''''''''''''''''```````````i-U@@@@@@@@@>_~`````````````'''''''........................................................... 
x  ......................'''''''''''''''''''''''''''''''''''''````````:;@@@@@@@@@|*l,`````````'''''''''............................................................. 
x  ........................''''''''''''''''''''''''''''''''''''``````i;?;;\@r@U>!;:i:`````''''''''''................................................................ 
x  .........................'''''''''''''''''''''''''''''''''''''``````;,,:;{@o/i```````'''''''''................................................................... 
x  ...........................''''''''''''''''''''''''''''''''''''``````````:l!:,`````'''''''....................................................................... 
x  .............................'''''''''''''''''''''''''''''''''''`````````,:l;,````''''........................................................................... 
x  ..............................'''''''''''''''''''''''''''''''''''```````,;,,,`,l@................................................................................ 
x  ......................................''''''''''''''''''''''''''''``````l........................................................................................ 
x  ................................................................................................................................................................. 
x  ................................................................................................................................................................. 

</pre>

<b>Query to produce an ASCII-art image of the Julia set</b>

<pre>
-- ported from PostgreSQL version https://explainextended.com/2013/12/31/happy-new-year-5/
WITH    x(n) AS 
        ( 
        select -40
        UNION ALL
        select n+1 from x where n < 40
        ),
        q (r, i, rx, ix, g) AS
        (       
        SELECT  x + r::float * step, y + i::float * step,
                x + r::float * step, y + i::float * step,
                0 
        FROM    ( 
                SELECT  0.25 x, -0.55 y, 0.002 step, r, i
                FROM    (select n as r from x) 
                cross join 
                (select n as i from x)
                )
        UNION ALL
        SELECT  r, i,
                CASE WHEN (rx * rx + ix * ix) < 1E8 THEN 
                    pow((rx * rx + ix * ix), 0.75) * COS(1.5 * ATAN2(ix, rx)) END - 0.2,
                CASE WHEN (rx * rx + ix * ix) < 1E8 THEN 
                    pow((rx * rx + ix * ix), 0.75) * SIN(1.5 * ATAN2(ix, rx)) END,
                g + 1
        FROM    q
        WHERE   rx IS NOT NULL
                AND g < 99
        ),
        Zt (i, r, x) AS (
        SELECT i, r, SUBSTR(" .:-=+*#%@", (MAX(g) /10 +1)::int, 1) as x
        FROM q
        GROUP BY i, r
        order by r
        )
SELECT  
        sum(x::lvarchar) as x
        from Zt 
        group by i
        order by i;

x  ::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::: 
x  ::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::: 
x  ::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::: 
x  ::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::: 
x  ::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::: 
x  ::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::: 
x  ::::::::::::::::::::::::::::::::::------------------------::::::::::::::::::::::: 
x  :::::::::::::::::::::::::::-------------------------------------::::::::::::::::: 
x  ::::::::::::::::::::::----------------------------------------------::::::::::::: 
x  ::::::::::::::::::-----------------------------------------------------:::::::::: 
x  :::::::::::::::-----------------=======+*@@@@@@@@@@@@*+=====---------------:::::: 
x  ::::::::::::-------------====+@@@@@@@@@@@@%%@%@@@%%@@%@%@@@@@===--------------::: 
x  ::::::::::----------===+@@@@@@@@@%%@@%@@%%%%%@@@%%%%@@@@@@%@@@@@@+==------------- 
x  :::::::----------==+@@@@@%@@%@@@@%@@@@%%@@@@@%%@%@@@%@%%%@%%@@%@@@@@@===--------- 
x  :::::----------=+@@%@@@@%%@%%%%@%@@@%@%%@%@%@%%@%@%@%@%%@%%%@%%@@@@@@%@@+==------ 
x  :::---------==@@@@%@%%@@@@@%%@%@%@%@%#%%%@%%%%%%%%@%@%%%%@%@%%@@%@@@@@%@@@@+==--- 
x  :---------=+@@@%@%%@@%@%@#@#%%%%@%@#@@#@%@#@#@@#%%@#@#@@%@#%@%@@%@@%@%%%%%@@@@==- 
x  -------==@@@@%%%@%@%@@@@#%%%@#@%@%@%@@#@@@%@#@@#%@@%@#@@%%%#@%#@%@%@%%@@%@%@@%%@@ 
x  -----==@@@%@%@%@%@@@%@#@@%@@@%@%@@%%@@##%@%##@@##@@###@@#%@#@##@#%@@@%@%%%@%@%@@@ 
x  ---==@@@%@@%@%%@@%@##@#@@#@%@%##@@##%@##%@#%#%@##%@#%#@@#@@##@#%%#@%#@@@%@%%%@%@@ 
x  -==@@%%@@@%%%@%@##@#@##@@###@%##@%#@#@#@#%#@%#%#@#%#@%##%@@#%@#%@%@%#@#%@@%%@%%%% 
x  =@@@%%@%%%@%@%%@%@##@@#%@#@#%#%#%#@@%##@##%@@##%@##@@@##@@@#@@#@@%#@##%#@%#@@%%@% 
x  @%@%@%@@%@##@%@#%@%#@@@#%%@@##@@##@@@##@##@@@##@@##@@@##@@@#%#%@@%#@#%@%@##@%%%@% 
x  @@@@@%@%%@@%%#@@#%@#@@@##%@@##@@##@@@##@##@@@%#@@##@@@##@@####%@@#%%#@@%#@#%#%@@% 
x  @%@@%%@%%#@%%#@@@#@#%@@%#@@@%#@@##@@@%#@##@@@@#@@##@@@%#@%####@@@###@@@#%@##@@%#@ 
x  %%%@@%@@%@##@#@@@####%@%#@@@@#%@##@@@@#%##@@@@#%###@@@%####@%#@@%###@@@#@@#@@@#%@ 
x  @%@%@##%%@@#@#%@@%#%##%%#@@@@#####@@@@####@@@%#####@@@####@@@#%@####@@%###%@@%#@@ 
x  @@##%#@##@@@###@@%#%@####%@@@#####@@@%####@@@######@@@###@@@@####@##@@####@@@%%@% 
x  #@#@%#@@#@@@####@%#@@@####@@@######@@%####%@@###%##%@@##%@@@@###%@##@##%##@@@#%## 
x  @##@@%#@#%@@%#%##%#@@@@###@@%##@###@@######@%##@@###@%##@@@@@###@@####%@%#@@%##%@ 
x  @%#@@@#%##%@%#@%###@@@@@##%@###@@###@##@@##%###@@@#####%@@@@@##%@@###%@@%#@%##@@@ 
x  @@#@@@##%##%%#@@###%@@@@%##@##@@@@#####@@#####@@@@#####@@@@@%##@@%###@@@%####@@@@ 
x  #%%#@@%#%@####%@@###@@@@@#####@@@@#####@@%####@@@@@#*##@@@@@###@@###@@@@%###@@@@@ 
x  @###%@@#@@@####@@%##@@@@@#####@@@@%#*##@@%#*##@@@@@####@@@@@###@@##%@@@@%##%@@@@% 
x  @@@##%%#@@@@###@@@##%@@@@%#*#%@@@@@####@@@#*#%@@@@@####@@@@########@@@@@###@@@@@# 
x  @@@@####%@@@@###@@###@@@@@#*#%@@@@@####@@@#*#@@@@@@%###@@@%#*######@@@@@###@@@@## 
x  %@@@@###%@@@@%##%#####@@@@#*#@@@@@@%###@@@#*#@@@@@@%###@@@##*#####%@@@@@##%@@%### 
x  #@@@@@###@@@@@########%@@@###@@@@@@@#*#@@@#*#@@@@@@@#*#@@#######*#%@@@@%##@@##### 
x  ##@@@@%##@@@@@%#####*##%@@#*#@@@@@@@#*#@#%#*#@@@@@@%#*#%#####@%#*#@@@@@########## 
x  %##@@@@##%@@@@@#*########@#*#%@@@@@@#*#####*#@@@@@@%#*#####%@@@#*#@@@@##*####%@@# 
x  %###%@@###@@@@@####@%##*###*##@@@@@@#*##*##*#%@@@@@%#*#**#%@@@@#*#@@@%#**##%@@@@# 
x  ###########@@@@####@@@##**#*##@@@@@@#*******##@@@@@##***##@@@@@###%@%#####@@@@@%# 
x  #########*#%@@@####@@@@##****#@@@@@%#***##***#@@@@@#***##@@@@@@####%####%@@@@@@## 
x  ##%@@%###*##%@@####@@@@@##***#%@@@@##**###***#@@@@@#**##@@@@@@@########%@@@@@@@## 
x  ###@@@@%######@####@@@@@@##**##@@@@#***#@##**##@@@%#**#%@@@@@@@#**#*##%@@@@@@@%## 
x  ###@@@@@@%##*######@@@@@@@##**#@@@@#**##@@##**#@@@#**##@@@@@@@@#****#%@@@@@@@@### 
x  %##@@@@@@@@##*##*##@@@@@@@@#**##@@##**#@@@%#**##@%#**#%@@@@@@@@#***##@@@@@@@@%#** 
x  @###@@@@@@@@##****#@@@@@@@@##**#%@#**##@@@@##**#%#**##@@@@@@@@%#***#@@@@@@@@@##*# 
x  ####%@@@@@@@@##***#%@@@@@@@@#***###**#@@@@@@#***##**#%@@@@@@@@##**##@@@@@@@@##*## 
x  #####@@@@@@@@@##**##@@@@@@@@%#**##**##@@@@@@##******#@@@@@@@@@##**#@@@@@@@@#####@ 
x  ###*##@@@@@@@@%#**##@@@@@@@@@#******#%@@@@@@%#******#@@@@@@@@@#**##@@@@@@@#####@@ 
x  @#####%@@@@@@@@##**#@@@@@@@@@##*****#@@@@@@@@#*****##@@@@@@@@##**#@@@@@@@###*#%@@ 
x  @@%####%@@@@@@@@#**##@@@@@@@@%#*****#@@@@@@@@##****#%@@@@@@@@#***#@@@@@%##**##@@@ 
x  @@@%#####@@@@@@@##**#@@@@@@@@@#*****#@@@@@@@@%#****#@@@@@@@@##**##@@@%###***##### 
x  @@@@%##*##%@@@@@@#**##@@@@@@@@#****##@@@@@@@@@#****#@@@@@@@@#***#%#####******#### 
x  @@@@@##**####@@@@#***##@@@@@@@##***#%@@@@@@@@@#****#@@@@@@@##***####*********#### 
x  #%%#####***########***#%@@@@@@%#***#%@@@@@@@@@#****#@@@@@@##***********########## 
x  ######*********####****#@@@@@@@#***#@@@@@@@@@@##***#@@@@@%#*********######%%@@@@@ 
x  **#######**************##@@@@@@#***#@@@@@@@@@@%#***#@@@@%#********###%@@@@@@@@@@@ 
x  ###############*********##@@@@@#***#@@@@@@@@@@%#***#@@@%#*******###@@@@@@@@@@@@@@ 
x  #%@@@@@@@@@@@%####********#%@@@#***#@@@@@@@@@@%#***#@@##******###@@@@@@@@@@@@@@@@ 
x  @@@@@@@@@@@@@@@@%###*******##@%#***#%@@@@@@@@@%#***#%##*****###@@@@@@@@@@@@@@@@@@ 
x  @@@@@@@@@@@@@@@@@@@%##*******###***##@@@@@@@@@#*****#******##@@@@@@@@@@@@@@@@@@@@ 
x  @@@@@@@@@@@@@@@@@@@@@%##************#@@@@@@@@@#***********##@@@@@@@@@@@@@@@@@@@@@ 
x  @@@@@@@@@@@@@@@@@@@@@@@##***********#@@@@@@@@@#**********#%@@@@@@@@@@@@@@@@@@@@@@ 
x  @@@@@@@@@@@@@@@@@@@@@@@@@##*********#@@@@@@@@@#*********#@@@@@@@@@@@@@@@@@@@@@@@@ 
x  @@@@@@@@@@@@@@@@@@@@@@@@@@##********#%@@@@@@@@#********#@@@@@@@@@@@@@@@@@@@@@@@@@ 
x  @@@@@@@@@@@@@@@@@@@@@@@@@@@##********#@@@@@@@#********#@@@@@@@@@@@@@@@@@@@@@@@@@@ 
x  @@@@@@@@@@@@@@@@@@@@@@@@@@@@##*******#@@@@@@@#*******#%@@@@@@@@@@@@@@@@@@@@@@@@@@ 
x  @@@@@@@@@@@@@@@@@@@@@@@@@@@@@##******##@@@@@@#******##@@@@@@@@@@@@@@@@@@@@@@@@@@@ 
x  @@@@@@@@@@@@@@@@@@@@@@@@@@@@@@##******#@@@@@#*******#@@@@@@@@@@@@@@@@@@@@@@@@@@@@ 
x  @@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@#******#%@@@@#******#@@@@@@@@@@@@@@@@@@@@@@@@@@@@@ 
x  @@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@#******#@@@%#*****#%@@@@@@@@@@@@@@@@@@@@@@@@@@@@@ 
x  @@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@%#*****##@@#******#@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@ 
x  @@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@#******#@#******#@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@ 
x  @@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@#******##******#@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@ 
x  @@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@%#************#@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@ 
x  @@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@#************#@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@ 
x  @@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@#***********#@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@ 
x  @@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@#**********#@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@ 
x  @@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@#**********#@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@ 

</pre>

Thanks for reading!
