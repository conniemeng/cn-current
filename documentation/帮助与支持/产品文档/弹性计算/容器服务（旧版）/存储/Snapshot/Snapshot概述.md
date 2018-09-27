# **Snapshot概述**

京东云支持为volume制作基于时间点的快照。快照功能是增量的， 也就是说，制作快照时，基于最近一次快照的增量数据才会被保存下来。 当快照被删除的时候，仅删除该快照保存的增量数据。

$ jcloud snapshot create --volume myvol --name new_snapshot
new_snapshot is created

快照仅在创建的地域下保留。可以基于现有的快照来创建新的volume。新的volume保留快照全部数据的副本，因此不能修改新Volume的大小。