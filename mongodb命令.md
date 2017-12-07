## 启动
mongo 10.46.24.145:27017

## 显示表
show dbs

## 使用表
use xxdb

## 显示所有的表
show collections

## 查找数据
db.member_platform_relations.find({"member_id" : "81"})

## 查找数据（单条）
db.member_platform_relations.find().limit(1)

## 移除数据
db.member_platform_relations.remove({"member_id" : "106"})

## 清表
db.member_platform_relations.drop()
