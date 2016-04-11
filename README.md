### 一、环境安装 
    1、安装Python2.7和pip https://pypi.python.org/pypi/pip#downloads
    2、安装Library
    pip install robotframework  (VERSION = '2.9.1')
    pip install robotframework-httplibrary(VERSION = '0.4.2')
    pip install requests  (VERSION = '2.9.1')
    pip install robotframework-requests (VERSION = '0.3.8')
    pip install robotframework-databaselibrary
    pip install PyMySQL
    3、安装wxPython2.8-win32-unicode-2.8.12.1-py27.exe
    4、安装robotframework-ride-1.2.3.win32.exe
    5、引用库
    Library HttpLibrary.HTTP
    Library RequestsLibrary
    Library Collections
    Library DatabaseLibrary
    Library json

### 二、遇到的问题和解决方式
    1、测试报告乱码问题(Windows系统中存在，Linux中正常)
    修改C:\Python27\Lib\site-packages\robot\utils\encodingsniffer.py  
    修改前：
    DEFAULT_SYSTEM_ENCODING = 'cp125'
    DEFAULT_OUTPUT_ENCODING = 'cp437'
    修改后：
    DEFAULT_SYSTEM_ENCODING = 'cp936'
    DEFAULT_OUTPUT_ENCODING = 'cp936'
    2、HttpLibrary 发送http请求报错，ascii codec can't decode byte 0xe8 in position 0:ordinal not in range(128)
    修改HttpLibrary类库的init.py ，添加如下：
    import sys
    reload(sys)
    sys.setdefaultencoding('utf-8')
 
    3、解决 requestlibrary  tojson  中文无法正常显示的问题
        修改  添加参数 ensure_ascii=False,
         def _json_pretty_print(self, content):
            """ Pretty print a JSON object
            'content'  JSON object to pretty print
            """
            temp = json.loads(content)
            return json.dumps(
                temp,
                ensure_ascii=False,
                sort_keys=True,
                indent=4,
                separators=(',',': ')
            )