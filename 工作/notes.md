# 2024-6-20

```mysql
create table sqyy_msg_send_task  
(  
TASK_ID VARCHAR(36) PRIMARY KEY COMMENT '任务ID',  
TASK_NAME VARCHAR(200) COMMENT '任务名称',  
TASK_TYPE VARCHAR(200) COMMENT '任务类型',  
TASK_RULE JSON COMMENT '任务规则',  
STATUS INT(2) COMMENT '状态',  
SEND_TEMPLATE_ID VARCHAR(50) COMMENT '推送模板ID',  
SEND_TYPE INT(1) COMMENT '手动/自动',  
SEND_START_TIME DATETIME COMMENT '推送开始时间',  
PRIORITY INT COMMENT '优先级 数字越小优先级越高',  
CREATED_BY VARCHAR(6) COMMENT '创建人',  
CREATED_TIME DATETIME COMMENT '创建时间',  
MODIFIED_BY VARCHAR(6) COMMENT '修改人',  
MODIFIED_TIME DATETIME COMMENT '修改时间'  
) comment '短信发送任务表';  
  
create table sqyy_msg_send_list  
(  
LIST_ID VARCHAR(36) PRIMARY KEY COMMENT '发送记录ID',  
TASK_ID VARCHAR(36) COMMENT '任务ID',  
SUCCESS_RECORD INT COMMENT '成功数',  
FAIL_RECORD INT COMMENT '失败数',  
SEND_START_TIME DATETIME COMMENT '发送开始时间',  
SEND_END_TIME DATETIME COMMENT '发送结束时间',  
SEND_STATUS INT COMMENT '任务状态',  
CREATED_BY VARCHAR(6) COMMENT '创建人',  
CREATED_TIME DATETIME COMMENT '创建时间',  
MODIFIED_BY VARCHAR(6) COMMENT '修改人',  
MODIFIED_TIME DATETIME COMMENT '修改时间'  
) comment '短信发送任务记录';  
  
create table sqyy_msg_send_detail  
(  
RECORD_ID VARCHAR(36) PRIMARY KEY COMMENT '发送记录ID',  
LIST_ID VARCHAR(36) COMMENT '发送记录ID',  
CUSTOMER_UID VARCHAR(6) COMMENT '客户ID',  
SEND_STATUS INT(1) COMMENT '发送状态',  
SEND_CONTENT VARCHAR(2000) COMMENT '发送内容',  
SEND_TIME DATETIME COMMENT '发送时间',  
CREATED_BY VARCHAR(6) COMMENT '创建人',  
CREATED_TIME DATETIME COMMENT '创建时间',  
MODIFIED_BY VARCHAR(6) COMMENT '修改人',  
MODIFIED_TIME DATETIME COMMENT '修改时间'  
) comment '短信发送任务详情'

```
# 2024-03-07

### 相似基金规则表
```mysql
create table fund_db_similar_rule(  
	LIST_ID VARCHAR(36) PRIMARY KEY COMMENT '主键',  
	MANAGER INT(1) COMMENT '1勾选,0未勾选',  
	CATEGORY INT(1) COMMENT '1勾选,0未勾选',  
	RISK INT(1) COMMENT '1勾选,0未勾选',  
	LABE INT(1) COMMENT '1勾选,0未勾选',  
	LABEL_NUM INT COMMENT '可以填写整数',  
	MODIFIED_BY VARCHAR(6) COMMENT '修改人',  
	MODIFIED_TIME DATETIME COMMENT '修改时间'  
)comment '相似基金规则表';
```

### 推荐基金表
```mysql
drop table fund_db_recommended;  
create table fund_db_recommended  
(  
	LIST_ID VARCHAR(36) PRIMARY KEY COMMENT '主键ID',  
	FUND_CODE VARCHAR(36) COMMENT '基金代码',  
	DESCRIPTION VARCHAR(3600) COMMENT '产品定位',  
	HIGHLIGHT VARCHAR(3600) COMMENT '亮点',  
	R_STATUS INT(1) COMMENT '状态（1 启用/0 停用）',  
	R_ORDER INT COMMENT '排序',  
	CREATED_BY VARCHAR(6) COMMENT '创建人',  
	CREATED_TIME DATETIME COMMENT '创建时间',  
	MODIFIED_BY VARCHAR(6) COMMENT '修改人',  
	MODIFIED_TIME DATETIME COMMENT '修改时间' ,  
	IS_DELETED INT(1) COMMENT '伪删除标识'  
) comment '推荐基金表';

```

### 推广点维护表
```mysql
create table fund_promotion(  
	LIST_ID VARCHAR(36) PRIMARY KEY COMMENT '主键ID',  
	NAME VARCHAR(200) COMMENT '推广点名称',  
	TYPE VARCHAR(2000) COMMENT '推广点类型(持仓收益率/基金经理观点)',  
	CONTENTS VARCHAR(4000) COMMENT '推广点内容',  
	RULE_INDICATOR VARCHAR(200) COMMENT '推广点规则指标',  
	RULE_OPERATOR VARCHAR(50) COMMENT '推广点规则运算符',  
	RULE_CONTENTS VARCHAR(200) COMMENT '推广点规则内容',  
	TIPS VARCHAR(4000) COMMENT '推广点话术',  
	CREATED_BY VARCHAR(6) COMMENT '创建人',  
	CREATED_TIME DATETIME COMMENT '创建时间',  
	MODIFIED_BY VARCHAR(6) COMMENT '修改人',  
	MODIFIED_TIME DATETIME COMMENT '修改时间' ,  
	IS_DELETED INT DEFAULT 0 COMMENT '是否删除 1 已删除 0 未删除'  
)comment '推广点维护表'
```

# 2024-03-06

### 修改customer存储体 


```mysql
-- 将主键修改为 CUSTOMER_UID
delte from zo_storable_define where sd_key = 'customer';
INSERT INTO zo.zo_storable_define (SD_ID, SD_KEY, TABLE_NAME, PRIMARY_KEY, PRIMARY_KEY2, CREATED_BY_FIELD, CREATED_TIME_FIELD, MODIFIED_BY_FIELD, MODIFIED_TIME_FIELD, SD_PERMISSION, CREATED_BY, CREATED_TIME, MODIFIED_BY, MODIFIED_TIME) VALUES ('70a17706-d5dd-402f-b1d9-e2bc77dca3ae', 'customer', 'customer', 'CUSTOMER_UID', '', '', '', '', '', 14, 'YUONG1', '2023-10-10 16:26:21', 'JYT8N7', '2024-03-06 10:42:36');

```

### staff表patch
```mysql
alter table staff add QUIT_TIME datetime comment '离职时间' after WORK_STATUS;  
alter table staff add QUIT_REMARK varchar(1000) comment '离职备注' after QUIT_TIME;  
alter table staff_his add QUIT_TIME datetime comment '离职时间' after WORK_STATUS;  
alter table staff_his add QUIT_REMARK varchar(1000) comment '离职备注' after QUIT_TIME;
```

