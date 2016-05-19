本文件最后更新时间：2016年4月30日
------------------------------------------------------------------------------------
严重注意：如果这玩意调出来时，排版完全错乱，请复制emuera.config到era目录中覆盖原文件即可
或者修改emuera.config中的设定：
(**同时要注意CSV目录里的：_default.config也要修改)

ボタンの途中で行を折りかえさない:YES

------------------------------------------------------------------------------------
说明：文件功能：
SYSTEM_DEBUG_Universal.ERB 日文版的文件
SYSTEM_DEBUG_Universal_CHS.ERB 中文版的文件
SYSTEM_DEBUG_Universal_earH.ERB 针对eraH在修改时弹出错时使用的文件
SYSTEM_DEBUG_Universal_earmaouEX_CHS.ERB 针对earmaouEX 中文版防作弊系统的破解专用文件
SYSTEM_DEBUG_Universal_era_protoNTR.ERB 针对era紅魔館protoNTR。增加了“住人同士の交流”中
		“住人同士イベント”开启时的“好感度”修改
------------------------------------------------------------------------------------
这玩意，是以eraToho的SYSTEM_DEBUG.ERB为蓝本改的

v1.05 CHS_maouEX
针对eramaouEX 0.6正式汉化版的防改金钱做了一点手脚

v1.05 & v1.05 CHS
针对某些游戏的上限进行的调整
针对原素质修改里的BUG进行了修改

V1.04 CHS
所有的菜单及提示修改为简体中文。但游戏的内容是日文的依然会显示日文或者乱码，如果有乱码，请老实使用日文版。

v1.04
对于某些era游戏的MONEY取的是MONEY:1或者MONEY:2，所以将MONEY的修改同时列出MONEY:0 MONEY:1 MONEY:2，让大家自由修改
修改了emuera.config有可能造成字体不完整的问题，和其它奇怪提示的问题

v1.03
已经修改好了 CFLAG，BASE，MAXBASE等调用超界或者无法显示的问题
现在默认为有文字代码就显示文字，没有就显示代号标号
**已经测试 eraToho, eraTheWorld, eramaou, eramaou_CHT, eraSQN, eraSQN_JP, eraIm 通过

v1.02
对于eratoho系，是完全支持，而且没有任何问题的了
对于eraSQN或者会出现变量超界，或者列表无法显示等问题，我在继续想办法解决
------------------------------------------------------------------------------------
------------------------------------------------------------------------------------
使用方法：
首先，你得把这玩意丢到ERB目录中，理论上不会重名。

然后：这玩意的函数头是 @DEBUG_MENU_U
所以，你必须会改ERB文件的内容，想办法在SHOP或者其它能方便调用的地方加入对应的选择项


例：eraToho\ERB\システム_メイン画面 SHOP.ERB 第444行起：

ELSEIF RESULT == 833 && TALENT:MASTER:831 && FLAG:574 > 0 && TARGET >= 0 && BASE:0 < MAXBASE:0
	CALL YASAI_REVIVAL
ELSEIF RESULT == 998
	CALL DICTIONARY_MENU
ELSEIF RESULT == 999 && TALENT:MASTER:998
	PRINTW デバッグ菜單を呼び出します
	CALL DEBUG_MENU_SHOP
ELSE
	REUSELASTLINE  
ENDIF
RETURN 0

你可以在这里做点手脚，改成：

ELSEIF RESULT == 833 && TALENT:MASTER:831 && FLAG:574 > 0 && TARGET >= 0 && BASE:0 < MAXBASE:0
	CALL YASAI_REVIVAL
ELSEIF RESULT == 998
	CALL DICTIONARY_MENU
ELSEIF RESULT == 999 && TALENT:MASTER:998
	PRINTW デバッグ菜單を呼び出します
	CALL DEBUG_MENU_SHOP
ELSEIF RESULT == 88224646                            ；自己加的条件判定，在主调教界面菜单输入88224646
	CALL DEBUG_MENU_U                                ；就会调用这玩意出来了
ELSE
	REUSELASTLINE  
ENDIF
RETURN 0


至于你要怎么折腾，只要你懂代码，慢慢玩吧……
