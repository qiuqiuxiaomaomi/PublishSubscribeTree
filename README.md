# PublishSubscribeTree
发布订阅技术研究


![](https://i.imgur.com/as6bUSc.png)

<pre>
Redis实现发布订阅

      1）发布
         jedis.publish("mychannel", line);
      2）订阅系统
         public class Subscriber extends JedisPubSub {
		    public Subscriber(){}

            //收到消息会调用
		    @Override
		    public void onMessage(String channel, String message) {       
		        System.out.println(String.format("receive redis published message, 
                                   channel %s, message %s", channel, message));
		    }
            //订阅了频道会调用
		    @Override
		    public void onSubscribe(String channel, int subscribedChannels) {    
		        System.out.println(String.format("subscribe redis channel success, 
                     channel %s, subscribedChannels %d",channel, subscribedChannels));
		    }
            //取消订阅 会调用
		    @Override
		    public void onUnsubscribe(String channel, int subscribedChannels) {   
		        System.out.println(String.format("unsubscribe redis channel, channel %s, 
                       subscribedChannels %d",channel, subscribedChannels));
		    }
		}
      3）订阅
        jedis.subscribe(subscriber, channel);

      发布者和订阅者都是Redis客户端，Channel则为Redis服务器端，发布者将消息发送到某个的频道，订阅了这
      个频道的订阅者就能接收到这条消息。Redis的这种发布订阅机制与基于主题的发布订阅类似，Channel相当于主题
</pre>

###订阅指定channel
![](https://i.imgur.com/mJhmP5N.png)
<pre>
      Redis 将所有接受和发送信息的任务交给 channel 来进行，而所有 channel 的信息就储存在
      redisServer 这个结构中.
</pre>


###订阅模式

![](https://i.imgur.com/6Oi9wZ9.png)

<pre>
      pubsub_channels 是一个字典，字典的键就是一个个 channel ，而字典的值则是一个链表，
      链表中保存了所有订阅这个 channel 的客户端
</pre>