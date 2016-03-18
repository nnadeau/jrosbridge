jrosbridge [![Build Status](https://travis-ci.org/nnadeau/jrosbridge.svg?branch=jdk-1.6)](https://travis-ci.org/nnadeau/jrosbridge)
==========

#### A Native Java EE rosbridge Client

### Example Usage

```java
public static void main(String[] args) throws InterruptedException {
	Ros ros = new Ros("localhost");
	ros.connect();

	Topic echo = new Topic(ros, "/echo", "std_msgs/String");
	Message toSend = new Message("{\"data\": \"hello, world!\"}");
	echo.publish(toSend);

	Topic echoBack = new Topic(ros, "/echo_back", "std_msgs/String");
	echoBack.subscribe(new TopicCallback() {
		@Override
		public void handleMessage(Message message) {
			System.out.println("From ROS: " + message.toString());
		}
	});

	Service addTwoInts = new Service(ros, "/add_two_ints", "rospy_tutorials/AddTwoInts");

	ServiceRequest request = new ServiceRequest("{\"a\": 10, \"b\": 20}");
	ServiceResponse response = addTwoInts.callServiceAndWait(request);
	System.out.println(response.toString());
	
	ros.disconnect();
}
```

### License
jrosbridge is released with a BSD license. For full terms and conditions, see the [LICENSE](LICENSE) file.

### Authors
See the [AUTHORS](AUTHORS.md) file for a full list of contributors.
