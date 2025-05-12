
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