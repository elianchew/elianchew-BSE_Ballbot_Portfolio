# Ball Tracking Robot
The ball tracking robot uses a Pi camera and an ultrasonic sensor to locate the ball. The robot uses motors to follow or intercept the ball while maintaining a set distance. The computer vision and the PID control make it complex and challenging

| **Engineer** | **School** | **Area of Interest** | **Grade** |
|:--:|:--:|:--:|:--:|
| Elian C | St. Joseph's Institution International  | Robotics and Computer Vision | Grade 9

**Replace the BlueStamp logo below with an image of yourself and your completed project. Follow the guide [here](https://tomcam.github.io/least-github-pages/adding-images-github-pages-site.html) if you need help.**

![Headstone Image](logo.svg)
  
# Final Milestone

**Don't forget to replace the text below with the embedding for your milestone video. Go to Youtube, click Share -> Embed, and copy and paste the code to replace what's below.**

<iframe width="560" height="315" src="https://www.youtube.com/embed/F7M7imOVGug" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" allowfullscreen></iframe>

For your final milestone, explain the outcome of your project. Key details to include are:
- What you've accomplished since your previous milestone
- What your biggest challenges and triumphs were at BSE
- A summary of key topics you learned about
- What you hope to learn in the future after everything you've learned at BSE



# Second Milestone

**Don't forget to replace the text below with the embedding for your milestone video. Go to Youtube, click Share -> Embed, and copy and paste the code to replace what's below.**

<iframe width="560" height="315" src="https://www.youtube.com/embed/y3VAmNlER5Y" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" allowfullscreen></iframe>

For your second milestone, explain what you've worked on since your previous milestone. You can highlight:
- Technical details of what you've accomplished and how they contribute to the final goal
- What has been surprising about the project so far
- Previous challenges you faced that you overcame
- What needs to be completed before your final milestone 

# First Milestone

**Don't forget to replace the text below with the embedding for your milestone video. Go to Youtube, click Share -> Embed, and copy and paste the code to replace what's below.**

<iframe width="560" height="315" src="https://www.youtube.com/embed/CaCazFBhYKs" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" allowfullscreen></iframe>

For your first milestone, describe what your project is and how you plan to build it. You can include:
- An explanation about the different components of your project and how they will all integrate together
- Technical progress you've made so far
- Challenges you're facing and solving in your future milestones
- What your plan is to complete your project

# Schematics 
Here's where you'll put images of your schematics. [Tinkercad](https://www.tinkercad.com/blog/official-guide-to-tinkercad-circuits) and [Fritzing](https://fritzing.org/learning/) are both great resoruces to create professional schematic diagrams, though BSE recommends Tinkercad becuase it can be done easily and for free in the browser. 

# Code
Here's where you'll put your code. The syntax below places it into a block of code. Follow the guide [here]([url](https://www.markdownguide.org/extended-syntax/)) to learn how to customize it to your project needs. 

```c++
void setup() {
  // put your setup code here, to run once:
  Serial.begin(9600);
  Serial.println("Hello World!");
}

void loop() {
  // put your main code here, to run repeatedly:

}
```

# Bill of Materials
Here's where you'll list the parts in your project. To add more rows, just copy and paste the example rows below.
Don't forget to place the link of where to buy each component inside the quotation marks in the corresponding row after href =. Follow the guide [here]([url](https://www.markdownguide.org/extended-syntax/)) to learn how to customize this to your project needs. 

| **Part** | **Note** | **Price** | **Link** |
|:--:|:--:|:--:|:--:|
| Screwdriver | Assembling the robot chassis | $20.27 | <a href="https://www.amazon.sg/dp/B0BBFJ2XKY?ref=ppx_yo2ov_dt_b_fed_asin_title"> Link </a> |
| H-Bridge Motor Drive | Controls the direction and speed of the DC Motors | $20.51 | <a href="https://www.amazon.sg/VKLSVAN-Channel-H-Bridge-Stepper-Controller/dp/B0DQPRDHSK/ref=sr_1_1?crid=Y8BXRSLRBPA2&dib=eyJ2IjoiMSJ9.N12Bqdf_2P8Sg-7hcxYlDFdt5Z4RdXTwKJO_O8gKZyxiHskn-fX8uaW0cgysQlNzSFdROvS8e3FcUe0l00L2-5dAW1d-Rlnw-cVgMJMF-gQlFt_OYgWtLGY7JOvS8YMSjqQ5XiUUDvqhGPtj-Z0rl4iCA0UL3GTLccxvOxph2dm8asICSbQS_waohnQv3jnLPt4Em2QdC7mOdPrb3AZmzTr8uudnXNQxHyM12Qb7HFkpzrYUDLJvCNcm4GpfMWZuPCzbj4U5sMbTd0MenIPGtimoEHj_3oT4jnWfwy3ha9I.yukHYovBVQjkpeKhMBX20XnFG99hJxHm1T11Qm8Gbb4&dib_tag=se&keywords=H-bridge&qid=1782927562&sprefix=h-bri%2Caps%2C278&sr=8-1&th=1"> Link </a> |
| Raspberry Pi 4 | Runs the Python code that processes the camera feed, calculates PID values, and sends GPIO signals to the H-Bridge to control the motors | $216.27 | <a href="https://www.amazon.sg/dp/B0C8LV6VNZ?ref=ppx_yo2ov_dt_b_fed_asin_title"> Link </a> |
| Multimeter | Checks the voltage of wires to prevent short circuit | $25.99 | <a href="https://www.amazon.sg/dp/B01ISAMUA6?ref=ppx_yo2ov_dt_b_fed_asin_title"> Link </a> |
| Ultrasonic Sensor | Measures the distance to the ball | $25.35 | <a href="https://www.amazon.sg/dp/B0CQCCGXCP?ref=ppx_yo2ov_dt_b_fed_asin_title"> Link </a> |
| Chassis Kit | Provides the physical framework to mount and support all components including wheels and the Raspberry Pi | $24.32 | <a href="https://www.amazon.sg/dp/B01LXY7CM3?ref=ppx_yo2ov_dt_b_fed_asin_title"> Link </a> |
| Pi Camera | Captures the live video feed, which the code then processes to detect the ball's colour and calculate its position relative to the centre of the frame | $24.45 | <a href="https://www.amazon.sg/dp/B07RWCGX5K?ref=ppx_yo2ov_dt_b_fed_asin_title&th=1"> Link </a> |
| Batteries | Provides power for the motors| $29.86 | <a href="https://www.amazon.sg/dp/B0035LCFNQ?ref=ppx_yo2ov_dt_b_fed_asin_title&th=1"> Link </a> |
| Motor Dual DC | Drives the wheels under the control of the H-Bridge | $19.80 | <a href="https://www.amazon.sg/dp/B09N6NXP4H?ref=ppx_yo2ov_dt_b_fed_asin_title"> Link </a> |
| Foam Ball | The target object that the robot tracks and intercepts | $12.95 | <a href="https://www.amazon.sg/dp/B000KYQ406?ref=ppx_yo2ov_dt_b_fed_asin_title"> Link </a> |
| Electronics Kit | Provides the breadboard and jumper wires to connect components such as the H-Bridge, ultrasonic sensors, and motors | $9.99 | <a href="https://www.amazon.com/dp/B01ERP6WL4?ref=ppx_yo2ov_dt_b_fed_asin_title"> Link </a> |

# Other Resources/Examples
One of the best parts about Github is that you can view how other people set up their own work. Here are some past BSE portfolios that are awesome examples. You can view how they set up their portfolio, and you can view their index.md files to understand how they implemented different portfolio components.
- [Example 1](https://trashytuber.github.io/YimingJiaBlueStamp/)
- [Example 2](https://sviatil0.github.io/Sviatoslav_BSE/)
- [Example 3](https://arneshkumar.github.io/arneshbluestamp/)

To watch the BSE tutorial on how to create a portfolio, click here.
