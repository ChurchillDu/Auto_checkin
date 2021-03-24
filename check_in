// ==UserScript==
// @name         机场自动签到
// @namespace    lhd
// @version      1.0.0
// @crontab * * once * *
// @author       lhd
// @grant GMSC_xmlhttpRequest
// @grant GM_notification
// @debug
// @supportURL   https://bbs.tampermonkey.net.cn/forum.php?mod=viewthread&tid=371
// @homepage     https://bbs.tampermonkey.net.cn/forum.php?mod=viewthread&tid=371
// ==/UserScript==
var username = ''
var password = ''
async function AutoSign() {
    GM_notification('我执行了');
    let xhr = await GMSC_xmlhttpRequest({
        url: "https://jinkela.red/user/logout",
        method: "GET",
        headers: {
            "Content-type": "application/x-www-form-urlencoded; charset=UTF-8",
        }
    })
    debugger;
    xhr = await GMSC_xmlhttpRequest({
        url: "https://jinkela.red/auth/login",
        method: "POST",
        data: 'email=' + encodeURIComponent(username) + '&passwd=' + encodeURIComponent(password) + '&code=',
        headers: {
            "Content-type": "application/x-www-form-urlencoded; charset=UTF-8",
        }
    }
    )
    if (xhr.responseText.indexOf('登出') != -1 || JSON.parse(xhr.responseText).msg == '登录成功') {
        xhr = await GMSC_xmlhttpRequest({
            url: "https://jinkela.red/user/checkin",
            method: "POST",
            data: '',
            headers: {
                "Content-type": "application/x-www-form-urlencoded; charset=UTF-8",
            }
        })
        var json = JSON.parse(xhr.responseText);
        if (json.msg == '您似乎已经签到过了...') {
            GM_notification('已经签到过了');
        } else if (json.msg.indexOf('获得') != -1) {
            GM_notification('签到成功');
        }
    }else if(xhr.responseText.indexOf('邮箱不存在') != -1)
    {
        GM_notification('邮箱不存在');
        
    }else{
        GM_notification('未知错误！'+xhr.responseText);
    }

}
AutoSign()








