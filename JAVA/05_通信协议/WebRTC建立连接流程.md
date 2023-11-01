背景：1.SDP会话描述协议
通过编辑SDP文本中的值，WebRTC被设计为可以调整提供或者应答，然后将其设置为本地或者远端描述

**RTCPeerConnection +** **信令:** **提供，应答和候选项**

RTCPeerConnection是WebRTC应用程序用来创建对等端连接并传输音视频的API。

初始化这个过程RTCPeerConnection有两个工作要做：
  1.确定本地媒体条件，如分辨率和编解码器功能。这是用于提供和应答机制的元数据。
 2. 获取应用程序主机的潜在网络地址，成为候选项
 一旦确定了本地数据，就必须通过信令机制与远端对等端进行交换。

让我们假设一个场景：Alice正在尝试呼叫Eve。下面是完整的提供/应答机制：

         1. Alice创建一个RTCPeerConnection对象。

         2. Alice使用RTCPeerConnection createOffer()方法产生一个提供（一个SDP会话描述）。

         3. Alice用他的提供调用setLocalDescription()。

         4. Alice将提供串联起来，并使用信令机制将其发送给Eve。

         5. Eve用Alice的提供调用setRemoteDescription()，以便她的RTCPeerConnection知道Alice的设置。

         6. Eve调用createAnswer()，以及success callback函数传入本地会话描述：Eve的应答。

         7. Eve通过调用setLocalDescription()将其应答设置为本地描述。

         8. Eve然后使用信令机制将她的字符串化的应答发回给Alice。

         9. Alice使用setRemoteDescription()将Eve的应答设置为远程会话描述。