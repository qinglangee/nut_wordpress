# python exception 处理

## 基本使用

		
		import traceback
		import logging
		try:
            downloadCompanyInfo(comId)
        except Exception  as e:
            exstr = traceback.format_exc()
            # print exstr
            logging.error('comId:{} download error!'.format(comId))
            if('HTTP Error 403' in str(e)):


## 打开链接， 失败尝试重连
重试代码


    import logging
    import urllib2
    import urllib
    from bs4 import BeautifulSoup
    import sys
    import os
    import re
    import time
    import random
    import traceback
    import datetime
    
    def tryUrlOpen(request):
        tryCount = 0;
        while(tryCount < 10): # 连接失败时， 重试10次
            tryCount = tryCount + 1
            try:
                response = urllib2.urlopen(request)
                return response
            except Exception  as e:
                errMsg = str(e)
                # 连接失败时定时重试  Errno 10061
                if( "Errno 10061" in errMsg):
                    sleepMinutes = (tryCount - 5) * 30 if tryCount > 5 else tryCount * 3 
                    logging.error("try reconnect " + str(tryCount) + " sleep:" + str(sleepMinutes) + "minutes    Err:" + errMsg)
                    time.sleep(sleepMinutes * 60)
                else:
                    raise e
        raise  Exception("try reconnect times out!")