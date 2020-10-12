## XSS

  XSS 通过修改 HTML 节点或者执行 JS 代码来攻击网站
  通过转义输入输出的内容来进行防御 ![dompurify](https://github.com/cure53/DOMPurify)
  通过 HTTP Header 中的 `Content-Security-Policy` 来开启 CSP 执行特定来源的代码

## CSRF
  - CSRF 就是利用用户的登录状态发起恶意请求
  - 防御
    1. Get 请求不对数据进行修改
    2. 不让第三方网站访问到用户 Cookie
    3. 阻止第三方网站请求接口
    4. 请求时附带验证信息，比如验证码或者 token
