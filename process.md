# 一、准备工作
1.在电脑上下载好飞书，并且注册好飞书的账号   [飞书：用于创建企业自建应用，接收机器人消息，调试API权限]  
<img width="1309" height="748" alt="image" src="https://github.com/user-attachments/assets/345ea1b9-b349-4cb7-ab70-e13c59547473" />
2.在电脑上下载MobaXterm，用来做SSH登录服务器  [远程SSH管理云服务器、上传项目代码、后台启动OpenClaw服务]  
<img width="927" height="570" alt="image" src="https://github.com/user-attachments/assets/7812d95b-eeb5-43f0-a09b-7f3954b79beb" />  
3.去到 阿里云 \ 腾讯云 购买Linux云服务器用于部署OpenClaw ，如下是我所购置的  
<img width="336" height="115" alt="image" src="https://github.com/user-attachments/assets/100d8019-051d-44e2-bc75-8a524a3cafd7" />    
（此外，还需要提前在阿里云平台先把服务器密码设置了）  
4.打开MobaXterm，并且点击新建会话，选择SSH连接，输入 服务器的ip地址 + 用户名，界面如下所示：  
<img width="894" height="703" alt="image" src="https://github.com/user-attachments/assets/438c077c-4bb7-4212-b0d1-6583c592791f" />  
5.后面进行输入刚刚设置的密码，然后再跳转到成功连接的状态，如下：
<img width="517" height="100" alt="image" src="https://github.com/user-attachments/assets/423845d7-2ba4-4619-a219-dbdbe23760cc" />  

# 二、实操
1.为了让文件更加整洁，先创建专属文件夹   
<img width="481" height="34" alt="image" src="https://github.com/user-attachments/assets/f23d6432-5ff2-4a02-a4b1-61e40a17834b" />   
2.安装Node.js24 （因为是Ubuntu官方脚本，它所提供的node js软件包内置捆绑了npm，所以下载node.js就会node.js 和 npm会一起下载）  
两条命令拉取 &nbsp;&nbsp;&nbsp;&nbsp;  命令一：curl -fsSL https://deb.nodesource.com/setup_24.x | bash -  &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; 命令二：apt-get install -y nodejs        
<img width="667" height="357" alt="image" src="https://github.com/user-attachments/assets/c4f247cc-6167-4171-ab02-cb6646441031" />     
<img width="661" height="305" alt="image" src="https://github.com/user-attachments/assets/a9e745dc-bfc5-4692-97d8-8429a7cef12f" />     
3.将npm全局缓存、全局安装包指定在专属的文件夹中（为了防止文件乱飘）     
两条指令 &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp ;指令1：npm config set cache /opt/openclaw-env/npm-cache &nbsp;&nbsp;&nbsp;&nbsp; &nbsp;&nbsp;&nbsp;&nbsp;指令2：npm config set prefix /opt/openclaw-env/npm-global  
<img width="657" height="65" alt="image" src="https://github.com/user-attachments/assets/b1b620ff-04b2-441b-a90d-b5cb9cd2451a" />    
4.把全局命令加入系统环境变量，否则等会终端会找不到openclaw命令  
两条指令 &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;指令1：echo "export PATH=/opt/openclaw-env/npm-global/bin:$PATH" >> /etc/profile &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; 指令2：source /etc/profile    
<img width="646" height="47" alt="image" src="https://github.com/user-attachments/assets/d11565d6-17cc-43c9-86cb-421738f92e96" />    
5.验证Node与npm安装
两条指令 &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;指令1：node -v &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; 指令2：npm -v  
<img width="451" height="61" alt="image" src="https://github.com/user-attachments/assets/d8c8a07c-abb9-4926-b379-51bc6e6ea8eb" />  
6.在专属目录内全局安装OpenClaw  
安装命令  npm install -g openclaw@latest  
<img width="1351" height="207" alt="image" src="https://github.com/user-attachments/assets/336d8df6-cc13-4f66-a1d9-8d38e019d2fc" />  
安装成功验证  openclaw --version  
<img width="541" height="30" alt="image" src="https://github.com/user-attachments/assets/f942f068-22f2-4a78-bbcd-9303adea4b67" />  
7.初始化OpenClaw，配置文件自动归类  
命令  openclaw onboard --install-daemon
<img width="816" height="717" alt="image" src="https://github.com/user-attachments/assets/e64d2bbe-7477-41f7-8321-b8499481b6a7" />  
8.初始化的是尽量都能跳过就跳过，等后面在可视化界面再设置也不迟    
<img width="665" height="624" alt="image" src="https://github.com/user-attachments/assets/3be99b34-60ac-41fd-9399-de941633b1db" />  
9.在MobaXterm新建一个本地会话，开SSH隧道转发，让自己可以在自己浏览器上查看到阿里云服务器打开的浏览器 (也可以在本地cmd中输入)
指令 ssh -N -L 18790:127.0.0.1:18789 root@你的公网IP 
并且会提示需要输入你的密码
<img width="743" height="151" alt="屏幕截图 2026-06-25 133920" src="https://github.com/user-attachments/assets/05525ef0-af8f-4b33-867c-d7023930ed84" />
10.随后在本机电脑的浏览器上搜索 http://localhost:18789/#token=ssh上显示的token（OpenClaw启动成功后会显示的）  
<img width="1350" height="1330" alt="image" src="https://github.com/user-attachments/assets/acfed2f3-45b0-41fe-9b89-0262f4732d7e" />

11.注意如何在下次重新登入呢？  
第一步：在MobaXterm登录阿里云服务器，进入服务器终端  
第二步：启动OpenClaw网关 &nbsp;&nbsp;&nbsp;&nbsp;指令:openclaw gateway start  (这一步启动之后，终端会打印带token的面板地址，复制token)  
第三步：在本地的CMD开SSH隧道输入：ssh -N -L 18789:127.0.0.1:18789 root@阿里云公网IP  
第四步：浏览器打开面板访问：http://localhost:18789/#token=你复制的token  

！！如果找不到token了，就输入指令：cat ~/.openclaw/openclaw.json 就会显示出来了。  

# 三、让OpenClaw连接飞书
1.在刚刚的MobaXterm里面下载飞书插件    
指令openclaw channels login --channel feishu  
<img width="708" height="183" alt="image" src="https://github.com/user-attachments/assets/ccf7f540-dc87-4dde-9fee-8213d884355b" />    
此时回到OpenClaw网页版的设置中频道就可以看到有飞书的状态和设置了   
<img width="1342" height="985" alt="image" src="https://github.com/user-attachments/assets/bb0e5be1-d587-4d45-80ca-3d454e27ca22" />  
2.现在去飞书开放平台，点开开发者后台，选择使用智能体模板创建，然后就获得了APP ID和APP Secret    
<img width="1348" height="578" alt="image" src="https://github.com/user-attachments/assets/6cf01e81-19bb-46fc-b8ae-5f97b1d492d8" />
3.现在回到MobaXterm里面，输入指令：openclaw channels login --channel feishu，并且把刚刚得到的APP ID和APP Secret配置好
<img width="744" height="572" alt="屏幕截图 2026-06-25 142518" src="https://github.com/user-attachments/assets/cbc30471-5064-44d1-ade0-4a132fccbd1b" />    
再次重启网关加载配置即可 （指令：openclaw gateway restart）如下所示   
<img width="1355" height="652" alt="image" src="https://github.com/user-attachments/assets/fcc7fd34-6b72-4255-bb3f-18572c728f2d" />    
4.现在去飞书创建一个群聊，并且把群聊id给到OpenClaw，也即是Actions中下面有ADD即可（这种是因为我在选择配置的是指定了机器人仅在我手动添加的指定群聊里回复）  
5.然后去飞书添加群机器人，选择刚刚我们所创建的智能助手  
<img width="1291" height="735" alt="image" src="https://github.com/user-attachments/assets/e31add88-5556-4de7-b0a4-a3402a51d868" />  

# 四、让Agent（机器人活起来） 
1.安装ollama本地部署，这样可以让OpenClaw用到本地大模型，从而让机器人回复，在命令行输入：curl -fsSL https://ollama.com/install.sh | sh  
<img width="675" height="63" alt="image" src="https://github.com/user-attachments/assets/6911054e-71a3-4be1-982e-d57adf8096b8" />    

but这里如果在Linux中下载太慢了，就可以在windows上先下载好，网址是：https://ollama.com/download/linux  

2.下载好Linux的安装包之后就把它放到我们的MobaXterm中去，并且应该要提前建立好文件夹，如下所示：   
<img width="211" height="176" alt="image" src="https://github.com/user-attachments/assets/8f5ecbd7-220a-469a-ac7a-8e31bdfb45e5" />  

3.传好之后，我们就进入到放置ollama的文件中去，并且进行解压  
两条指令&nbsp;&nbsp;&nbsp;&nbsp;：cd /opt/openclaw-env/ollama/&nbsp;&nbsp;&nbsp;&nbsp;tar -axvf ollama-linux-amd64.tar.zst&nbsp;&nbsp;&nbsp;&nbsp;如下所示：    
<img width="735" height="838" alt="image" src="https://github.com/user-attachments/assets/97f0e659-5590-4f9f-b0c4-e2da0a51f9f6" />  
4.创建软链接，让全局都可以用ollama命令：ln -s /opt/openclaw-env/ollama/bin/ollama /usr/local/bin/ollama，并且输入：ollama -v查看是否安装成功，如下所示：   
<img width="521" height="45" alt="image" src="https://github.com/user-attachments/assets/efb86088-1b72-478f-971d-815ff7f377fc" />  
5.现在启动ollama输入指令：ollama serve,并且新打开一个终端，原始终端也不能关，现在输入ollama list查看一下是否启动成功。如下所示：  
<img width="1014" height="300" alt="image" src="https://github.com/user-attachments/assets/ca09d658-d99f-4d33-89df-04e4e1fede5e" />  
<img width="465" height="45" alt="image" src="https://github.com/user-attachments/assets/4ced9f49-3455-4e56-bace-fe899d7a1849" />  
6.现在ollama本地部署成功了，但是其里面还没有大模型，所以我们拉取一个，输入指令：ollama pull qwen3:0.6b，如下所示：  
<img width="650" height="174" alt="image" src="https://github.com/user-attachments/assets/6b0eaab9-100a-4fcb-bcc1-5ff3cbf4bd29" />  
！！同时你也可以让模型下载到固定的地方，这样可以更好的方便管理，输入指令：export OLLAMA_MODELS=/opt/openclaw-env/ollama_model
7.现在就是回到OpenClaw，点开模型这里，然后配置好ollama的url这些配置，如图所示：  
<img width="1305" height="1275" alt="image" src="https://github.com/user-attachments/assets/25df9a93-94ea-4b1e-8d9b-eddab1505262" />    
9.现在重启网关，并且在对话栏进行与之对话，现在使用的就是ollama本地大模型了，如图所示，与之的对话：   
<img width="954" height="1012" alt="image" src="https://github.com/user-attachments/assets/9f8494cc-1b74-4d35-a12c-4798eb8ccb9c" />  
（也可以在网页直接与之对话，但是因为我的云服务器是2核4G的服务器，所以我就直接在SSH里面进行对话了，现在已经说明是联通了。）  
10.找到左侧菜单栏的“定时任务”然后点开并且填写内容如下所示：   
<img width="700" height="576" alt="image" src="https://github.com/user-attachments/assets/ec0dae2f-ca4c-444e-b233-8eee010e0515" />  
<img width="1014" height="325" alt="image" src="https://github.com/user-attachments/assets/4ff2ccb3-3682-4c67-a00f-b4c81e5ebea8" />  

# 五、另外的方法
1、在最开始下载open claw的时候就是使用命令：curl -fsSL https://openclaw.ai/install.sh | bash，结果如下所示：
<img width="747" height="1185" alt="屏幕截图 2026-06-28 112200" src="https://github.com/user-attachments/assets/2f74b490-382f-45cf-ad71-6074e19413fb" />  
2.随后的指导如下所示：（因为我是本地部署ollama所以就在这用的是ollama的本地部署模型）    
<img width="796" height="1178" alt="屏幕截图 2026-06-28 112231" src="https://github.com/user-attachments/assets/48aa6a37-0e58-4ab8-830f-903299213cb1" />   
3.接着在飞书开放平台上建立起飞书智能体  
<img width="1235" height="467" alt="image" src="https://github.com/user-attachments/assets/dc68f521-7a2a-4fd0-9e1f-001354ce5abd" />  
4.接着在飞书建立群聊，并且点击加入机器人，这个机器人得是你在飞书开放平台上建立的那个，如图所示：
<img width="820" height="548" alt="image" src="https://github.com/user-attachments/assets/e92fea57-8628-4d24-9e05-c9c06d202060" />   
例如上面这个“小智的助手”  
5.接着在MobaXterm中使用vim建立feishu_bot.py即可，指令：vim feishu_bot.py,如下所示（此时需要把你在飞书平台上创建的机器人的App ID和App Secret填写）
<img width="683" height="1234" alt="屏幕截图 2026-06-28 140902" src="https://github.com/user-attachments/assets/8881030e-b68d-44c5-a654-5258436efb4a" />  
<img width="898" height="951" alt="image" src="https://github.com/user-attachments/assets/4834f04d-6a75-473c-bc9e-577546c539b0" />
6.点击到飞书开放平台，点击【事件与回馈】中的事件配置，确保加入了如下这个事件：  
<img width="1104" height="153" alt="image" src="https://github.com/user-attachments/assets/0bf1a49b-9f8e-40cb-8358-5091cceeed6c" />  
7.接着在同页的时间配置方面，点击配置到将事件发送至开发者服务器，并且下面url输入：http://你的服务器公网地址:5000/feishu_callback
8.保存，并且处理好之后，即可输入命令：  
1).pkill -f python3  
2).nohup python3 feishu_bot.py > bot.log 2>&1 &  
3).tail -f bot.log  
9.然后就在飞书上进行和bot聊天，如下所示：
<img width="376" height="480" alt="image" src="https://github.com/user-attachments/assets/541abb2e-5c33-40bb-8d10-82f1203d940f" />  
至此就完成了openclaw部署本地ollama连接飞书了。
