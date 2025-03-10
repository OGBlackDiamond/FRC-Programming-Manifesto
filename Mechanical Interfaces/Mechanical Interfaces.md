Mechanical interfaces are the parts of the robot that directly interact with hardware to influence behavior. This includes motors, motor controllers, encoders, and the like. The key to an effective mechanism is good code. Usually this will extend beyond turning a motor on and off. You might want to develop some kind of feedback or feedforward loop that will allow you to better control that mechanism, or use motion profiling to be able to ease a mechanism in and out of setpoints. It all depends on the mechanism and the desired goal, but it is the programmer’s job to ensure that the mechanical aspect gets controlled to the best of its ability. 

Before you even touch the code, there are several key pieces of information that you need before you go implementing. The biggest ones are the kind of motor being used, the kind of motor controller being used, and any encoders or sensors that are used on the mechanism that you’re trying to control. It's also crucial to understand the behavior of the mechanism, and its physical limits. These parameters will all need to be defined when you’re configuring the subsystem for a mechanism.

## Implementation

Actually using this information is a bit different depending on what is actually being used on the robot, and there are a few options that I'll cover here. Generally, though, the Spark Max is the gold standard for motor controllers, so I'll try to focus on that here. 

Generally, you want to define your motor controller objects in a subsystem-by-subsystem basis. That is to say, all of the motor controllers should be defined in their respective classes. Until the robot is actually wired and ready to go, you won't know what 'port' each controller is using, so you'll have to use a dummy value.


```java
...
public class ExampleSubsystem extends SubsystemBase {

	private final SparkMax exampleMotor = new SparkMax(
		ExampleConstants.exampleMotorPort,
		SparkLowLevel.MotorType.kBrushless
	);

	...
}
```