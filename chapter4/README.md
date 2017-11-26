## 四、操作PG

### 4.1 pg_num和pgp_num

查看rbd pool中的 pg_num 和 pgp_num 属性

```
root@ceph0:/etc/ceph# ceph osd pool get rbd pg_num
pg_num: 64
root@ceph0:/etc/ceph# ceph osd pool get rbd pgp_num
pgp_num: 64
```

健康的 pg_num 和 pgp_num 计算方法：

​	关于pgmap的数目，**osd_num \*100 / replica_num**，**向上取2的幂**。比如15个osd，三备份，15 \*100/3=500，得到pg_num = 512，线上重新设定这个数值时会引起数据迁移，请谨慎处理。

设置

```
root@ceph0:/etc/ceph# ceph osd pool set rbd pg_num 512
set pool 0 pg_num to 512
root@ceph0:/etc/ceph# ceph osd pool set rbd pgp_num 512
set pool 0 pgp_num to 512
root@ceph0:/etc/ceph# 
```

### 4.2 查看集群PG信息

1、查看所有pg状态

```
ceph pg stat
```

2、查看pg组的映射信息，获取PG列表

```
ceph pg dump
```

3、查看指定 PG 的 Acting Set 或 Up Set 中包含的 OSD

```
ceph pg map {pg-num}
```

4、查看某一个pg详细信息

```
ceph pg {pool-num}.{pg-id} query
```

5、显示一个集群中所有pg统计

```
ceph pg dump --format plain
```

