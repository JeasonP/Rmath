# 自学SQL刷题笔记

网站地址[SQLBolt](https://sqlbolt.com/lesson/select_queries_introduction)

## lesson 1

    找到所有电影的名称：
    1.SELECT title FROM movies;

    找到所有电影的导演：
    2.SELECT director FROM movies;

    找到所有电影的名称和导演
    3.SELECT director,title FROM movies;

    找到所有电影的名称和上映年份：
    4.SELECT year,title FROM movies;

    找到所有电影的所有信息：
    5.SELECT * FROM movies;

## lesson 2

    找到id为6的电影：
    1.SELECT * FROM movies where id='6';

    找到在2000-2010年间year上映的电影：
    2.SELECT * FROM movies where year between 2000 and 2010;

    找到不是在2000-2010年间year上映的电影：
    3.SELECT * FROM movies where year not between 2000 and 2010;

    找到头5部电影：
    4.SELECT * FROM movies where id in (1,2,3,4,5);

## lesson 3

    找到所有Toy Story系列电影：
    1.SELECT * FROM movies where title like 'toy story%';

    找到所有John Lasseter导演的电影：
    2.SELECT * FROM movies where director like 'john lasseter';

    找到所有不是John Lasseter导演的电影：
    3.SELECT * FROM movies where director not like 'john lasseter';

    找到所有电影名为 "WALL-" 开头的电影：
    4.SELECT * FROM movies where title like 'wall-_';

## lesson 4

    按导演名排重列出所有电影(只显示导演)，并按导演名正序排列：
    1.SELECT distinct director FROM movies order by director desc;

    列出按上映年份最新上线的4部电影：
    2.SELECT * FROM movies order by year desc limit 4;

    按电影名字母序升序排列，列出前5部电影：
    3.SELECT * FROM movies order by title asc limit 5;

    按电影名字母序升序排列，列出上一题之后的5部电影：
    4.SELECT * FROM movies order by title asc limit 5 offset 5;

## lesson 5

    列出所有加拿大人的Canadian信息(包括所有字段)：
    1.SELECT city,population FROM north_american_cities where country like 'canada';

    列出所有在Chicago西部的城市，从西到东排序(包括所有字段)：
    2.SELECT * FROM north_american_cities where country like 'united states' order by latitude desc;

    List all the cities west of Chicago, ordered from west to east:
    3.SELECT * FROM north_american_cities where longitude<-87.629768 order by longitude asc limit 6;

    用人口数population排序,列出墨西哥Mexico最大的2个城市(包括所有字段):
    4.SELECT * FROM north_american_cities where country like 'mexico' order by population desc limit 2;

    列出美国United States人口3-4位的两个城市和他们的人口(包括所有字段):
    5.SELECT * FROM north_american_cities where country like 'united states' order by population desc limit 2 offset 2;

## lesson 6

    找到所有电影的国内Domestic_sales和国际销售额:
    1.SELECT movies.*,boxoffice.* FROM movies,boxoffice where movies.id=boxoffice.movie_id;
    &&
    SELECT movies.*,boxoffice.* FROM movies inner join boxoffice on movies.id=boxoffice.movie_id;
    &&
    SELECT * FROM movies inner join boxoffice on movies.id=boxoffice.movie_id;
    &&
    SELECT *,* FROM movies inner join boxoffice on movies.id=boxoffice.movie_id;

    找到所有国际销售额比国内销售大的电影:
    2.SELECT movies.*,boxoffice.* FROM movies,boxoffice where movies.id=boxoffice.movie_id and international_sales>Domestic_sales;
    &&
    SELECT *,* FROM movies inner join boxoffice on movies.id=boxoffice.movie_id where international_sales>domestic_sales;

    找出所有电影按市场占有率rating倒序排列:
    3.SELECT movies.*,boxoffice.* FROM movies,boxoffice where movies.id=boxoffice.movie_id order by rating desc;
    &&
    SELECT *,* FROM movies inner join boxoffice on movies.id=boxoffice.movie_id order by boxoffice.rating desc;
    &&
    SELECT * FROM movies inner join boxoffice on movies.id=boxoffice.movie_id order by boxoffice.rating desc;

    每部电影按国际销售额比较,排名最靠前的导演是谁,国际销量多少:
    4.SELECT movies.director,boxoffice.international_sales FROM movies,boxoffice where movies.id=boxoffice.movie_id order by international_sales desc limit 1;

## lesson 7

    找到所有有雇员的办公室(buildings)名字:
    1.select distinct building from employees left join buildings where building is not null;

    找到所有办公室里的所有角色（包含没有雇员的）,并做唯一输出(DISTINCT):
    2.select distinct buildings.building_name,role from buildings left join employees on buildings.building_name=employees.building order by building_name;      

    找到所有有雇员的办公室(buildings)和对应的容量:
    3.select distinct building,capacity from employees left join buildings on employees.building=buildings.building_name
    where building is not null;

## lesson 8

    找到雇员里还没有分配办公室的(列出名字和角色就可以):
    1.select role,name from employees where building is null;

    找到还没有雇员的办公室:
    2.select distinct buildings.building_name from buildings left join employees on employees.building=buildings.building_name
    where building is null;

## lesson 9

    列出所有的电影ID,名字和销售总额(以百万美元为单位计算) :
    1.SELECT movies.id,title,(domestic_sales+international_sales)/1000000 FROM movies left join boxoffice on movies.id=boxoffice.movie_id;

    列出所有的电影ID,名字和市场指数(Rating的10倍为市场指数):
    2.SELECT movies.id,title,rating*10 FROM movies left join boxoffice on movies.id=boxoffice.movie_id;

    列出所有偶数年份的电影，需要电影ID,名字和年份:
    3.SELECT movies.id,title,year FROM movies where year%2=0;

    John Lasseter导演的每部电影每分钟值多少钱,告诉我最高的3个电影名和价值就可以:
    4.SELECT title, (Domestic_sales+International_sales)/length_minutes as per_min_price
    FROM movies left join boxoffice
    on movies.id=boxoffice.movie_id 
    where director like 'john lasseter'
    order by (Domestic_sales+International_sales)/length_minutes desc
    limit 3;

## lesson 10

    找出就职年份最高的雇员(列出雇员名字+年份）:
    1.SELECT name,max(years_employed) FROM employees;
    
    按角色(Role)统计一下每个角色的平均就职年份
    2.SELECT role,avg(years_employed) FROM employees group by role;

    按办公室名字总计一下就职年份总和:
    3.SELECT building,sum(years_employed) FROM employees group by building;

    每栋办公室按人数排名,不要统计无办公室的雇员:
    4.SELECT building,count(building) 
    FROM employees 
    where building is not null 
    group by building;

## lesson 11

    统计一下Artist角色的雇员数量:
    1.SELECT count(role) FROM employees where role like 'artist';

    按角色统计一下每个角色的雇员数量:
    2.SELECT count(role) ,role FROM employees group by role;

    算出Engineer角色的就职年份总计:
    3.SELECT sum(years_employed) FROM employees where role like 'engineer';

    按角色分组算出每个角色按有办公室和没办公室的统计人数(列出角色，数量，有无办公室,注意一个角色如果部分有办公室，部分没有需分开统计）:
    4.SELECT count(name) ,role ,case when building is not null then '1'
    else '0' end as bn
    FROM employees 
    where 1
    group by role , bn;

## lesson 12

    统计出每一个导演的电影数量（列出导演名字和数量）:
    1.select director,count(*) from movies  group by director;

    统计一下每个导演的销售总额(列出导演名字和销售总额):
    2.select director,sum(Domestic_sales+International_sales) 
    from movies left 
    join boxoffice 
    on movies.id=boxoffice.movie_id 
    group by director;

    按导演分组计算销售总额,求出平均销售额冠军（统计结果过滤掉只有单部电影的导演，列出导演名，总销量，电影数量，平均销量):
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

    找出每部电影和单部电影销售冠军之间的销售差，列出电影名，销售额差额:
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
