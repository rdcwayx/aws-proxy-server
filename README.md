# 用亚马逊云服务（AWS）自动创建一台internet squid 代理服务器（EC2实例）

## 介绍
这个模板(template)可以让AWS客户创建任意区域的squid服务器(internet 代理）而不用登录到EC2服务器，也不执行任何命令，要做的仅仅是把模板推送到[AWS CloudFormation](http://aws.amazon.com/cloudformation/).

该项目给出实例说明使用AWS 云服务的Cloudformation 的便利性，但我觉得有些人会觉得这个模板在一些特殊环境里有用。一些在线服务限制源IP地址范围，但人们可以用这个模板通过快速启动在美国，爱尔兰，新加坡，澳大利亚，德国，南美洲和日本web代理，而不需要有很好的技术技能就能启用linux系统，然后自动安装并配置Squid来实现他们的目标。

##如何部署
0. 创建一个AWS账号，如果您还没有一个。您需要用国际信用卡申请一个AWS账户。
1. 将模板保存到您的PC / Mac （git clone https://git.oschina.net/rdcwayx/aws-proxy-server.git ）。
2. 登录到AWS管理控制台，选择区域 （region），再打开CloudFormation选项。
3. 选择“创建新栈 （create stack）”按钮。
4. 在“选择模板”：选择“*上传模板文件*”，并指向您保存在步骤1中template文件，
5. 接下来的页面中，“指定参数”要求的模板的具体信息。与EC2简单的代理，你需要指定你想使用的端口号和限制您的客户端IP地址。这个模板创建一个名为防火墙安全组来限制其他用户使用代理服务器。您可以检查[这里](http://whatismyipaddress.com/)得到你自己的IP地址。

    ***需要注意的是IP地址需要与子网掩码指定。换句话说，如果你要指定一个IP地址（“1.2.3.4”），那么你应该输入“1.2.3.4/32”***

    ***如果你允许来自任何IP地址，可以用“0.0.0.0/0”。但会被他人探测和使用，而产生意想不到的费用***
    
6. 单击继续两次，并完成向导。
7. 当该堆栈(stack)状态变为绿色（CREATE_COMPLETE），然后单击管理控制台的底部窗格中的输出（output）选项卡中找到代理服务器的IP地址 (比如 54.23.176.119)。
8. 配置你自己的Web浏览器使用代理 (比如 54.23.176.119:3128)。你可以开始享受了！

**在你不再需要你这个模板推出的代理服务器后，不要忘记“删除堆栈”，并确保其实例被终止（terminal）。**

**如果你不需要通过该代理服务器访问互联网，停止（stop）EC2实例，这将节省你的钱。您可以在以后启动，但会得到不同的IP地址。您需要调整您的浏览器的代理服务器的IP地址。**

请注意，对于新的用户，AWS给予12个月免费启动一个t1.micro或者t2.micro实例与EBS卷作为根设备。

## 对AWS 的cloudformation感兴趣，你想要了解更多？请访问以下站点：

*   [AWS CloudFormation - product site](http://aws.amazon.com/cloudformation/)
*   [Sample Templates](http://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/sample-templates-services-us-west-2.html)
*   [AWS CloudFormation Documentation](http://aws.amazon.com/documentation/cloudformation/)