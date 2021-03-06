# Lintcode中SQL刷题笔记

## 2092 · 查询授课教师编号

请编写 SQL 语句，查询课程表 courses 中不重复的开课教师编号 teacher_id 。

    SELECT distinct(teacher_id) from courses; 

## 2081 · 向表中插入当前的日期

请编写 SQL 语句，向记录表 records 中插入当前的日期。

    INSERT into records
    VALUES(curdate());

## 2046 · 查询课程创建日期按 ‘年-月-日 时：分：秒’ 显示

查询 courses 表，查询课程创建时间，按照 ’年-月-日 时：分：秒’ 的格式返回结果，返回列名显示为 DATE_FORMAT。

    SELECT DATE_FORMAT(`created_at`, '%Y-%m-%d %H:%i:%S') AS `DATE_FORMAT`
    FROM `courses`;

## 2043 · 查询在第一季度创建的课程

从课程表 courses 中查询第一季度（1月、2月、3月）创建的课程。

    select name, created_at
    from courses
    where month(created_at) in (1, 2, 3)

## 2042 · 查询课程表中所有的课程名和创建日期中的年份和月份

题目描述：请编写 SQL 语句，查询课程表 courses 所有课程中的课程名（name）和创建日期中的年份（别名：year）和月份（ 别名：month）。

    select name, year(created_at) as year, month(created_at) as month from courses;

## 2041 · 查询指定教师授课的课程信息

请编写 SQL 语句，查询课程表 courses 中教师 id （teacher_id）为 1、2 或 3 的课程名称、教师 id 和课程创建时间，并将结果集按教师 id 升序排列，如果教师 id 相同，则按照课程创建时间降序排列。

    select name, teacher_id, created_at
    from courses
    where teacher_id = 1 or teacher_id = 2 or teacher_id = 3
    order by teacher_id, created_at desc;

## 2040 · 查询教师 id 不为 3 且人数大于 800 的课程

题目要求查询课程表 courses 中，教师 id teacher_id 不为 3，且学生人数 student_count 超过 800 的所有课程，最后返回满足条件的课程的所有信息。

    select id, name, student_count, created_at, teacher_id
    from courses
    where teacher_id != 3 and student_count > 800;

## 2039 · 查询课程表中课程的创建日期

请编写 SQL 语句，从课程表 courses 中查询课程的名字 name 和课程创建时间 created_at，从课程创建时间 created_at 中提取出创建课程的日期，用 created_date 作为结果集列名。

    select name, date_format(created_at, '%Y-%m-%d') as created_date
    from courses;

## 2037 · 查询 2020 年 8 月前的课程名和课程日期

请编写 SQL 语句，从课程表 courses 中查询 2020 年 8 月前的课程名和创建日期，并为创建日期的列名起别名为 created_date (日期指 created_at 中不包括具体时间的部分)。

    select name, date_format(created_at, '%Y-%m-%d') as created_date
    from courses
    where created_at < '2020-08-01';

## 2036 · 计算课程表中所有课程开课日期与指定日期的月数差

请编写 SQL 语句，查询 courses 表，计算课程创建时间与 '2020-04-22' 的月数差，返回列名显示为 MonthDiff。

    select timestampdiff(month, created_at, '2020-04-22') as MonthDiff from courses;

## 2035 · 计算课程表中课程创建日期与指定日期相差的年数

请编写 SQL 语句，查询 courses 表，计算课程表中创建课程时间（created_at）与 2021 年 4 月 1 日的年数差，结果课程名称列显示为 courses_name ，创建课程时间显示为 courses_created_at ，年数差列名显示为 year_diff 。

    SELECT `name` AS `courses_name` ,`created_at` AS `courses_created_at`,TIMESTAMPDIFF(YEAR, `created_at`, '2021-04-01') AS `year_diff` 
    FROM `courses`;

## 2032 · 将课程创建日期均提前一天

请编写 SQL 语句，修改 courses 表中课程的课程创建日期，将课程创建日期均提前一天，最后返回课程 id 、课程名称 name 及修改后的开课日期，修改后的课程创建日期命名为 new_created 。

    SELECT `id`, `name`, DATE_SUB(`created_at`, INTERVAL 1 DAY) AS `new_created`
    FROM `courses`;

## 2030 · 查询所有课程创建时间的小时

请编写 SQL 语句，从课程表 courses 中查询所有课程的课程名称（ name ）和课程创建时间（ created_at ）的小时数，将提取小时数的列名起别名为 created_hour。

    select name, hour(created_at) as created_hour
    from courses;

## 2029 · 计算 2019 年 03 月 26 日到课程创建时间的天数

请编写 SQL 语句，查询 courses 表，计算从 2019 年 03 月 26 日到创建时间（created_at）相差的天数，结果列名以 date_diff 显示 。

    select datediff(created_at, '2019-03-26') as date_diff
    from courses;

## 2028 · 将课程创建日期均推迟一天

请编写 SQL 语句，修改 courses 表中课程的课程创建日期，将课程创建日期均推迟一天，最后返回课程名称 name 及修改后的课程创建时间，修改后的课程创建时间命名为 new_created 。

    select name, date_add(created_at, interval 1 day) as new_created
    from courses;

## 2027 · 查询课程创建日期按‘年 月’显示

请编写 SQL 语句，查询 courses 表，查询课程创建时间，按照’年 月‘的格式返回结果，返回列名显示为 DATE_FORMAT。

    select date_format(created_at, '%Y %m') as DATE_FORMAT from courses;

## 2026 · 向表中插入当前时间（精确到毫秒）

请编写 SQL 语句，向记录表 records 中插入当前的时间（精确到毫秒）。

表定义: records (记录表)

    INSERT INTO `records` 
    -- 值为当前时间
    VALUES (NOW(3));

## 2025 · 查询课程表中的课程创建时间

题目描述：请编写 SQL 语句，查询课程表中课程的创建时间，以 ‘时:分:秒’ 格式输出，最后返回的列名为 created_at 。

    select date_format(created_at, '%H:%i:%s') as created_at from courses;

## 2024 · 查询所有课程表的课程名和创建日期的年份

请编写 SQL 语句，从课程表 courses 中查询课程的名字和创建年份，并为 created_at 起别名为 created_year。

    select name, year(created_at) as created_year from courses;

## 2023 · 计算 2018 年 01 月 13 日到课程创建时间的天数

请编写 SQL 语句，查询 courses 表，计算从 2018 年 01 月 13 日到创建课程时间（created at）相差天数，结果列名请以 date_diff 显示。

    select timestampdiff(day,'2018-01-13',created_at) as date_diff from courses;

## 2022 · 将课程创建日期均推迟一年

请编写 SQL 语句，修改课程表 courses 中课程的课程创建日期，将课程创建日期均往后推迟一年，最后返回课程名称 name 及修改后的课程创建日期，修改后的课程创建日期命名为 new_created 。

    SELECT name,date_add(created_at,interval 1 year) as new_created from courses;

## 2021 · 向教师表指定的列插入教师信息

请编写 SQL 语句，向教师表 teachers 插入一条新的教师记录，该记录指定列的字段内容如下：

| name | email | age | country |
| ---- | ---- | ---- | ---- |
| XiaoFu | XiaoFu@lintcode.com | 20 | CN |

    insert into teachers(name , email , age , country) 
    values('XiaoFu','XiaoFu@lintcode.com' , 20 , 'CN');

## 2020 · 更新选择人工智能的学生人数

请编写 SQL 语句，将课程表 courses 中人工智能课 (Artificial Intelligence) 的学生人数修改为 500 人。

    update courses
    set student_count = 500
    where name = 'Artificial Intelligence';

## 2018 · 向课程表指定的列插入 'Flash Sale' 课程信息

请编写 SQL 语句，向课程表 courses 插入一条新的课程记录，该记录指定列的字段内容如下：

|name |student_count| created_at| teacher_id|
|----|----|----|----|
|Flash Sale| 100 |2018-01-01| 5|

    insert into courses(name, student_count, created_at, teacher_id)
    values('Flash Sale', 100, '2018-01-01', 5);

## 1998 · 统计在 2020 年 1 月到 5 月的课程

请编写 SQL 语句，统计课程表 courses 中 2020 年 1 月到 5 月之间的课程数量，最后返回统计值，结果列名显示为 course_count 。

    select count(id)
    from courses
    where created_at between '2020-01-01' and '2020-05-31';

## 1994 · 更新所有课程信息

请编写 SQL 语句，将课程表 courses 中所有课程的学生人数都改为 0。

    update courses
    set student_count = 0;

## 1918 · 第二高的球员的身高

编写一个 SQL 语句，获取球员 (players) 表中第二高的身高 (height)

    SELECT MAX(height) AS second_height
    FROM players
    WHERE height < (
        SELECT MAX(height)
        FROM players
    );

## 1922 · 删除重复的姓名

编写一个 SQL 语句，来删除 contacts 表中所有重复的姓名，重复的姓名里只保留 id 最小的那个。

    delete from contacts 
    where id not in (
    select * from (
    (select min(id) from contacts group by name))tblTmp);

## 1928 · 网课上课情况分析 I

online_class_situations 表展示了一些同学上网课的行为活动。
每行数据记录了一名同学在退出网课之前，当天使用同一台设备登录课程后听过的课程数目（可能是0个）。
写一条 SQL 语句，查询每位同学第一次登录平台听课的日期。

    select student_id student_id, min(date) earliest_course_date
    from online_class_situations
    where course_number > 0
    group by student_id;

## 1929 · 网课上课情况分析 II

online_class_situations 表展示了一些同学上网课的行为活动。
每行数据记录了一名同学在退出网课之前，当天使用同一台设备登录课程后听过的课程数目（可能是0个）。
写一条 SQL 语句，查询每位同学第一次登录平台听课的设备ID (device_id)。

    SELECT DISTINCT
        student_id,
        min(device_id)  AS device_id
    FROM 
        online_class_situations
    WHERE
        course_number > 0
    GROUP BY
        student_id

## 1913 · 查询学生学籍信息（多表连接）

编写一个 SQL 语句，满足条件：无论 students 是否有学籍 (enrollments) 信息，学生都需要根据如下两个表提供以下信息：

* student_name,
* phone,
* hometown,
* address
  
    select s.student_name, s.phone, e.hometown, e.address
    from students as s
    left join enrollments as e on s.id = e.student_id;

## 一个表中有，另一个表中没有的

    select a.* from a 
    left join b 
    on (a.id=b.id) 
    where b.id is NULL

## 简历投递 ⅱ

students 表存储了所有学生的信息，包括学生 id 和学生姓名 name companies 表存储了所有公司的信息，包括公司 id 、公司名称 name 和 公司地址 address records 表存储了所有的简历投递数据，包括学生 id (student_id) 和 公司 id (company_id) 请编写 SQL 语句，查询接收简历最多的公司名称和地址。

    select name, address 
    from 
        companies 
    where id in 
        (select company_id 
            from 
                records 
            group by 
                company_id 
            having count(student_id)
            =
            (select max(c.count_c) 
            from  
                (select count(student_id) as count_c 
                from 
                    records 
                group by 
                    company_id) c));
凡是在group by后面出现的字段，必须同时在select后面出现；凡是在select后面出现的、同时未在聚合函数中出现的字段，必须同时出现在group by后面，检查sql是否符合上述法则，当然，出现group by时，如果select后边有主键，group by逐渐也是可以的，只是此时group by好像也没起到什么作用

## 挂科最多的同学 II

exams 表中存放着同学们的考试记录 请用 SQL 语句，找到挂科数最多的同学所对应的 student_id

    SELECT student_id from( SELECT student_id,count(id) as c from exams WHERE is_pass = 0 GROUP BY student_id HAVING c= (SELECT max(c) from (SELECT student_id,count(id) as c from exams WHERE is_pass = 0 GROUP BY student_id ) as b) ) as t

1946 · 俱乐部年度比赛得分排名 II

rankings 表记录了某俱乐部年度比赛的排名及得分信息，包括项目 id (category_id)，年份 (year)，排名 (rank) 以及分数 (score) categories 表记录了项目的名称 (name) 请编写 SQL 语句，查询 rankings 表和 categories 表中所有项目对应的项目名称 (name)、该项目平均分数 (average_score) 平均分数需要保留两位小数

    select t2.name,round(AVG(t1.score),2) average_score
    from 
    rankings t1 inner join categories t2 on t1.category_id = t2.id 
    group by t2.name
    order by average_score desc;

## 1943 · 寻找特定身高的同学

student_heights 表记录着同学们的身高，其中包括很多重复的身高 请编写一个 SQL 语句，在只出现过一次的身高中，找出最高的身高

    select max(a) height from (
    select max(height) a from student_heights
    group by height
    having count(height) = 1 
    ) v;

## 1942 · 相距最近的两棵树苗

某处新种植有一些距离不等的树苗，已知这些树苗和一个大的浇水桶都在一条直线上 sapling_distances 表存储了一些树苗到浇水桶的距离 (distance) 请编写一个 SQL 语句，找到最近的两棵树苗的距离 (shortest_distance)。

    select MIN(s1.distance - s2.distance) as shortest_distance from 
    sapling_distances as s1 inner join sapling_distances as s2 
    where/on s1.distance >s2.distance having shortest_distance !="None";
