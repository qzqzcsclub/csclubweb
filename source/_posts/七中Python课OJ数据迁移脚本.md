### 使用说明

- 如果报错缺少requests库，请使用命令行：

```
pip install requests
```

或者

```
py -m pip install requests
```

- 首先输入原账号信息，而后可选择提交程序是否和获取原账号程序一起进行。以最近一次通过的程序为准。
- 代码文件均会保存。
- 输入验证码若图片加载失败请尝试重新打开。

### 代码如下

```py
import os
import time
import hashlib

import requests
import re
import html

from getpass import getpass

logger = open("./log.html", "w")
logger.write("&lt;table border=\"1\"&gt;")
domain = 'http://py.ssoier.cn:7077/'

def fetch_data(cookie, proid=1001, savefile=True):
    s = requests.get(
        domain + "status.php?showname=" + cookie['username']
        + "&amp;showpid=" + str(proid) + "&amp;showres=Accepted",
        cookies=cookie)
    match = re.search('ee=\"([\\w\\s`|#:,-]+)\"', s.text)
    if match:
        records = match.group(1).split("#")
        for record in records:
            if len(record) == 0:
                continue
            num = record.split("`")[1][1:]
            print("Fetched User '%s's id: %s" % (cookie['username'], num))
            s = requests.get(domain + "show_source.php?runid=" + num,
                             cookies=cookie)
            match = re.search('&lt;pre id=\'abc123\' class=\'(sh_cpp|sh_python)\'&gt;([\\w\\W]+)&lt;/pre&gt;', s.text)
            if match:
                ispy = match.group(1) == "sh_python"
                code = match.group(2)
                code = html.unescape(code)
                if savefile:
                    file = open("./ssoier/" + str(proid) + "." + ("py" if ispy else "cpp"), "w")
                    file.write(code)
                    file.close()
                return code, ispy
    return None, None


def submit_code(cookie, proid=1001, t=('', False), jump=True):
    if jump:
        code, _ = fetch_data(cookie, proid, False)
        if code:
            print("%s already accepted" % proid)
            return
    if t is None:
        t = '', False
    code, ispy = t
    if len(code) == 0:
        try:
            file = open("./ssoier/" + str(proid) + ".py", "r")
            ispy = True
        except IOError:
            try:
                file = open("./ssoier/" + str(proid) + ".cpp", "r")
            except IOError:
                return
        code = file.read()
    postdata = {
        'user_id': cookie['username'],
        'problem_id': proid,
        'language': 5 if ispy else 7,
        'source': code,
        'submit': '提交'
    }
    s = requests.post(domain + "action.php", data=postdata, cookies=cookie)
    requests.get(domain + "logout.php", cookies=cookie)
    match = re.search("statusx.php\\?runidx=(\\d+)", s.text)
    num = match.group(1)
    logger.write("&lt;tr&gt;&lt;td&gt;%s&lt;/td&gt;&lt;td&gt;%s&lt;/td&gt;&lt;td&gt;&lt;code&gt;%s&lt;/code&gt;&lt;/td&gt;" % (proid, num, code))
    print("Submitted Problem %s as ID = %s" % (proid, num))


def encode_pw(pw):
    md = hashlib.md5()
    md.update(pw.encode("utf-8"))
    pw = md.hexdigest()
    sha = hashlib.sha1()
    sha.update(pw.encode("utf-8"))
    return sha.hexdigest()


def login_request(title='|'):
    from_un = input(title + " Username: ")
    from_pw = getpass(title + " Password: ")
    cookie = {
        "username": from_un,
        "password": encode_pw(from_pw)
    }
    req = requests.get(domain + "ranklist.php", cookies=cookie)
    cookie['PHPSESSID'] = req.cookies.get_dict()['PHPSESSID']
    match = re.search("&lt;font color=red size=5&gt;&lt;b&gt;([\\w\\W]+)&lt;/b&gt;&lt;/font&gt;", req.text)
    if match and match.group(1).find("登录") &gt;= 0:
        print("Failed to login")
    else:
        print("Successfully logged in")
    return cookie, req.text


# Main
try:
    os.mkdir("ssoier")
except FileExistsError:
    print("Datapack already exist")
fetch_cookie, req_text = login_request("From")
offline = input("Fetch data first? (y/n) ").lower() == "y"
if offline:
    for prob in range(1001, 1109):
        fetch_data(fetch_cookie, prob)
to_cookie, req_text = login_request("To")
jump_ac = input("Skip accepted problem? (y/n) ").lower() == "y"
sleep_time = max(float(input("Sleeping time between each two submissions (second): ")), 0.5)
problem = input("Submit all(*) or a single problem: ")
if problem == "*":
    for prob in range(1001, 1109):
        if offline:
            submit_code(to_cookie, prob, jump=jump_ac)
        else:
            tut = fetch_data(fetch_cookie, prob)
            submit_code(to_cookie, prob, tut, jump_ac)
        time.sleep(sleep_time)
else:
    probs = map(int, problem.split())
    for prob in probs: 
      if offline:
          submit_code(to_cookie, int(prob), jump=jump_ac)
      else:
          tut = fetch_data(fetch_cookie, int(problem))
          submit_code(to_cookie, int(prob), tut, jump_ac)

```