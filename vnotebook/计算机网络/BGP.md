路由重发布：在路由协议域的边界设备上，从路由信息从一个协议导入另一个协议
                       只有在路由表中的路由才能被重发布
BGP同步规则：BGP路由器不应使用通过IBGP对等体获得的路由或将其通告给EBGP对等体，除非该路由是本地的或者又通过IGP获得。
防止路由黑洞： 1 开启同步规则 
                        2 将BGP路由引入其他协议
                        3 所有的路由器都运行BGP，且两两建立对等体关系
                        4 MPLS
防环： 1 AS_PATH （只对EBGP有效， 因为在IBGP之间，AS_PATH不变）
           2 IBGP的水平分割：路由器不能把来自IBGP对等体的路由发给IBGP  (该规则要求IBGP全互联FULL MESH)
解决IBGP FULL MESH 消耗资源大的问题：
                  1 路由反射器(Route Reflector)
                  2 联邦(Confederation) 


BGP路由通告规则 ：
                 1 当到达同一目的地址存在多条路径时，BGP路由只会选择最优的使用(前提是未开启负载均衡)
                 2 BGP只把自己使用的，也就是最优的路由传递给对等体。
                 3 从EBGP学习来的路由，会向所有的对等体通告，包括EBGP,IBGP
                 4 从IBGP学习来的对等体不会通告给IBGP对等体(水平分割规则，存在路由反射器的情况除外)
                 5 从IBGP学习来的对等体是否会通告给EBGP对等要视IGP和BGP同步的情况来决定。
                 6 路由器只发送更新的路由


路由器把BGP路由通告给EBGP时，nexthop会变成自己的出接口地，如果通告给IBGP，默认情况下，nexthop不会变。可以在建立对等体关系时，指定next-hop-local，
这个通告给IBGP的时候，nexthop会变成自己的出接口。 (只有nexthop可达，路由才是valid。)

EBGP对等体关系一般都是直连的，默认是TTL是1(防止DDos攻击),如果EBGP没有直连，则需要修改默认TTL的直，使用
peer 1.1.1.1 ebgp-max-hop(IBGP没有这个限制)

refresh bgp all import : 


BGP属性： 
               1 公认必遵 ： 所有的BGP实现都必须能识别，且在update报文中必须携带  Origin/AS_Path/Nexthop
               2 公认自决 ： 所有的BGP实现都必须能识别，但不要求必须包含在Update中  Local_Prefernece/ATOMIC_Aggregate
               3 可选传递 ： 可以不支持该属性，但即使不支持也应该接受包含该属性的路由并传递给其他对等体 Community/Aggregate
               4 可选非传递 ：可以不支持该属性， 不识别该属性的BGP进程忽略包含这个属性的更新消息 MED/Originator_ID/Cluster_list/*pre_value

Prefered_Value: 入方向的路由的优先级， 只在本地有效，不能传递
Local_Prefernece： 出方向的路由优先级，只能在IBGP对待体间传递
Origin ：路由的起源 ，有三个值 ：优先顺序   I(IGP，通过network语句引入） > E（EGP） >？（ Incomplete 未知来源， import等)

AS_SET 的路由长度为1 
聚合路由可以继承原来路由的属性，


bgp 路由自动汇总功能 ，默认关闭， 开启：summary automatic 。 只对import-route命令注入的路由有效，且会按照主类网络进行汇总

bgp路由手动汇总： 1  创建静态路由      
                                   2  aggregate 
                      aggregate 默认不会抑制明细路由，加detail-suppressed抑制明细路由。明细路由的属性默认不会被继承，汇总的路由有自己的属性，as-set参数来让汇总的路由继承
             明细路由的属性
                     aggregate suppres-policy 以策略的方式来汇总路由 
                     aggregate  attribute-policy 来给汇总路由设置属性
                    aggregate origin-policy 来指定汇总路由“为谁而生”
