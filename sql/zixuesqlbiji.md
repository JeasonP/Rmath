# 自学SQL刷题笔记

网站地址[SQLBolt](https://sqlbolt.com/lesson/select_queries_introduction)

## lesson 1

    1.SELECT title FROM movies;

    2.SELECT director FROM movies;

    3.SELECT director,title FROM movies;

    4.SELECT year,title FROM movies;

    5.SELECT * FROM movies;

## lesson 2

    1.SELECT * FROM movies where id='6';

    2.SELECT * FROM movies where year between 2000 and 2010;

    3.SELECT * FROM movies where year not between 2000 and 2010;

    4.SELECT * FROM movies where id in (1,2,3,4,5);

## lesson 3

    1.SELECT * FROM movies where title like 'toy story%';

    2.SELECT * FROM movies where director like 'john lasseter';

    3.SELECT * FROM movies where director not like 'john lasseter';

    4.SELECT * FROM movies where title like 'wall-_';

## lesson 4

    1.SELECT distinct director FROM movies order by director desc;

    2.SELECT * FROM movies order by year desc limit 4;

    3.SELECT * FROM movies order by title asc limit 5;

    4.SELECT * FROM movies order by title asc limit 5 offset 5;

## lesson 5

    1.SELECT city,population FROM north_american_cities where country like 'canada';

    2.SELECT * FROM north_american_cities where country like 'united states' order by latitude desc;

    3.SELECT * FROM north_american_cities where longitude<-87.629768 order by longitude asc limit 6;

    4.SELECT * FROM north_american_cities where country like 'mexico' order by population desc limit 2;

    5.SELECT * FROM north_american_cities where country like 'united states' order by population desc limit 2 offset 2;

## lesson 6

    1.SELECT movies.*,boxoffice.* FROM movies,boxoffice where movies.id=boxoffice.movie_id;
    &&
    SELECT movies.*,boxoffice.* FROM movies inner join boxoffice on movies.id=boxoffice.movie_id;
    &&
    SELECT * FROM movies inner join boxoffice on movies.id=boxoffice.movie_id;
    &&
    SELECT *,* FROM movies inner join boxoffice on movies.id=boxoffice.movie_id;

    2.SELECT movies.*,boxoffice.* FROM movies,boxoffice where movies.id=boxoffice.movie_id and international_sales>Domestic_sales;
    &&
    SELECT *,* FROM movies inner join boxoffice on movies.id=boxoffice.movie_id where international_sales>domestic_sales;

    3.SELECT movies.*,boxoffice.* FROM movies,boxoffice where movies.id=boxoffice.movie_id order by rating desc;
    &&
    SELECT *,* FROM movies inner join boxoffice on movies.id=boxoffice.movie_id order by boxoffice.rating desc;
    &&
    SELECT * FROM movies inner join boxoffice on movies.id=boxoffice.movie_id order by boxoffice.rating desc;

    4.SELECT movies.director,boxoffice.international_sales FROM movies,boxoffice where movies.id=boxoffice.movie_id order by international_sales desc limit 1;

## lesson 7

    1.select distinct building from employees left join buildings where building is not null;

    2.select distinct buildings.building_name,role from buildings left join employees on buildings.building_name=employees.building order by building_name;      

    3.select distinct building,capacity from employees left join buildings on employees.building=buildings.building_name
    where building is not null;

## lesson 8

    1.select role,name from employees where building is null;

    2.select distinct buildings.building_name from buildings left join employees on employees.building=buildings.building_name
    where building is null;

## lesson 9

    1.SELECT movies.id,title,(domestic_sales+international_sales)/1000000 FROM movies left join boxoffice on movies.id=boxoffice.movie_id;

    2.SELECT movies.id,title,rating*10 FROM movies left join boxoffice on movies.id=boxoffice.movie_id;

    3.SELECT movies.id,title,year FROM movies where year%2=0;

    4.SELECT title, (Domestic_sales+International_sales)/length_minutes as per_min_price
    FROM movies left join boxoffice
    on movies.id=boxoffice.movie_id 
    where director like 'john lasseter'
    order by (Domestic_sales+International_sales)/length_minutes desc
    limit 3;

## lesson 10

    1.SELECT name,max(years_employed) FROM employees;
    
    2.SELECT role,avg(years_employed) FROM employees group by role;

    3.SELECT building,sum(years_employed) FROM employees group by building;

    4.SELECT building,count(building) 
    FROM employees 
    where building is not null 
    group by building;

## lesson 11

    1.SELECT count(role) FROM employees where role like 'artist';

    2.SELECT count(role) ,role FROM employees group by role;

    3.SELECT sum(years_employed) FROM employees where role like 'engineer';

    4.SELECT count(name) ,role ,case when building is not null then '1'
    else '0' end as bn
    FROM employees 
    where 1
    group by role , bn;

## lesson 12

    1.select director,count(*) from movies  group by director;

    2.select director,sum(Domestic_sales+International_sales) 
    from movies left 
    join boxoffice 
    on movies.id=boxoffice.movie_id 
    group by director;

    3.select 
    sum(Domestic_sales+International_sales) as sum_sale,
    director,
    count(director),
    avg(Domestic_sales+International_sales) as avg_sale
        from movies 
    left join boxoffice 
        on movies.id=boxoffice.movie_id 
    group by director
    having count(director)>1
    order by avg_sale desc
    limit 1;

    4.select title,
    (select max(Domestic_sales+International_sales) from Boxoffice)-(Domestic_sales+International_sales) 
    from movies
    left join boxoffice
    on movies.id=boxoffice.movie_id;

### 查询执行顺序

    1. FROM 和 JOINs
    FROM 或 JOIN会第一个执行，确定一个整体的数据范围. 如果要JOIN不同表，可能会生成一个临时Table来用于 下面的过程。总之第一步可以简单理解为确定一个数据源表（含临时表)

    2. WHERE
    我们确定了数据来源 WHERE 语句就将在这个数据源中按要求进行数据筛选，并丢弃不符合要求的数据行，所有的筛选col属性 只能来自FROM圈定的表. AS别名还不能在这个阶段使用，因为可能别名是一个还没执行的表达式

    3. GROUP BY
    如果你用了 GROUP BY 分组，那GROUP BY 将对之前的数据进行分组，统计等，并将是结果集缩小为分组数.这意味着 其他的数据在分组后丢弃.

    4. HAVING
    如果你用了 GROUP BY 分组, HAVING 会在分组完成后对结果集再次筛选。AS别名也不能在这个阶段使用.

    5. SELECT
    确定结果之后，SELECT用来对结果col简单筛选或计算，决定输出什么数据.

    6. DISTINCT
    如果数据行有重复DISTINCT 将负责排重.

    7. ORDER BY
    在结果集确定的情况下，ORDER BY 对结果做排序。因为SELECT中的表达式已经执行完了。此时可以用AS别名.

    8. LIMIT / OFFSET
    最后 LIMIT 和 OFFSET 从排序的结果中截取部分数据.

    结论
    不是每一个SQL语句都要用到所有的句法，但灵活运用以上的句法组合和深刻理解SQL执行原理将能在SQL层面更好的解决数据问题，而不用把问题 都抛给程序逻辑.
