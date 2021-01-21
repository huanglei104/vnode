main->
       ngx_master_process_cycle->
              ngx_start_worker_processes->
                     ngx_spawn_process->
                            proc(ngx_worker_process_cycle)->(由子进程来执行)
                                ngx_worker_process_init(所有模块的初始化)->ngx_add_channel_event->ngx_add_conn(ngx_event_actions.add_conn)
                                ngx_process_events_and_timers->
                                        ngx_process_events(ngx_event_actions.process_events)->
                                                ngx_epoll_process_events->
                                                        epoll_wait->

ngx_event_actions是根据配置来确定的，对epoll来说， ngx_event_actions = ngx_epoll_module_ctx.actions;(src/event/modules/ngx_epoll_module.c:369)



ngx_spawn_process:创建子进程，父子进程间通过socketpair进行通信，也就是channel。channel也是由epoll来管理

如果模块有init_process，则会调用模块的该函数。ngx_event_core_module 模块，init_process = ngx_event_process_init，该函数中设置了rev->handler的值。


--prefix=/usr/local/ --conf-path=/etc/nginx/nginx.conf --with-http_ssl_module --with-pcre=../pcre-8.44 --with-zlib=../zlib-1.2.11 --with-stream --with-mail