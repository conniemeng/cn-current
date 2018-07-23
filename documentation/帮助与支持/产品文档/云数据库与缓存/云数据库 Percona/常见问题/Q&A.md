# Q&A

1. 
Q：Percona 相对于 MySQL 有何优势？
A：Percona 相对于 MySQL 提供了更丰富的服务性能诊断和更多的功能，也做了性能优化，具体详见 [官方文档](https://www.percona.com/software/mysql-database/percona-server/feature-comparison)。
1. 
Q：目前云数据库支持数据库类型？
A：目前支持数据库类型为 Percona 5.7，后期会支持更多的数据库类型。
1. 
Q：根据备份或时间点创建数据库时，为什么不用输入用户名和密码？
A：根据备份或时间点创建的新数据库会沿用备份源数据库的用户名和密码，暂不支持创建时用户手动输入。
1. 
Q：根据备份创建时，为什么我的可选配置显示只显示一部分？
A：用户在根据备份创建时，只能选择大于当前备份实际大小的配置。
1. 
Q：现在自动备份的保存多少天啊？
A：目前自动备份至少为您保留7天。
1. 
Q：云数据库支持外网访问么？
A：目前云数据库只支持通过子网访问。
1. 
Q：云数据库的库名称不支持哪些关键字？
库名称不支持mysql、information_schema、performance_schema和sys；同时也不支持以下关键字：
percona, admin, aurora, replicator, xtrabak, root, mysql, test, eagleye, information_schema, guest, add, analyze, asc, between, blob, call, change, check, condition, continue, cross, current_timestamp, database, day_microsecond, dec, default, desc, distinct, double, each, enclosed, exit, fetch, float8, foreign, goto, having, hour_minute, ignore, infile, insensitiv, int1, int4, interval, iterate, keys, leading, like, lines, localtimestamp, longblob, low_priority, mediumint, minute_microsecond, modifies, no_write_to_binlog, on, optionally, out, precision, purge, read, references, rename, require, revoke, schema, select, set, spatial, sqlexception, sql_big_result, ssl, table, tinyblob, to, true, unique, update, using, utc_timestamp, varchar, when, with, xor, all, and, asensitive, bigint, both, cascade, char, collate, connection, convert, current_date, current_user, databases, day_minute, decimal, delayed, describe, distinctrow, drop, else, escaped, explain, float, for, from, grant, high_priority, hour_second, in, inner, insert, int2, int8, into, join, kill, leave, limit, load, lock, longtext, match, mediumtext, minute_second, natural, null, optimize, or, outer, primary, raid0, reads, regexp, repeat, restrict, right, schemas, sensitive, show, specific, sqlstate, sql_calc_found_rows, starting, terminated, tinyint, trailing, undo, unlock, usage, utc_date, values, varcharacter, where, write, year_month, alter, as, before, binary, by, case, character, column, constraint, create, current_time, cursor, day_hour, day_second, declare, delete, deterministic, div, dual, elseif, exists, false, float4, force, fulltext, group, hour_microsecond, if, index, inout, int, int3, integer, is, key, label, left, linear, localtime, long, loop, mediumblob, middleint, mod, not, numeric, option, order, outfile, procedure, range, real, release, replace, return, rlike, second_microsecond, separator, smallint, sql, sqlwarning, sql_small_result, straight_join, then, tinytext, trigger, union, unsigned, use, utc_time, varbinary, varying, while, x509, zerofill, jcloud_yunding_db_push, jcloudv_push_rw, jcloudv_push_ro, jddb_percona
1. 
Q：云数据库的用户（账号）名称不支持哪些关键字？
A：用户（账号）名称不支持 root、admin、os_admin,、 replicater、monitor；同时也不支持以下关键字：
percona, admin, aurora, replicator, xtrabak, root, mysql, test, eagleye, information_schema, guest, add, analyze, asc, between, blob, call, change, check, condition, continue, cross, current_timestamp, database, day_microsecond, dec, default, desc, distinct, double, each, enclosed, exit, fetch, float8, foreign, goto, having, hour_minute, ignore, infile, insensitiv, int1, int4, interval, iterate, keys, leading, like, lines, localtimestamp, longblob, low_priority, mediumint, minute_microsecond, modifies, no_write_to_binlog, on, optionally, out, precision, purge, read, references, rename, require, revoke, schema, select, set, spatial, sqlexception, sql_big_result, ssl, table, tinyblob, to, true, unique, update, using, utc_timestamp, varchar, when, with, xor, all, and, asensitive, bigint, both, cascade, char, collate, connection, convert, current_date, current_user, databases, day_minute, decimal, delayed, describe, distinctrow, drop, else, escaped, explain, float, for, from, grant, high_priority, hour_second, in, inner, insert, int2, int8, into, join, kill, leave, limit, load, lock, longtext, match, mediumtext, minute_second, natural, null, optimize, or, outer, primary, raid0, reads, regexp, repeat, restrict, right, schemas, sensitive, show, specific, sqlstate, sql_calc_found_rows, starting, terminated, tinyint, trailing, undo, unlock, usage, utc_date, values, varcharacter, where, write, year_month, alter, as, before, binary, by, case, character, column, constraint, create, current_time, cursor, day_hour, day_second, declare, delete, deterministic, div, dual, elseif, exists, false, float4, force, fulltext, group, hour_microsecond, if, index, inout, int, int3, integer, is, key, label, left, linear, localtime, long, loop, mediumblob, middleint, mod, not, numeric, option, order, outfile, procedure, range, real, release, replace, return, rlike, second_microsecond, separator, smallint, sql, sqlwarning, sql_small_result, straight_join, then, tinytext, trigger, union, unsigned, use, utc_time, varbinary, varying, while, x509, zerofill, jcloud_yunding_db_push, jcloudv_push_rw, jcloudv_push_ro, jddbaclholder
1. 
Q：如何修改云数据库参数和字符集？
A：目前京东云暂不支持用户自定义修改参数和字符集，您可以通过提交工单的方式将您的需求反馈给京东云的工程师，由工程师协助您进行修改。