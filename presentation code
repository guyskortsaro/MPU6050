import processing.serial.*;

Serial myPort;
String data = "";
float roll, pitch, yaw;

void setup() {
  size(800, 600, P3D);  // Set up the window size
  myPort = new Serial(this, "/dev/ttyUSB0", 9600);  // Open the serial port (adjust to your port)
  myPort.bufferUntil('\n');  // Wait for the end of line to process data
  frameRate(60);  // Set the frame rate to 60 for smoother updates
}

void draw() {
  background(0);  // Set background to black

  // Position and display the data
  translate(width / 2, height / 2, 0);  // Move the origin to the center

  // Display the roll, pitch, and yaw values as text
  textSize(24);
  fill(255);  // Set text color to white
  text("Roll: " + int(roll), -200, -250);
  text("Pitch: " + int(pitch), -200, -200);
  text("Yaw: " + int(yaw), -200, -150);

  // Apply the rotations to the 3D box based on roll, pitch, and yaw
  rotateX(radians(pitch));
  rotateY(radians(roll));
  rotateZ(radians(yaw));

  // Draw a shorter 3D box with green color
  fill(0, 255, 0);  // Set box color to green
  box(150, 80, 100);  // Draw a smaller and shorter box
}

// This function will be called when new serial data is available
void serialEvent(Serial myPort) {
  data = myPort.readStringUntil('\n');  // Read incoming data until newline
  if (data != null) {
    data = trim(data);  // Remove any leading or trailing whitespace

    // Split the incoming string into roll, pitch, and yaw values
    String[] items = split(data, '/');
    if (items.length == 3) {
      roll = float(items[0]);  // Convert the first part to float (roll)
      pitch = float(items[1]);  // Convert the second part to float (pitch)
      yaw = float(items[2]);  // Convert the third part to float (yaw)
    }
  }
}
