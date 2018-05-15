Using a MessageHandler in MirrorMaker
======================================

This project contains a custom MessageHandler which gives a prefix to the source topic name. 

* Add the jar containing the handler to the class path. For example:

    `export CLASSPATH=$CLASSPATH:/Users/gwen/workspaces/kafka-examples/MirrorMakerHandler/target/TopicSwitchingHandler-1.0-SNAPSHOT.jar`

* Start MirrorMaker. Specify the Handler class in "--message.handler" and any arguments in "--message.handler.args". For example:

    `bin/kafka-mirror-maker.sh --consumer.config config/consumer.properties --message.handler com.shapira.examples.TopicSwitchingHandler --message.handler.args prefix- --producer.config config/producer.properties --whitelist mm1`

* As a prefix "prefix-" is given to com.shapira.examples.TopicSwitchingHandler, MirrorMake with TopicSwitchingHandler consumes from mm1 and produces to prefix-mm1. Test it with a producer on source topic and consumer on destination:

    `bin/kafka-console-producer.sh --topic mm1 --broker-list localhost:9092`
    
    `bin/kafka-console-consumer.sh --topic prefix-mm1 --zookeeper localhost:2181 --from-beginning`
