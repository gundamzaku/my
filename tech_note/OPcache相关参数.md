配置指令的简短说明

    opcache.enable boolean 启用操作码缓存。如果禁用此选项，则不会优化和缓存代码
    opcache.enable_cli boolean 仅针对 CLI 版本的 PHP 启用操作码缓存
    opcache.memory_consumption integer OPcache 的共享内存大小，以兆字节为单位
    opcache.interned_strings_buffer integer 用来存储临时字符串的内存大小，以兆字节为单位
    opcache.max_accelerated_files integer OPcache 哈希表中可存储的脚本文件数量上限 设置值取值范围最小值是 200，最大值在 PHP 5.5.6 之前是 100000，PHP 5.5.6 及之后是 1000000。
    opcache.max_wasted_percentage integer 浪费内存的上限，以百分比计。 如果达到此上限，那么 OPcache 将产生重新启动续发事件。
    opcache.use_cwd boolean 如果启用，OPcache 将在哈希表的脚本键之后附加改脚本的工作目录， 以避免同名脚本冲突的问题。 禁用此选项可以提高性能，但是可能会导致应用崩溃。
    opcache.validate_timestamps boolean 如果启用，那么 OPcache 会每隔 opcache.revalidate_freq 设定的秒数 检查脚本是否更新。 如果禁用此选项，你必须使用 opcache_reset() 或者 opcache_invalidate() 函数来手动重置 OPcache，也可以 通过重启 Web 服务器来使文件系统更改生效。
    opcache.revalidate_freq integer 检查脚本时间戳是否有更新的周期，以秒为单位。 设置为 0 会导致针对每个请求， OPcache 都会检查脚本更新。如果 opcache.validate_timestamps 配置指令设置为禁用，那么此设置项将会被忽略。
    opcache.revalidate_path boolean 如果禁用此选项，在同一个 include_path 已存在的缓存文件会被重用
    opcache.save_comments boolean 如果禁用，脚本文件中的注释内容将不会被包含到操作码缓存文件， 这样可以有效减小优化后的文件体积，但会导致某些框架不可用
    opcache.load_comments boolean 如果禁用，则即使文件中包含注释，也不会加载这些注释内容。 本选项可以和 opcache.save_comments 一起使用，以实现按需加载注释内容。
    opcache.fast_shutdown boolean 如果启用，则会使用快速停止续发事件。
    opcache.enable_file_override boolean 如果启用，则在调用函数 file_exists()， is_file() 以及 is_readable() 的时候， 都会检查操作码缓存，无论文件是否已经被缓存。 如果应用中包含检查 PHP 脚本存在性和可读性的功能，这样可以提升性能。 但是如果禁用了 opcache.validate_timestamps 选项， 可能存在返回过时数据的风险。
    opcache.optimization_level integer 控制优化级别的二进制位掩码。
    opcache.inherited_hack boolean 在 PHP 5.3 之前的版本，OPcache 会存储代码中使用 DECLARE_CLASS 操作码 来实现继承的位置。当文件被加载之后，OPcache 会尝试使用当前环境来绑定被继承的类。 由于当前脚本中可能并不需要 DECLARE_CLASS 操作码，如果这样的脚本需要对应的操作码被定义时， 可能无法运行。 在 PHP 5.3 及后续版本中，此配置指令会被忽略。
    opcache.dups_fix boolean 仅作为针对 “不可重定义类”错误的一种解决方案。
    opcache.blacklist_filename string OPcache 黑名单文件位置。 黑名单文件为文本文件，包含了不进行预编译优化的文件名，每行一个文件名。 黑名单中的文件名可以使用通配符，也可以使用前缀。 此文件中以分号（;）开头的行将被视为注释。
    例如：

; 将特定文件加入到黑名单
/var/www/broken.php
; 以字符 x 文件打头的文件
/var/www/x
; 通配符匹配
/var/www/*-broken.php

    opcache.max_file_size integer 以字节为单位的缓存的文件大小上限。设置为 0 表示缓存全部文件。
    opcache.consistency_checks integer 如果是非 0 值，OPcache 将会每隔 N 次请求检查缓存校验和
    opcache.force_restart_timeout integer 如果缓存处于非激活状态，等待多少秒之后计划重启。 如果超出了设定时间，则 OPcache 模块将杀除持有缓存锁的进程， 并进行重启。
    opcache.error_log string OPcache 模块的错误日志文件。
    opcache.log_verbosity_level integer OPcache 模块的日志级别。
    opcache.preferred_memory_model string OPcache 首选的内存模块。可选值包括： mmap，shm, posix 以及 win32。
    opcache.protect_memory boolean 保护共享内存，以避免执行脚本时发生非预期的写入
    opcache.mmap_base string 在 Windows 平台上共享内存段的基地址。
    opcache.restrict_api string 仅允许路径是以指定字符串开始的 PHP 脚本调用 OPcache API 函数。
