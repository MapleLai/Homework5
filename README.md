<h1> 飞碟游戏（物理版）</h1>

游戏介绍
-------------
飞碟从角飞出做平抛运动，一共有3种，分值由低到高为白、灰、黑，分值越高飞行速度越快。游戏一共有5轮，每轮射出10个飞碟，随着轮数的增加，3种飞碟所占的比例将会改变，当第5轮的10个飞碟全部击毁或飞出视界，游戏结束。

游戏界面
-------------
+ 开始界面
![开始](https://raw.githubusercontent.com/MapleLai/Homework5/master/Screenshot/%E5%BC%80%E5%A7%8B.png)
+ 过程界面
![过程](https://raw.githubusercontent.com/MapleLai/Homework5/master/Screenshot/%E8%BF%87%E7%A8%8B.png)
+ 结束界面
![结束](https://raw.githubusercontent.com/MapleLai/Homework5/master/Screenshot/%E7%BB%93%E6%9D%9F.png)

+ [演示视频](https://pan.baidu.com/s/1EHGLDmmj22nl1ppwc7saDg)

代码介绍
----------------
要使飞碟具有物理效果，需要在飞碟预制添加刚体。当然也可以在代码中动态生成，但有一点要注意的是不能在update函数里给gameObject添加刚体，虽然游戏能正常运行，但在运行的过程中会弹出“该gameObject已经添加了刚体”的重复警告。如果飞碟要完成平抛运动的话需要有一个竖直向下的恒力，刚体本身是有提供重力的，但由于这个力太大飞碟会下落的很快，所以我把刚体的重力勾选取掉，在代码里面动态添加一个竖直向下的力。  

+ 飞碟预制：    
![飞碟预制](https://raw.githubusercontent.com/MapleLai/Homework5/master/Screenshot/%E9%A3%9E%E7%A2%9F%E9%A2%84%E5%88%B6.png)  

利用Unity优秀的物理引擎可以帮我们达到的预想的物理效果，因为与运动学版的飞碟游戏在很多代码上都是差不多的，因此只介绍2个版本在飞碟飞行实现的不同之处。    
+ 运动学版：利用Translate函数使飞碟在每个deltaTime内按speed速度沿着direction方向飞行，这是一个直线运动。  
<pre>transform.Translate(gameobject.GetComponent<Disk>().direction * 
                    gameobject.GetComponent<Disk>().speed * 
                    Time.deltaTime);</pre>  
+ 物理版：
<pre>//给gameObject添加一个竖直向下的力
gameobject.GetComponent<Rigidbody>().AddForce(0,-80,0);
//在每个update里让飞碟都有一个水平向右的相同速度
gameobject.GetComponent<Rigidbody>().velocity = new Vector3(gameobject.GetComponent<Disk>().speed,0,0);</pre>  

以上就是两个版本飞碟游戏的不同实现，具体的可以参考Scripts文件里的代码，游戏的演示视频在上面有给出。
