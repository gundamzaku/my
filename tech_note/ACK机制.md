 ### RabbitMQ消息队列：ACK机制 

每个Consumer可能需要一段时间才能处理完收到的数据。如果在这个过程中，Consumer出错了，异常退出了，而数据还没有处理完成，那么 非常不幸，这段数据就丢失了。因为我们采用no-ack的方式进行确认，也就是说，每次Consumer接到数据后，而不管是否处理完 成，RabbitMQ Server会立即把这个Message标记为完成，然后从queue中删除了。

如果一个Consumer异常退出了，它处理的数据能够被另外的Consumer处理，这样数据在这种情况下就不会丢失了（注意是这种情况下）。

为了保证数据不被丢失，RabbitMQ支持消息确认机制，即acknowledgments。为了保证数据能被正确处理而不仅仅是被Consumer收到，那么我们不能采用no-ack。而应该是在处理完数据后发送ack。

在处理数据后发送的ack，就是告诉RabbitMQ数据已经被接收，处理完成，RabbitMQ可以去安全的删除它了。
