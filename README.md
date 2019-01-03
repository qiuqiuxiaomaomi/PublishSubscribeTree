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