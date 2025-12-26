# SQL 备份

[toc]

## 挂jeff 账号

`update rtm.tbl_csm_user set delete_flag = 0, tenant_id =1191, role_id =( select inst_id from rtm.tbl_csm_rbac_role where tenant_id = 1191 and role_name = 'GlobalAdministrator') where email = 'jeffzhu.jianfengzhu@honeywell.com';`  	

## 关闭/开启 租户SSO

`update rtm.tbl_csm_config set config_value = '{"enable":false,"type":1}' where config_id = 1191 and  config_key = 'sso';`     

`update rtm.tbl_csm_config set config_value = '{"enable":true,"type":1}' where config_id = 1191 and  config_key = 'sso';`         

## 批量导入用户

```
# do $$
# <<first_block>>
# DECLARE
# u_id int8;
# BEGIN
# for i in 0..10000 loop
# select nextval('tbl_csm_user_user_id_seq'::regclass) into u_id;
# --first 3 col
# INSERT INTO rtm.tbl_csm_user
# ( role_id,tenant_id,email, user_id,  "password",   is_worker, status,   ws_session_id, is_ws_online , first_active_time, active_code, active_dead_line, start_time, end_time, first_name, create_time, create_by, last_login_time, app_salt, server_salt,  last_name, delete_flag,   data_private_agree_flag,   error_login_count,      need_sign_on, need_sign_on_dc)
# VALUES( '3267,3268', 1076,i||'@performancetest.com',u_id,'$2a$04$X9fIvsiSV4rVYaqa6ikp..EN4jgOUcS.0y.gwbOiQGyw4TyzsXkMS',    1, 1,   '0', 0,   '2024-04-10 05:30:09.807', '153ef1d8-481a-4f4d-a48a-0af7a5e40854', '2024-04-10 05:30:09.807', '2024-04-10 05:29:24.638', '2199-12-31 23:59:59.000', 'chen', '2024-04-10 05:29:24.638', -1, '2024-12-11 05:23:22.123', '$2a$04$dqEUp5olofnxfo3Tj0l/qu', '$2a$04$X9fIvsiSV4rVYaqa6ikp..',   'hui', 0,   '1111',   0,   1, 1 );
# --first 2 col
# INSERT INTO rtm.tbl_csm_worker
# ( tenant_id, user_name,inst_id,connect_id,   "password", app_salt, server_salt,    org_id,    svr_id,   is_online, online_time, offline_time,
#   private_key, public_key, created_time, start_time, end_time, delete_flag,  curr_dws_recv_time, zone_id,   user_alarm, has_alert, has_alarm, has_sensor_alert, has_sensor_alarm, first_name,   last_name,   proccess_node  ,apply_global)
# VALUES( 1076, i||'@performancetest.com',u_id,'WK_aaaa'||i||'-116c-42ce-b5e1-0096d69a0b2f', '$2a$04$X9fIvsiSV4rVYaqa6ikp..EN4jgOUcS.0y.gwbOiQGyw4TyzsXkMS', '$2a$04$dqEUp5olofnxfo3Tj0l/qu', '$2a$04$X9fIvsiSV4rVYaqa6ikp..',    -14292,   'toIot^0',  0, '2024-12-11 21:28:02.475', '2024-12-12 00:52:13.551',
#         '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', '2024-04-10 05:29:24.638', '1970-01-01 00:00:00.000', '2199-12-31 15:59:58.000', 0,  '2024-12-12 00:52:10.418', 2783,   0, 0, 0, 0, 0, 'chen',   'hui',   'toSaas',   1 );
# --first 2 col
# INSERT INTO rtm.tbl_csm_organization_user
# (  tenant_id,  organization_id,user_id, created_by, created_time, delete_flag, delete_time, update_time, updated_by)
# VALUES(  1076,  2427,u_id, -1, '2024-04-10 05:29:24.638', 0, '1970-01-01 00:00:00.000', '2024-04-10 05:29:24.638', -1);
# end loop;
# END first_block $$;
#
#
# --delete from rtm.tbl_csm_user where email like '%@performancetest.com';
# --delete from rtm.tbl_csm_worker where user_name like '%@performancetest.com';
```



## 统计BumpCal Results 数据



```
COPY (
    SELECT * FROM (
        select
            tp.product_name,
            dc.serial_no,
            dc.device_id,
            dc.tenant_id,
            dc.test_time,
            CASE (dc.test_info->>'detectorTestResult')::int
                WHEN -1 THEN 'Not Applicable (NA)'
                WHEN 0  THEN 'Success'
                WHEN 1  THEN 'Partial Success'
                WHEN 2  THEN 'Fail'
                WHEN 3  THEN 'Unknown'
                WHEN 4  THEN 'Not Tested'
                WHEN 5  THEN 'Null / Invalid'
                ELSE 'Invalid Code: ' || (dc.test_info->>'detectorTestResult')
            END AS testResultDesc,
            (
                SELECT STRING_AGG(
                    s->'sensorCommonInfo'->>'sensorName',
                    ', ' ORDER BY s->'sensorCommonInfo'->>'sensorName'
                )
                FROM json_array_elements(dc.test_info->'sensorTestResult') AS s
                WHERE LOWER(s->'sensorCommonInfo'->>'sensorName') NOT LIKE '%slot%'
            ) AS sensorNames,
            ROW_NUMBER() OVER (ORDER BY dc.device_id) as rn
        FROM rtm.tbl_device_certificate dc 
        LEFT JOIN rtm.tbl_product_sku tps ON tps.sku = dc.sku
        LEFT JOIN rtm.tbl_product tp ON tp.product_id = tps.product_id
        WHERE dc.type = 2
    ) sub
    WHERE rn > 500000
) TO STDOUT WITH (FORMAT CSV, HEADER TRUE, QUOTE '"', ESCAPE '"', ENCODING 'UTF8');
```

