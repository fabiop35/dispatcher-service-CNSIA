#Dispatcher Service CH10 from the Book Cloud Native Spring in Action.

Functionality for dispaching orders using Spring Cloud Function, RabbitMQ, Functions, Spring Cloud Stream.

#create project
curl https://start.spring.io/starter.zip -d groupId=com.cnsia -d artifactId=dispatcher-service-CNSIA -d name=dispatcher-service-CNSIA -d packageName=com.cnsia.dispatcherservice -d groupId=cnsia -d dependencies=cloud-function,devtools,actuator -d javaVersion=17 -d bootVersion=3.2.0 -d type=gradle-project -d descriotion="Functionality for dispatching orders" -o dispatcher-service-CNSIA.zip


#run containers: mq broker and mq console
docker run --privileged -d -p 15672:15672 -p 5672:5672 --name polar-rabbit -e RABBITMQ_DEFAULT_USER=user -e RABBITMQ_DEFAULT_PASS=password rabbitmq:3-management

#Rabbit admin console
http://localhost:15672


#RUN Alpine image
qemu-system-x86_64 -machine q35 -m 1024 -smp cpus=2 -cpu qemu64 \
  -drive if=pflash,format=raw,read-only,file=$PREFIX/share/qemu/edk2-x86_64-code.fd \
  -netdev user,id=n1,hostfwd=tcp::2222-:22,hostfwd=tcp::5672-:5672,hostfwd=tcp::15672-:15672 -device virtio-net,netdev=n1 \
  -nographic alpine/alpine.img


#TEST Function
gradle test --tests DispatchingFunctionsIntegrationTests

#ToDo: TESTS
gradle test --tests FunctionsStreamIntegrationTests


#RabbitMQ Objects
Input Exchange: order-accepted - Queue: order-accepted.dispacher-service
Output Exchange: order-dispatched - Queue: order-dispatche.order-service
