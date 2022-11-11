---
link: null
title: github密码失效&hexo d失败 - whale3070's blog
description: news: GitHub防黑客新措施：弃用账密验证Git操作，改用token或SSH密钥，今晚0点执行
keywords: null
author: John Doe
date: 2021-08-15T15:43:00.000Z
publisher: InfoSec learning
stats: paragraph=15 sentences=19, words=82
---
news: [GitHub防黑客新措施：弃用账密验证Git操作，改用token或SSH密钥，今晚0点执行](https://www.thepaper.cn/newsDetail_forward_14042848)

8月14日，github的密码验证失效，后续都使用双因素认证。

于是我在github代码推送的时候遇到这个问题。

![](https://i.imgur.com/ATuSEtV.png)

```
123456789101112
```

```
remote: Support <span class="hljs-keyword">for</span> password authentication was removed on August <span class="hljs-number">13</span>, <span class="hljs-number">2021.</span> Please use a personal access token instead.<br>remote: Please see https:<br>fatal: unable <span class="hljs-keyword">to</span> access 'https:<br>FATAL {<br>  err: Error: Spawn failed<br>      at ChildProcess.<anonymous> (/home/kali/Documents/<span class="hljs-module-access"><span class="hljs-module"><span class="hljs-identifier">Whale3070</span>.</span></span>github.io/node_modules/hexo-util/lib/spawn.js:<span class="hljs-number">51</span>:<span class="hljs-number">21</span>)<br>      at <span class="hljs-module-access"><span class="hljs-module"><span class="hljs-identifier">ChildProcess</span>.</span></span>emit (events.js:<span class="hljs-number">314</span>:<span class="hljs-number">20</span>)<br>      at <span class="hljs-module-access"><span class="hljs-module"><span class="hljs-identifier">Process</span>.</span><span class="hljs-module"><span class="hljs-identifier">ChildProcess</span>.</span><span class="hljs-module"><span class="hljs-identifier">_handle</span>.</span></span>onexit (internal/child_process.js:<span class="hljs-number">276</span>:<span class="hljs-number">12</span>) {<br>    code: <span class="hljs-number">128</span><br>  }<br>} Something's wrong. Maybe you can find the solution here: %s https:<br><br></anonymous>
```

## 开启双因素认证

[https://docs.github.com/en/github/authenticating-to-github/securing-your-account-with-two-factor-authentication-2fa/configuring-two-factor-authentication](https://docs.github.com/en/github/authenticating-to-github/securing-your-account-with-two-factor-authentication-2fa/configuring-two-factor-authentication)

要下一个app，扫码获得一次性密码。
以后登录需要github密码+app上的六位数验证码

## 生成一个token

[https://docs.github.com/en/github/authenticating-to-github/keeping-your-account-and-data-secure/creating-a-personal-access-token](https://docs.github.com/en/github/authenticating-to-github/keeping-your-account-and-data-secure/creating-a-personal-access-token)
查看上文生成token以后，获得一串长度为40的字符串

在blog源码根目录下， `vi _config.yml`

```
123456
```

```
<br><br><span class="hljs-symbol">deploy:</span><br><span class="hljs-symbol">  type:</span> git<br><span class="hljs-symbol">  repo:</span> https:<br><span class="hljs-symbol">  branch:</span> main
```

即可正常hexo d更新blog
