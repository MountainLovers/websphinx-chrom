# WebSphinx chrome/opera addon

SPHINX: a password **S**tore that **P**erfectly **H**ides from **I**tself
(**N**o **X**aggeration)

SPHINX is a cryptographic password storage as described in
https://eprint.iacr.org/2015/1099

And as presented by the Levchin Prize winner 2018 Hugo Krawczyk on
Real World Crypto https://www.youtube.com/watch?v=px8hiyf81iM

## What is this thing?(这是什么？)

It allows you to have only a few (at least one) passwords that you
need to remember, while at the same time provides unique 40 (ASCII)
character long very random passwords (256 bit entropy). Your master
password is encrypted (blinded) and sent to the password storage
server which (without decrypting) combines your encrypted password
with a big random number and sends this (still encrypted) back to you,
where you can decrypt it (it's a kind of end-to-end encryption of
passwords) and use the resulting unique, strong and very random
password to register/login to various services. The resulting strong
passwords make offline password cracking attempts infeasible. If say
you use this with google and their password database is leaked your
password will still be safe.

它可以让你只拥有一些需要记忆的口令（至少一个），同时提供40不同ASCII码长的高熵口令(256比特)。你的主口令被加密并且发送至口令存出服务器，然后返回一个大随机数（加密过的）给你。你可以解密（一种端到端的口令加密）然后使用独一无二的，强的和随机的结果口令来注册/登录不同的服务。强结果口令可以使离线尝试攻击很困难。如果你用这项技术在Google注册，即使Google数据库泄露，你的口令也是安全的。

How is this different from my password storage which stores the
passwords in an encrypted database? Most importantly using an
encrypted database is not "end-to-end" encrypted. Your master password
is used to decrypt the database read out the password and send it back
to you. This means whoever has your database can try to crack your
master password on it, or can capture your master password while you
type or send it over the network. Then all your passwords are
compromised. If some attacker compromises your traditional password
store it's mostly game over for you. Using sphinx the attacker
controlling your password store learns nothing about your master nor
your individual passwords. Also even if your strong password leaks,
it's unique and cannot be used to login to other sites or services.

这与把我的口令存储在加密数据库中的存储方案有什么不同？最重要的是使用的加密方式不是端对端的加密。你的主口令可以被用来解密数据库然后读出所有的口令然后返回给你。这意味着无论是谁拥有你的数据库都可以尝试攻击你的主口令，或者在你通过网络传输的时候截取你的主口令。然后你的所有口令都被攻破。如果有些攻击者攻破了你的传统口令存储，那你就玩儿完了。使用SPHINX攻击者控制你的口令存储也无法得知任何你主口令或者使用的口令的相关信息。即使你的强口令泄露，这是独一无二的，也无法用于登录其他站点或服务。

## Usage（用法）

WebSphinx tries to automatically figure out what you want to do: login, create
a new account or change a password. It tries to figure this out by counting the
number of password input fields that are seen on the page. If this fails then
you can manually insert the password by clicking on the field where you want
the password inserted and on the WebSphinx popup click on **Insert Password**.

WebSphinx尝试着自动分别出你想干什么：登录、创建新账户或者修改密码。他尝试通过计算你在这个网页上的口令输入次数来分辨。如果它分辨失败，你可以手动插入口令通过点击你想插入口令的地方和WebSphinx弹窗上点击**Insert Password**。

If there is a text input field with a username already filled in, then it will
try to find a password for that user to login or change, or create a password
for this user if there is no such user yet associated with the current site by
the password storage. If there is no user to be found in a text field, then you
can enter the user in the WebSphinx popup, or you can select it from a list of
users that the password storage knows about.

如果有文本框已经填写了用户名，他接下来会为那些没有在这个网站上注册过的用户试着找一个口令来登录或者修改或者创建口令。如果文本域里没找到用户，你可以在WebSphinx弹窗里输入用户。或者你可以在已经存储了口令的用户列表里选择一个。

## Installation

WebSphinx is not in the Chrome Web Store, if you want to install it
follow these steps (this applies to all Operating Systems):

WebSphinx没有上线Chrome Web Store，如果你想要安装，请遵循以下步骤（适用于所有操作系统）：

 1. Create a directory on your filesystem containing the files in the
    websphinx directory. On windows if you used the winsphinx MSI
    installer this directory can be found under `c:\Program Files\Sphinx 1.0\websphinx`.
    
    在你的文件系统中建立一个文件夹，包含websphinx目录。在windows上如果你使用winsphinx MSI安装器，这个目录在`c:\Program Files\Sphinx 1.0\websphinx`.
    
 2. Start your browser if it is not running,

    如果没运行浏览器，打开浏览器。

 3. open [chrome://extension](chrome://extension) in your browser,

    打开 [chrome://extension](chrome://extension) 。

 4. enable `Developer Mode`,

    启用开发者模式。

 5. `Load Unpacked Extension` and provide the directory created in step 1.,

    加载未打包扩展然后选择步骤1中的目录。

 6. If all went well, you should get a yellowyish sphinx button.

    如果所有都完成了，你应该可以看到一个sphinx的按钮。

The WebSphinx extension requires the installation of a native
messaging host. If you are on Linux or MacOS you
need [pwdsphinx](https://github.com/stef/pwdsphinx), if you are on
Windows you need [winsphinx](https://github.com/stef/winsphinx).

WebSphinx需要安装一个原生信息宿主。如果你是Linux或MacOS用户，你需要安装[pwdsphinx](https://github.com/stef/pwdsphinx).如果你是windows用户，你需要 [winsphinx](https://github.com/stef/winsphinx).

The windows installer should take care of everything and you should be
done if you did the steps 1-5 above and succeeded at step 6. But if
you are on Linux/BSD/MacOS you need to change *%PATH%* in
*websphinx.json* so it refers to *websphinx.py* which came with
pwdsphinx.

windows安装器应该完成了前面步骤1-5并且成功在步骤6.如果你使用Linux/BSD/MaxOS你需要在websphinx.json改一下%PATH%来与websphinx.py对照。

### Native Messaging Host Manifest

Copy *websphinx.json*, depending on your browser to finish the installation:

- Linux/BSD
  - Per-user: `~/.config/{google-chrome,chromium}/NativeMessagingHosts/websphinx.json`
  - System: `/etc/{opt/chrome,chromium}/native-messaging-hosts/websphinx.json`
- MacOS
  - Per-user: `~/Library/Application Support/{Google/Chrome,Chromium}/NativeMessagingHosts/websphinx.json`
  - System-wide: `/Library/{Google/Chrome,Chromium}/NativeMessagingHosts/websphinx.json`

### Pinentry

You also need to install one of the X11 pinentry packages, choose according to your taste:
 - either `apt-get install pinentry-qt` (or anything equivalent on your OS)
 - or `apt-get install pinentry-gtk2`
 - or `apt-get install pinentry-gnome3`
 - or `apt-get install pinentry-fltk`

and set the pinentry variant if it is not invoked with
`/usr/bin/pinentry` in your sphinx config file in the `websphinx`
section.

## Credits

Icon made by Freepik from www.flaticon.com
