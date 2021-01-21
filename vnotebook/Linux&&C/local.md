locale的catelog
/etc/locale.conf能配置的环境变量有：
LANG  这个变量的值会覆盖掉所有未设置的 LC_* 变量的值.
LANGUAGE  gettext会根据LANGUAGE选择使用的语言
LC_CTYPE
LC_NUMERIC
LC_TIME 时间和日期的格式
LC_COLLATE 这个变量的值决定排序和正则表达式的格式顺序.
LC_MONETARY
LC_MESSAGES
LC_PAPER
LC_NAME
LC_ADDRESS
LC_TELEPHONE
LC_MEASUREMENT
LC_IDENTIFICATION 
LANGUAGE: 。用户通过这个变量指定一个locale 列表。如果前面的 locale 缺少翻译，会自动使用后面的 locale 显示界面。比如：LANGUAGE="zh_CN:en_GB:en"

LC_ALL:这个变量的值会覆盖掉 LANG 和所有 LC_* 变量的值,无论它们是否设置.这意味着它只是为了测试和排除问题而设置.该变量不能在locale.conf 文件中设置 



glibc支持的所有的locale的定义都在/usr/share/i18n/locales目录下，通过反注释/etc/locale.gen文件中的行，并运行locale-gen就会在/usr/lib/locale生成locale-archive文件，该文件包含
了系统可用的locale,默认有c,posix。

函数setlocale
/usr/share/locale/locale/下是一各个应用程序的翻译文件。