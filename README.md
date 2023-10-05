# Controller
Controller functions (how its programed)
package org.firstinspires.ftc.teamcode;

import com.qualcomm.robotcore.eventloop.opmode.LinearOpMode;
import com.qualcomm.robotcore.hardware.Servo;
import com.qualcomm.robotcore.eventloop.opmode.TeleOp;
import com.qualcomm.robotcore.hardware.DcMotor;
import com.qualcomm.robotcore.hardware.DcMotorSimple;

@TeleOp(name = "magic (Blocks to Java)")
public class magic extends LinearOpMode {
  
  
  
  private int rdirection = 1;
  private int ldirection = -1;
  private DcMotor rightfront;
  private DcMotor leftfront;
  private DcMotor leftback;
  private DcMotor rightback;
  private Servo arm;
  private double h = 1;
  private double g = 1;
  private boolean z;
  private Servo hand;
  private double k;
  private double x = 0.4;
  private double c = 0.65;

  /**
   * This function is executed when this OpMode is selected from the Driver Station.
   */
  @Override
  public void runOpMode() {
    rightfront = hardwareMap.get(DcMotor.class, "rightfront");
    leftfront = hardwareMap.get(DcMotor.class, "leftfront");
    leftback = hardwareMap.get(DcMotor.class, "leftback");
    rightback = hardwareMap.get(DcMotor.class, "rightback");
    arm = hardwareMap.get(Servo.class, "arm");
    hand = hardwareMap.get(Servo.class, "hand");

    // Reverse one of the drive motors.
    // You will have to determine which motor to reverse for your robot.
    // In this example, the right motor was reversed so that positive
    // applied power makes it move the robot in the forward direction.
    waitForStart();
    if (opModeIsActive()) {
      // Put run blocks here.
      while (opModeIsActive()) {
        // Put loop blocks here.
        // The Y axis of a joystick ranges from -1 in its topmost position
        // to +1 in its bottommost position. We negate this value so that
        // the topmost position corresponds to maximum forward power.
        
        if (gamepad2.right_trigger > 0){
          leftback.setPower(gamepad2.left_stick_y - gamepad2.left_stick_x);
          rightfront.setPower(gamepad2.left_stick_y - gamepad2.left_stick_x);
          leftfront.setPower(-gamepad2.left_stick_y - gamepad2.left_stick_x);
          rightback.setPower(-gamepad2.left_stick_y - gamepad2.left_stick_x);
          
        } else {
          if (gamepad2.left_trigger > 0){
            leftback.setPower((gamepad2.left_stick_y - gamepad2.left_stick_x)*x);
            rightfront.setPower((gamepad2.left_stick_y - gamepad2.left_stick_x)*x);
            leftfront.setPower((-gamepad2.left_stick_y - gamepad2.left_stick_x)*x);
            rightback.setPower((-gamepad2.left_stick_y - gamepad2.left_stick_x)*x);
          } else {
            leftback.setPower((gamepad2.left_stick_y - gamepad2.left_stick_x)*c);
            rightfront.setPower((gamepad2.left_stick_y - gamepad2.left_stick_x)*c);
            leftfront.setPower((-gamepad2.left_stick_y - gamepad2.left_stick_x)*c);
            rightback.setPower((-gamepad2.left_stick_y - gamepad2.left_stick_x)*c);
          }
        }
        
        leftfront.setPower(-gamepad2.right_stick_y);
        if (0.39 <= (h + (gamepad1.right_stick_y/1000)) && (h + (gamepad1.right_stick_y/1000)) <= 1){
          h = h + (gamepad1.right_stick_y/1000);
        }
        if (gamepad2.dpad_left){
          leftfront.setPower(g);
          leftback.setPower(-g);
          rightfront.setPower(g);
          rightback.setPower(-g);
        }
        if (gamepad2.dpad_right){
          leftfront.setPower(-g);
          leftback.setPower(g);
          rightfront.setPower(-g);
          rightback.setPower(g);
        }
        if (gamepad2.dpad_up){
          leftfront.setPower(g);
          leftback.setPower(-g);
          rightfront.setPower(-g);
          rightback.setPower(g);
        }
        if (gamepad2.dpad_down){
          leftfront.setPower(-g);
          leftback.setPower(g);
          rightfront.setPower(g);
          rightback.setPower(-g);
        }
        if (gamepad1.b){
          k = 1;
        }
        if (gamepad1.a){
          k = 0;
        }
        
        arm.setPosition(h);
        hand.setPosition(k);
      }
    }
  }
}


