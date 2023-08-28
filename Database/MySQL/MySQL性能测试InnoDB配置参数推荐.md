```
[mysqld]

basedir = /mysql/base
datadir = /mysql/base/data

# binlog
log-bin = /mysql/binlog/binlog
log_error = /data/mysql_data/log/mysql.err # 错误日志，便于定位分析
binlog_error_action = ABORT_SERVER # 默认值，控制当binlog写入/flush或者同步时出问题如何处理。ABORT_SERVER：当binlog出现问题的时候master无法写入并且自杀宕机。
binlog_format = row # 默认值，记录所有执行语句，会产生大量的日志文件。
binlog_checksum = NONE # 非默认值，减少CPU消耗（5.6开始默认值为crc32，之前版本默认值为none），组复制必须配置为NONE。
binlog_rows_query_log_events = 1 # 非默认值，与binlog_format=row结合使用。
log_slave_updates = 1 # 非默认值。A -> B -> C 有效？？
master_info_repository = TABLE
max_binlog_size = 250M
relay_log_info_repository = TABLE
relay_log_recovery = 1 # 默认开启
sync_binlog = 1 # 非默认值，每提交一次，存储引擎调用文件系统sync进行缓存刷新，安全性高，性能低。
sync_relay_log = 1 # 非默认值，slave的I/O线程每次接收到master发送过来的binlog日志都要写入系统缓冲区，然后刷入relay log中继日志里，安全性高，性能低。
log_bin_trust_function_creators = 1 # 非默认值，影响安全性，测试环境开启。

# gtid
gtid_mode = ON
enforce_gtid_consistency = 1
binlog_gtid_simple_recovery = 1

# innodb engine
innodb_log_group_home_dir = /mysql/log
innodb_undo_directory = /mysql/undo
innodb_data_file_path = ibdata1:2000M:autoextend # 对预置数据阶段性能有微弱影响，不影响稳定性能
innodb_temp_data_file_path = ibtmp1:12M:autoextend:max:50G
innodb_data_home_dir = /data/mysql_data/data/
innodb_flush_log_at_trx_commit = 1 # 全量覆盖使用参数1，跟sync_binlog=1结合，使数据尽量落盘；
innodb_doublewrite = 0 # 非默认值。直接写文件。默认开启，buffer和数据文件双写
innodb_flush_method = O_DIRECT #默认为fsync，可以考虑修改为O_DIRECT
innodb_buffer_pool_size = 32G # 通常建议为内存的一半
innodb_buffer_pool_instances=16 # 非默认值，默认值为8或1 if innodb_buffer_pool_size < 1GB。调大有助于提高并发性能，建议设置为innodb_buffer_pool_size 的公约数
innodb_io_capacity = 8192
innodb_lru_scan_depth = 8192 # 默认1024
innodb_log_file_size = 32GB # 测试环境负载大，避免频繁产生新的日志文件
innodb_log_files_in_group = 16
innodb_max_dirty_pages_pct = 75 # 默认90，想要更频繁的产生主机刷盘数据，可适当调小
innodb_purge_threads = 32 # 最大值： InnoDB 引擎将用于从其数据库中清除删除标记记录的线程数。可适当调整为4
innodb_read_io_threads = 64 # 最大值：InnoDB 引擎读IO请求线程数，建议CPU核数整数倍。可适当调整为16
innodb_write_io_threads = 64 # 最大值。可适当调整为16
innodb_open_files = 4096

# cache 调优过程中需要关注
key_buffer_size = 16M
tmp_table_size = 64M
max_heap_table_size = 64M
max_connections = 2000
max_connect_errors = 1000
thread_cache_size = 200
open_files_limit = 65535
binlog_cache_size = 1M
join_buffer_size = 8M
sort_buffer_size = 2M
read_buffer_size = 8M
read_rnd_buffer_size = 8M
table_definition_cache = 2000
table_open_cache_instances = 8
table_open_cache = 2000

# slow log
slow_query_log = 1
log_slow_admin_statements = 1
log_slow_slave_statements = 1
long_query_time  = 1

# semisync
rpl_semi_sync_master_enabled = 1 # master开启半同步
rpl_semi_sync_slave_enabled = 0 # slave不开启半同步
rpl_semi_sync_master_wait_point  = AFTER_SYNC # 5.7开始为默认值，开启无损复制，所谓的增强版同步复制
rpl_semi_sync_master_wait_for_slave_count = 1 # master提交后需要的ACK回复的数量
rpl_semi_sync_master_wait_no_slave = 0 # 默认为1。master发现 rpl_semi_sync_master_clients 小于 rpl_semi_sync_master_wait_for_slave_count，则master立即转为异步模式
rpl_semi_sync_master_timeout = 10000 # 默认10s master等待slave的ack回复的超时的时间。

# performance-schema 性能测试不建议开，出现问题后，如需定位，可以开启后辅助定位分析
performance-schema-instrument ='wait/lock/metadata/sql/mdl=ON'
performance-schema-instrument = 'memory/% = COUNTED'
performance-schema-instrument = 'stage/innodb/alter%=ON'
performance-schema-consumer-events-stages-current=ON
performance-schema-consumer-events-stages-history=ON
performance-schema-consumer-events-stages-history-long=ON
```
