LOAD DATA
APPEND
INTO TABLE test_raw
FIELDS TERMINATED BY ','
OPTIONALLY ENCLOSED BY '"'
(
        key_field
        num_of_values                           INTEGER EXTERNAL,
        ddl_data_varray         VARRAY COUNT(num_of_values)
        (
                ddl_data_varray                 CHAR(25)
        )
)


