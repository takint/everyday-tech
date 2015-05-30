Query disk IO in SQL Server:
SELECT * FROM sys.dm_io_virtual_file_stats(DB_ID('CentralDB'), NULL) AS IO_Stats
Parameter: NULL see all files.