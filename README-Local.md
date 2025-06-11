
* [搬运一下关于近期使用ruoyi-vue-pro的一些资料分享](https://linux.do/t/topic/112441/21?page=2)
* [商城模块](https://blog.csdn.net/qq_41146650/article/details/138678506)
* [ERP](https://blog.csdn.net/qq_41146650/article/details/138681481)

```sql
ALTER TABLE `trade_order` 
ADD COLUMN `give_coupon_template_counts` json DEFAULT NULL COMMENT '赠送的优惠券模板数量';

ALTER TABLE `trade_order` 
ADD COLUMN `give_coupon_ids` TEXT COMMENT '赠送的优惠劵编号';

ALTER TABLE `trade_order` 
ADD COLUMN `point_activity_id` BIGINT COMMENT '积分商城活动的编号';

ALTER TABLE `trade_delivery_pick_up_store` 
ADD COLUMN `verify_user_ids` BIGINT COMMENT '核销员工用户编号';

ALTER TABLE `promotion_coupon_template`
ADD COLUMN `description` TEXT COMMENT '优惠券说明';

```

```sql
CREATE TABLE `jimu_report_export_job` (
  `id` varchar(32) CHARACTER SET utf8mb4 COLLATE utf8mb4_unicode_ci NOT NULL COMMENT '主键',
  `name` varchar(100) CHARACTER SET utf8mb4 COLLATE utf8mb4_unicode_ci DEFAULT NULL COMMENT '任务名称',
  `begin_time` datetime DEFAULT NULL COMMENT '开始时间',
  `end_time` datetime DEFAULT NULL COMMENT '结束时间',
  `exec_interval` varchar(100) CHARACTER SET utf8mb4 COLLATE utf8mb4_unicode_ci DEFAULT NULL COMMENT '执行频率',
  `report_conf` text CHARACTER SET utf8mb4 COLLATE utf8mb4_unicode_ci COMMENT '导出报表配置',
  `last_run_time` datetime DEFAULT NULL COMMENT '最后执行时间',
  `receiver_email` text CHARACTER SET utf8mb4 COLLATE utf8mb4_unicode_ci COMMENT '接收通知的邮件',
  `file_sync_path` varchar(255) CHARACTER SET utf8mb4 COLLATE utf8mb4_unicode_ci DEFAULT NULL COMMENT '文件同步路径',
  `status` int DEFAULT NULL COMMENT '状态(0:停止;1:启动)',
  `create_by` varchar(50) CHARACTER SET utf8mb3 COLLATE utf8mb3_general_ci DEFAULT NULL COMMENT '创建人',
  `create_time` datetime DEFAULT NULL COMMENT '创建时间',
  `update_by` varchar(50) CHARACTER SET utf8mb3 COLLATE utf8mb3_general_ci DEFAULT NULL COMMENT '修改人',
  `update_time` datetime DEFAULT NULL COMMENT '修改时间',
  `tenant_id` varchar(10) CHARACTER SET utf8mb3 COLLATE utf8mb3_general_ci DEFAULT NULL COMMENT '多租户标识',
  PRIMARY KEY (`id`) USING BTREE
) ENGINE=InnoDB DEFAULT CHARSET=utf8mb4 COLLATE=utf8mb4_unicode_ci ROW_FORMAT=DYNAMIC COMMENT='积木报表导出计划表';
```

```sql
CREATE TABLE `jimu_report_category`  (
  `id` varchar(32) CHARACTER SET utf8mb4 COLLATE utf8mb4_general_ci NOT NULL COMMENT '主键',
  `name` varchar(100) CHARACTER SET utf8mb4 COLLATE utf8mb4_general_ci NOT NULL COMMENT '分类名称',
  `parent_id` varchar(32) CHARACTER SET utf8mb4 COLLATE utf8mb4_general_ci NULL DEFAULT NULL COMMENT '父级id',
  `iz_leaf` int(1) NULL DEFAULT NULL COMMENT '是否为叶子节点(0 否 1是)',
  `source_type` varchar(10) CHARACTER SET utf8mb4 COLLATE utf8mb4_general_ci NULL DEFAULT NULL COMMENT '来源类型( report 积木报表 screen 大屏  drag 仪表盘)',
  `del_flag` int(1) NULL DEFAULT NULL COMMENT '删除标识(0 正常 1 已删除)',
  `create_by` varchar(32) CHARACTER SET utf8 COLLATE utf8_general_ci NULL DEFAULT NULL COMMENT '创建人',
  `create_time` timestamp NULL DEFAULT NULL COMMENT '创建时间',
  `update_by` varchar(32) CHARACTER SET utf8 COLLATE utf8_general_ci NULL DEFAULT NULL COMMENT '更新人',
  `update_time` timestamp NULL DEFAULT NULL COMMENT '更新时间',
  `tenant_id` varchar(11) CHARACTER SET utf8mb4 COLLATE utf8mb4_general_ci NULL DEFAULT NULL COMMENT '租户id',
  PRIMARY KEY (`id`) USING BTREE
) ENGINE = InnoDB CHARACTER SET = utf8mb4 COLLATE = utf8mb4_general_ci COMMENT = '分类' ROW_FORMAT = Dynamic;

INSERT INTO jimu_report_category (id, name, parent_id, iz_leaf, source_type, del_flag, create_by, create_time, update_by, update_time, tenant_id) VALUES ('984272091947253760', '数据报表', '0', 1, 'report', 0, 'admin', '2024-08-16 11:52:44', NULL, NULL, '1000');
INSERT INTO jimu_report_category (id, name, parent_id, iz_leaf, source_type, del_flag, create_by, create_time, update_by, update_time, tenant_id) VALUES ('984302961118724096', '图形报表', '0', 1, 'report', 0, 'admin', '2024-08-16 13:55:24', NULL, NULL, '1000');
INSERT INTO jimu_report_category (id, name, parent_id, iz_leaf, source_type, del_flag, create_by, create_time, update_by, update_time, tenant_id) VALUES ('984302991393210368', '打印设计', '0', 1, 'report', 0, 'admin', '2024-08-16 13:55:31', NULL, NULL, '1000');

ALTER TABLE jimu_report_category ADD COLUMN sort_no int NULL COMMENT '排序' AFTER tenant_id;

update jimu_report_category set sort_no = 0 where sort_no is null;
```