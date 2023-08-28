# InnoDB 关键配置参数
InnoDB has a number of parameters that can control various functional aspects as well as performance. 

| **Parameter Name** | **Description** | **Default Value** | **Suggested Value** |
| --- | --- | --- | --- |
| [innodb\_checksum\_algorithm](https://dev.mysql.com/doc/refman/8.0/en/innodb-parameters.html#sysvar_innodb_checksum_algorithm "https://dev.mysql.com/doc/refman/8.0/en/innodb-parameters.html#sysvar_innodb_checksum_algorithm") | Tablespace page checksum algorithm. | crc32 | crc32 |
| [innodb\_doublewrite](https://dev.mysql.com/doc/refman/8.0/en/innodb-parameters.html#sysvar_innodb_doublewrite "https://dev.mysql.com/doc/refman/8.0/en/innodb-parameters.html#sysvar_innodb_doublewrite") | Write data to doublewrite buffer before writing to data file. | On | Data integrity - set to On <br> Performance - set Off |
| [innodb\_flush\_log\_at\_trx\_commit](https://dev.mysql.com/doc/refman/8.0/en/innodb-parameters.html#sysvar_innodb_flush_log_at_trx_commit "https://dev.mysql.com/doc/refman/8.0/en/innodb-parameters.html#sysvar_innodb_flush_log_at_trx_commit") | Controls log flushing and writing. | 1 | Data integrity - set to 1 <br> Performance - set to 2 |
| [innodb\_flush\_neighbors](https://dev.mysql.com/doc/refman/8.0/en/innodb-parameters.html#sysvar_innodb_flush_neighbors "https://dev.mysql.com/doc/refman/8.0/en/innodb-parameters.html#sysvar_innodb_flush_neighbors") | Same extent buffer pool and other dirty pages flushing. Extent is a group of pages within a tablespace. | 0 (zero) - disabled) | 0 (zero) - disabled |
| [innodb\_flush\_method](https://dev.mysql.com/doc/refman/8.0/en/innodb-parameters.html#sysvar_innodb_flush_method "https://dev.mysql.com/doc/refman/8.0/en/innodb-parameters.html#sysvar_innodb_flush_method") | Data (buffer pool) and log files (redo, undo) write to disk (flush) method; O\_DIRECT is used during flushing IO skipping fsync() after each write operation. <br> Windows will always use async\_unbuffered.  | fsync | Linux <br> ≤ 8.0.14 use O\_DIRECT (Always use with XFS Filesystem) <br> ≥ 8.0.13 use O\_DIRECT\_NO\_FSYNC |
| [innodb\_idle\_flush\_pct](https://dev.mysql.com/doc/refman/8.0/en/innodb-parameters.html#sysvar_innodb_idle_flush_pct "https://dev.mysql.com/doc/refman/8.0/en/innodb-parameters.html#sysvar_innodb_idle_flush_pct") | Buffer pool flushing during idle period as a percentage of innodb\_io\_capacity. Value of 100 does not limit page flushing when InnoDB is idle. | 100 | 100 |
| [innodb\_io\_capacity](https://dev.mysql.com/doc/refman/8.0/en/innodb-parameters.html#sysvar_innodb_io_capacity "https://dev.mysql.com/doc/refman/8.0/en/innodb-parameters.html#sysvar_innodb_io_capacity") | Number of available IOPS to background tasks (dirty page flushing, merging data from the change buffer) | 200 |  ≥ 1000 |
| [innodb\_io\_capacity\_max](https://dev.mysql.com/doc/refman/8.0/en/innodb-parameters.html#sysvar_innodb_io_capacity_max "https://dev.mysql.com/doc/refman/8.0/en/innodb-parameters.html#sysvar_innodb_io_capacity_max") | Number of maximum available IOPS to background tasks.  | 100 | ≥ 2000 |
| [innodb\_log\_compressed\_pages](https://dev.mysql.com/doc/refman/8.0/en/innodb-parameters.html#sysvar_innodb_log_compressed_pages "https://dev.mysql.com/doc/refman/8.0/en/innodb-parameters.html#sysvar_innodb_log_compressed_pages") | Redo log page compression (for table compression only). | On | Off |
| [innodb\_log\_file\_size](https://dev.mysql.com/doc/refman/8.0/en/innodb-parameters.html#sysvar_innodb_log_file_size "https://dev.mysql.com/doc/refman/8.0/en/innodb-parameters.html#sysvar_innodb_log_file_size") | Size of the log file. | 50 MB (503331648 bytes) | ≥ 1 GB 
| [innodb\_log\_files\_in\_group](https://dev.mysql.com/doc/refman/8.0/en/innodb-parameters.html#sysvar_innodb_log_files_in_group "https://dev.mysql.com/doc/refman/8.0/en/innodb-parameters.html#sysvar_innodb_log_files_in_group") | Number of log files in the log group. | 2 | ≥16 
| [innodb\_use\_native\_aio](https://dev.mysql.com/doc/refman/8.0/en/innodb-parameters.html#sysvar_innodb_use_native_aio "https://dev.mysql.com/doc/refman/8.0/en/innodb-parameters.html#sysvar_innodb_use_native_aio") | Use asynchronous I/O - Linux only. | On | On |
| [innodb\_data\_home\_dir](https://dev.mysql.com/doc/refman/8.0/en/innodb-parameters.html#sysvar_innodb_data_home_dir "https://dev.mysql.com/doc/refman/8.0/en/innodb-parameters.html#sysvar_innodb_data_home_dir") | The common part of the directory path for InnnoDB system tablespace files.  | The MySQL datadir.  | Only change this if using a separate layout for data, binary, and transaction log directories. |
| [innodb\_data\_file\_path](https://dev.mysql.com/doc/refman/8.0/en/innodb-parameters.html#sysvar_innodb_data_file_path "https://dev.mysql.com/doc/refman/8.0/en/innodb-parameters.html#sysvar_innodb_data_file_path") | Defines the attributes of the InnoDB system tablespace files.  | Create a single auto extending data file named ibdata1.  | Change this if using a separate layout for data, binary, and transaction log directories and/or setting a different innodb\_page\_size. |
| [innodb\_log\_group\_home\_dir](https://dev.mysql.com/doc/refman/8.0/en/innodb-parameters.html#sysvar_innodb_log_group_home_dir "https://dev.mysql.com/doc/refman/8.0/en/innodb-parameters.html#sysvar_innodb_log_group_home_dir") | The directory containing the InnoDB redo log files.  | Create two files name ib\_logfile0 and ib\_logfile1 in the datadir.  | Only change this if using a separate layout for data, binary, and transaction log directories. |
| [innodb\_undo\_directory](https://dev.mysql.com/doc/refman/8.0/en/innodb-parameters.html#sysvar_innodb_undo_directory "https://dev.mysql.com/doc/refman/8.0/en/innodb-parameters.html#sysvar_innodb_undo_directory") | The path where innodb creates undo tablespaces. | Undo table spaces are created in the datadir.  | Only change this if using a separate layout for data, binary and transaction log directories. |
| [innodb\_page\_size](https://dev.mysql.com/doc/refman/8.0/en/innodb-parameters.html#sysvar_innodb_page_size "https://dev.mysql.com/doc/refman/8.0/en/innodb-parameters.html#sysvar_innodb_page_size") | Specifies the page size for InnoDB tablespaces. Can only be specified prior to initializing the MySQL instance and cannot be changed afterward. <br> Affects the maximum row length.  | The default size is 16K.  | The recommendation is to leave this setting as default. <br> The performance profile (Less IOPS more Bandwidth) of storage I/O could change as the block size will increase with larger page sizes. |
| [innodb\_file\_per\_table](https://dev.mysql.com/doc/refman/8.0/en/innodb-parameters.html#sysvar_innodb_file_per_table "https://dev.mysql.com/doc/refman/8.0/en/innodb-parameters.html#sysvar_innodb_file_per_table") | If enabled tables are created on a file per table basis. When disabled tables are created in the system tablespace.  | ON | Recommend leaving this property ON if attempting to use a separate layout for data, binary and transaction log directories. |
| [innodb\_max\_dirty\_pages\_pct](https://dev.mysql.com/doc/refman/8.0/en/innodb-parameters.html#sysvar_innodb_max_dirty_pages_pct "https://dev.mysql.com/doc/refman/8.0/en/innodb-parameters.html#sysvar_innodb_max_dirty_pages_pct") | Establishes a target for flushing activity. Pages will be flushed from the buffer pool so that the total amount of dirty pages does not exceed this value.   | 90 | To flush more often make this value smaller.  |
| [innodb\_max\_dirty\_pages\_pct\_lwm](https://dev.mysql.com/doc/refman/8.0/en/innodb-parameters.html#sysvar_innodb_max_dirty_pages_pct_lwm "https://dev.mysql.com/doc/refman/8.0/en/innodb-parameters.html#sysvar_innodb_max_dirty_pages_pct_lwm") | A low watermark representing the percentage of dirty pages at which preflushing is enabled to control the dirty page ratio. | 10 | Always ensure this value is less than innodb\_max\_dirty\_pages\_pct.  |
| [innodb\_read\_io\_threads](https://dev.mysql.com/doc/refman/8.0/en/innodb-parameters.html#sysvar_innodb_read_io_threads "https://dev.mysql.com/doc/refman/8.0/en/innodb-parameters.html#sysvar_innodb_read_io_threads") | The number of I/O threads for read operations in InnoDB.  | 4 | If the MySQL server has enough cores increase this value to increase IO throughput.  |
| [innodb\_write\_io\_threads](https://dev.mysql.com/doc/refman/8.0/en/innodb-parameters.html#sysvar_innodb_write_io_threads "https://dev.mysql.com/doc/refman/8.0/en/innodb-parameters.html#sysvar_innodb_write_io_threads") | The number of I/O threads for write operations in InnoDB.  | 4 | If the MySQL server has enough cores increase this value to increase IO throughput.  |

> **innodb_log_file_size** and **innodb_log_files_in_group**
> 
> MySQL重做日志的大小和数量由`innodb_log_file_size`和`innodb_log_files_in_group`参数控制。重做日志的大小是`innodb_log_file_size`和`innodb_log_files_in_group`值的乘积，这些值应小于**512GB**。默认情况下，一个组中有两个**48GB**的重做日志文件，总共**96GB**。重做日志文件的大小可以和缓冲池一样大，不超过**512GB**。此外，配置大型重做日志文件可能会降低检查点频率。一般建议是有足够的重做日志空间可用来处理超过一个小时的写入活动。另一方面，配置大型日志文件将增加崩溃恢复时间。

# MySQL option file examples 
## Linux 
This option file will allow connections from any interface. Binary logs, transaction logs, undo files, and data files will be stored in separate locations. The innodb_page_size will be set to 16K and the 32Gb buffer pool will be divided into 16 separate instances. 

```
# For advice on how to change settings please see
# http://dev.mysql.com/doc/refman/8.0/en/server-configuration-defaults.html

[mysqld]
# Server Management
bind-address = 0.0.0.0
port = 3306
socket=/var/lib/mysql/mysql.sock
max_connections = 4000
log-error=/var/log/mysqld.log
pid-file=/var/run/mysqld/mysqld.pid
back_log = 1500
table_open_cache=8000
table_open_cache_instances=16
max_prepared_stmt_count=512000

# Data and log management
basedir = /mysql/base
datadir = /mysql/base/data
innodb_data_home_dir = /mysql/base/data
innodb_data_file_path  = ibdata1:12M:autoextend
innodb_log_group_home_dir = /mysql/log
innodb_undo_directory = /mysql/undo
log-bin = /mysql/binlog/binlog

# innodb settings
innodb_page_size = 16K
innodb_buffer_pool_size=32G
innodb_buffer_pool_instances=16
innodb_log_buffer_size=32M
innodb_file_per_table
innodb_log_file_size=1024M
innodb_log_files_in_group=32
innodb_open_files=4000
innodb_log_compressed_pages=off
innodb_doublewrite=ON
innodb_thread_concurrency=0
innodb_flush_log_at_trx_commit=1
innodb_max_dirty_pages_pct=90
innodb_max_dirty_pages_pct_lwm=10
innodb_use_native_aio=1
innodb_stats_persistent=1
innodb_spin_wait_delay=6
innodb_max_purge_lag_delay=300000
innodb_max_purge_lag=0
innodb_flush_method=O_DIRECT
innodb_checksum_algorithm=crc32
innodb_io_capacity=1000
innodb_io_capacity_max=3000
innodb_lru_scan_depth=9000
innodb_change_buffering=none
innodb_read_only=0
innodb_page_cleaners=4
innodb_undo_log_truncate=off
innodb_adaptive_flushing=1
innodb_flush_neighbors=0
innodb_read_io_threads=16
innodb_write_io_threads=16
innodb_purge_threads=4
innodb_adaptive_hash_index=0
innodb_monitor_enable='%'

# Error Message files
# lc_messages_dir = /mysql/lcmessages
# lc_messages = en_US

#other
binlog_expire_logs_seconds=300
```

## Microsoft Windows 
This option file will allow connections from any interface. Binary logs, transaction logs, undo files, and data files will be stored in separate locations. The innodb_page_size will be set to 16K and the 32Gb buffer pool will be divided into 16 separate instances. 

```
# Other default tuning values
# MySQL Server Instance Configuration File
# ----------------------------------------------------------------------
# Generated by the MySQL Server Instance Configuration Wizard
#
#
# Installation Instructions
# ----------------------------------------------------------------------
#
# On Linux you can copy this file to /etc/my.cnf to set global options,
# mysql-data-dir/my.cnf to set server-specific options
# (@localstatedir@ for this installation) or to
# ~/.my.cnf to set user-specific options.
#
# On Windows you should keep this file in the installation directory 
# of your server (e.g. C:\Program Files\MySQL\MySQL Server X.Y). To
# make sure the server reads the config file use the startup option 
# "--defaults-file". 
#
# To run the server from the command line, execute this in a 
# command line shell, e.g.
# mysqld --defaults-file="C:\Program Files\MySQL\MySQL Server X.Y\my.ini"
#
# To install the server as a Windows service manually, execute this in a 
# command line shell, e.g.
# mysqld --install MySQLXY --defaults-file="C:\Program Files\MySQL\MySQL Server X.Y\my.ini"
#
# And then execute this in a command line shell to start the server, e.g.
# net start MySQLXY
#
#
# Guidelines for editing this file
# ----------------------------------------------------------------------
#
# In this file, you can use all long options that the program supports.
# If you want to know the options a program supports, start the program
# with the "--help" option.
#
# More detailed information about the individual options can also be
# found in the manual.
#
# For advice on how to change settings please see
# https://dev.mysql.com/doc/refman/8.0/en/server-configuration-defaults.html
#
#
# CLIENT SECTION
# ----------------------------------------------------------------------
#
# The following options will be read by MySQL client applications.
# Note that only client applications shipped by MySQL are guaranteed
# to read this section. If you want your own MySQL client program to
# honor these values, you need to specify it as an option during the
# MySQL client library initialization.
#
[client]

# pipe=

# socket=MYSQL

port=3306

[mysql]
no-beep

# default-character-set=

# SERVER SECTION
# ----------------------------------------------------------------------
#
# The following options will be read by the MySQL Server. Make sure that
# you have installed the server correctly (see above) so it reads this 
# file.
#
# server_type=1
[mysqld]
# Data ,undo and log management
basedir = C:/MySQL/Base
datadir = C:/MySQL/Base/Data
innodb_data_home_dir = C:/MySQL/Base/Data
innodb_data_file_path  = ibdata1:12M:autoextend
innodb_log_group_home_dir = C:/MySQL/Log/Data
innodb_undo_directory = C:/MySQL/Undo/Data
log-bin = C:/MySQL/BinLog/Data
# innodb settings
innodb_buffer_pool_size=32G
innodb_buffer_pool_instances=16
innodb_log_buffer_size=32M
innodb_file_per_table
innodb_log_file_size=1024M
innodb_log_files_in_group=32
innodb_open_files=4000
innodb_log_compressed_pages=off
innodb_doublewrite=0
innodb_thread_concurrency=0
innodb_flush_log_at_trx_commit=1
innodb_max_dirty_pages_pct=90
innodb_max_dirty_pages_pct_lwm=10
innodb_stats_persistent=1
innodb_spin_wait_delay=6
innodb_max_purge_lag_delay=300000
innodb_max_purge_lag=0
innodb_checksum_algorithm=crc32
innodb_io_capacity=1000
innodb_io_capacity_max=3000
innodb_lru_scan_depth=9000
innodb_change_buffering=none
innodb_read_only=0
innodb_page_cleaners=4
innodb_undo_log_truncate=off
innodb_adaptive_flushing=1
innodb_flush_neighbors=0
innodb_read_io_threads=16
innodb_write_io_threads=16
innodb_purge_threads=4
innodb_adaptive_hash_index=0
innodb_monitor_enable='%'
# The next three options are mutually exclusive to SERVER_PORT below.
# skip-networking
# enable-named-pipe
# shared-memory

# shared-memory-base-name=MYSQL

# The Pipe the MySQL Server will use
# socket=MYSQL

# The TCP/IP Port the MySQL Server will listen on
port=3306

# Path to installation directory. All paths are usually resolved relative to this.
# basedir="C:/Program Files/MySQL/MySQL Server 8.0/"

# Path to the database root
# datadir=C:/ProgramData/MySQL/MySQL Server 8.0\Data
# datadir=C:/MySQL/Data_01/Data
# The default character set that will be used when a new schema or table is
# created and no character set is defined
# character-set-server=

# The default authentication plugin to be used when connecting to the server
default_authentication_plugin=caching_sha2_password

# The default storage engine that will be used when create new tables when
default-storage-engine=INNODB

# Set the SQL mode to strict
sql-mode="STRICT_TRANS_TABLES,NO_ENGINE_SUBSTITUTION"

# General and Slow logging.
log-output=FILE

general-log=0

general_log_file="MYSQL-WINDOWS.log"

slow-query-log=1

slow_query_log_file="MYSQL-WINDOWS-slow.log"

long_query_time=10

# Error Logging.
log-error="MYSQL-WINDOWS.err"

# ***** Group Replication Related *****
# Specifies the base name to use for binary log files. With binary logging
# enabled, the server logs all statements that change data to the binary
# log, which is used for backup and replication.
log-bin="MYSQL-WINDOWS-bin"

# ***** Group Replication Related *****
# Specifies the server ID. For servers that are used in a replication topology,
# you must specify a unique server ID for each replication server, in the
# range from 1 to 2^32 - 1. “Unique” means that each ID must be different
# from every other ID in use by any other source or replica.
server-id=1

# ***** Group Replication Related *****
# The host name or IP address of the replica to be reported to the source
# during replica registration. This value appears in the output of SHOW REPLICAS
# on the source server. Leave the value unset if you do not want the replica to
# register itself with the source.
# report_host=0.0

# NOTE: Modify this value after Server initialization won't take effect.
lower_case_table_names=1

# Secure File Priv.
secure-file-priv="C:/ProgramData/MySQL/MySQL Server 8.0/Uploads"

# The maximum amount of concurrent sessions the MySQL server will
# allow. One of these connections will be reserved for a user with
# SUPER privileges to allow the administrator to login even if the
# connection limit has been reached.
max_connections=151

# The number of open tables for all threads. Increasing this value
# increases the number of file descriptors that mysqld requires.
# Therefore you have to make sure to set the amount of open files
# allowed to at least 4096 in the variable "open-files-limit" in
# section [mysqld_safe]
table_open_cache=2000

# Maximum size for internal (in-memory) temporary tables. If a table
# grows larger than this value, it is automatically converted to disk
# based table This limitation is for a single table. There can be many
# of them.
tmp_table_size=9G

# How many threads we should keep in a cache for reuse. When a client
# disconnects, the client's threads are put in the cache if there aren't
# more than thread_cache_size threads from before.  This greatly reduces
# the amount of thread creations needed if you have a lot of new
# connections. (Normally this doesn't give a notable performance
# improvement if you have a good thread implementation.)
thread_cache_size=10

#*** MyISAM Specific options
# The maximum size of the temporary file MySQL is allowed to use while
# recreating the index (during REPAIR, ALTER TABLE or LOAD DATA INFILE.
# If the file-size would be bigger than this, the index will be created
# through the key cache (which is slower).
myisam_max_sort_file_size=100G

# The size of the buffer that is allocated when sorting MyISAM indexes
# during a REPAIR TABLE or when creating indexes with CREATE INDEX
# or ALTER TABLE.
myisam_sort_buffer_size=18G

# Size of the Key Buffer, used to cache index blocks for MyISAM tables.
# Do not set it larger than 30% of your available memory, as some memory
# is also required by the OS to cache rows. Even if you're not using
# MyISAM tables, you should still set it to 8-64M as it will also be
# used for internal temporary disk tables.
key_buffer_size=16M

# Size of the buffer used for doing full table scans of MyISAM tables.
# Allocated per thread, if a full scan is needed.
read_buffer_size=64K

read_rnd_buffer_size=256K

#*** INNODB Specific options ***
# innodb_data_home_dir=

# Use this option if you have a MySQL server with InnoDB support enabled
# but you do not plan to use it. This will save memory and disk space
# and speed up some things.
# skip-innodb

# If set to 1, InnoDB will flush (fsync) the transaction logs to the
# disk at each commit, which offers full ACID behavior. If you are
# willing to compromise this safety, and you are running small
# transactions, you may set this to 0 or 2 to reduce disk I/O to the
# logs. Value 0 means that the log is only written to the log file and
# the log file flushed to disk approximately once per second. Value 2
# means the log is written to the log file at each commit, but the log
# file is only flushed to disk approximately once per second.
innodb_flush_log_at_trx_commit=1

# The size of the buffer InnoDB uses for buffering log data. As soon as
# it is full, InnoDB will have to flush it to disk. As it is flushed
# once per second anyway, it does not make sense to have it very large
# (even with long transactions).
innodb_log_buffer_size=1M

# InnoDB, unlike MyISAM, uses a buffer pool to cache both indexes and
# row data. The bigger you set this the less disk I/O is needed to
# access data in tables. On a dedicated database server you may set this
# parameter up to 80% of the machine physical memory size. Do not set it
# too large, though, because competition of the physical memory may
# cause paging in the operating system.  Note that on 32bit systems you
# might be limited to 2-3.5G of user level memory per process, so do not
# set it too high.
innodb_buffer_pool_size=8M

# Size of each log file in a log group. You should set the combined size
# of log files to about 25%-100% of your buffer pool size to avoid
# unneeded buffer pool flush activity on log file overwrite. However,
# note that a larger logfile size will increase the time needed for the
# recovery process.
innodb_log_file_size=48M

# Number of threads allowed inside the InnoDB kernel. The optimal value
# depends highly on the application, hardware as well as the OS
# scheduler properties. A too high value may lead to thread thrashing.
innodb_thread_concurrency=33

# The increment size (in MB) for extending the size of an auto-extend InnoDB system tablespace file when it becomes full.
innodb_autoextend_increment=64

# The number of regions that the InnoDB buffer pool is divided into.
# For systems with buffer pools in the multi-gigabyte range, dividing the buffer pool into separate instances can improve concurrency,
# by reducing contention as different threads read and write to cached pages.
innodb_buffer_pool_instances=8

# Determines the number of threads that can enter InnoDB concurrently.
innodb_concurrency_tickets=5000

# Specifies how long in milliseconds (ms) a block inserted into the old sublist must stay there after its first access before
# it can be moved to the new sublist.
innodb_old_blocks_time=1000

# It specifies the maximum number of .ibd files that MySQL can keep open at one time. The minimum value is 10.
innodb_open_files=300

# When this variable is enabled, InnoDB updates statistics during metadata statements.
innodb_stats_on_metadata=0

# When innodb_file_per_table is enabled (the default in 5.6.6 and higher), InnoDB stores the data and indexes for each newly created table
# in a separate .ibd file, rather than in the system tablespace.
innodb_file_per_table=1

# Use the following list of values: 0 for crc32, 1 for strict_crc32, 2 for innodb, 3 for strict_innodb, 4 for none, 5 for strict_none.
innodb_checksum_algorithm=0

# The number of outstanding connection requests MySQL can have.
# This option is useful when the main MySQL thread gets many connection requests in a very short time.
# It then takes some time (although very little) for the main thread to check the connection and start a new thread.
# The back_log value indicates how many requests can be stacked during this short time before MySQL momentarily
# stops answering new requests.
# You need to increase this only if you expect a large number of connections in a short period of time.
back_log=80

# If this is set to a nonzero value, all tables are closed every flush_time seconds to free up resources and
# synchronize unflushed data to disk.
# This option is best used only on systems with minimal resources.
flush_time=0

# The minimum size of the buffer that is used for plain index scans, range index scans, and joins that do not use
# indexes and thus perform full table scans.
join_buffer_size=256K

# The maximum size of one packet or any generated or intermediate string, or any parameter sent by the
# mysql_stmt_send_long_data() C API function.
max_allowed_packet=4M

# If more than this many successive connection requests from a host are interrupted without a successful connection,
# the server blocks that host from performing further connections.
max_connect_errors=100

# Changes the number of file descriptors available to mysqld.
# You should try increasing the value of this option if mysqld gives you the error "Too many open files".
open_files_limit=4161

# If you see many sort_merge_passes per second in SHOW GLOBAL STATUS output, you can consider increasing the
# sort_buffer_size value to speed up ORDER BY or GROUP BY operations that cannot be improved with query optimization
# or improved indexing.
sort_buffer_size=256K

# The number of table definitions (from .frm files) that can be stored in the definition cache.
# If you use a large number of tables, you can create a large table definition cache to speed up opening of tables.
# The table definition cache takes less space and does not use file descriptors, unlike the normal table cache.
# The minimum and default values are both 400.
table_definition_cache=1400

# Specify the maximum size of a row-based binary log event, in bytes.
# Rows are grouped into events smaller than this size if possible. The value should be a multiple of 256.
binlog_row_event_max_size=8K

# If the value of this variable is greater than 0, a replica synchronizes its master.info file to disk.
# (using fdatasync()) after every sync_master_info events.
sync_master_info=10000

# If the value of this variable is greater than 0, the MySQL server synchronizes its relay log to disk.
# (using fdatasync()) after every sync_relay_log writes to the relay log.
sync_relay_log=10000

# If the value of this variable is greater than 0, a replica synchronizes its relay-log.info file to disk.
# (using fdatasync()) after every sync_relay_log_info transactions.
sync_relay_log_info=10000

# Load mysql plugins at start."plugin_x ; plugin_y".
# plugin_load

# The TCP/IP Port the MySQL Server X Protocol will listen on.
loose_mysqlx_port=33060
```

# 参考
[InnoDB Configuration Parameters](https://support.purestorage.com/Solutions/MySQL_and_MariaDB/MySQL_-_Getting_Started/InnoDB_Configuration_Parameters#InnoDB_Configuration_Parameters)
