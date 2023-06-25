# Face Detection via Intel & Raspberry Pi edge devices

TGIF project: Intel Neural Compute Stick 2 and Raspberry Pi detect faces. 

You can unmute this video to listen to sound or follow along with the slides and transcript below the video.

<video src="https://user-images.githubusercontent.com/38410965/111721442-44464700-8836-11eb-99f3-c6946d9d1c02.mp4" autoplay controls loop muted style="max-width: 730px;">
</video>

#

> Hi.  This is Steve Depp.  This is going to serve as my demo video 5 and my 50% update for my final project, all in one.  For my final project, I will be constructing a Donkey car, a robot car, and then having it read American Sign Language as it moves hopefully.  I’m not going to cover the set up of the Raspberry Pi in this video.  I have to say that it’s fairly easy.  I will touch upon things that were difficult.  
Here I am ssh’ing into the Raspberry Pi which is now headless.

### Steve Depp    
### 462-55 / DV5    

- [x] **Intel Neural Compute Stick 2 with Raspberry Pi  4**     
- [x] **50% update for final project: Donkey Car reads ASL**    

After setting up Raspberry Pi 4 with monitor, mouse and keyboard,  
ssh pi@192.168.1.135

<img width="572" alt="Last login Fri Hay 8 222619 on ttys003" src="https://user-images.githubusercontent.com/38410965/116009662-f79a1c80-a5e8-11eb-8cad-2b674583a6e8.png">

#

> So, the Raspberry Pi does have power problems.  Most people have an issue with the HDMI port on their monitor when they try and plug it into, you know, an old monitor or TV because most people don’t really have a monitor that they want to dedicate to, you know, a $39 computer.  
The Donkey car throttle and steering were working perfectly well, and then, all of a sudden, they stopped, and I think that may have been related to the power of the Raspberry Pi because I was unplugging it and plugging it in again and again. So, this code here allows you to, sort of, monitor what’s going on in the Raspberry Pi’s power.
Throttle has nothing to do with cars; so, just to let you know about that.   

**Raspberry Pi have power problems**    
- HDMI port on monitor    
- Donkey car throttle and steering died.    

<img width="567" alt="pi@raspberrypi" src="https://user-images.githubusercontent.com/38410965/116009668-01bc1b00-a5e9-11eb-9d92-b83a404fc2d3.png">

#

> So, Intel Neural Compute Stick 2.  I’m just going to call it “stick” from now on.  To use that, you would need to download “openvino”, the openvino toolkit.  So, you wget that and unpack it into a downloads file.  

**Intel Neural Compute Stick 2 —> open vino toolkit**    
wget and unpack    
https://download.01.org/opencv/2020/openvinotoolkit/2020.1/l_openvino_toolkit_runtime_raspbian_p_2020.1.023.tgz    

<img width="569" alt="vinotoolkit2020 1l_openvino_toolkit_runtime_raspbian_p_2020 1 023 tgz" src="https://user-images.githubusercontent.com/38410965/116009676-0b458300-a5e9-11eb-9abc-4dc6a2a7465d.png">

<img width="568" alt="optintelopenvino" src="https://user-images.githubusercontent.com/38410965/116009684-10a2cd80-a5e9-11eb-9bfe-b90652cdb6eb.png">

#

> These files are all on the Raspberry Pi.  
You install dependencies, which in this case is really just “cmake” since most of the files are in c+ or c++, err, c++ or c..  In fact all the files are in c++ in this example. 

**Install dependencies:**    
cmake to build in c or c++    

<img width="785" alt="ssh pi@192 168 1 135" src="https://user-images.githubusercontent.com/38410965/116009697-1c8e8f80-a5e9-11eb-8f94-d19500047b23.png">

#

> You set up an environment and its variables and make them permanent.  Now, in terms of permanent, you can totally wipe out the OS, reinstall it in 5 minutes. So, if you make any mistakes, it’s fairly inexpensive. 

**Setup an environment & variables**    

<img width="610" alt="raspberrypi- $ source optántelopenvinobinseti" src="https://user-images.githubusercontent.com/38410965/116009710-2617f780-a5e9-11eb-9be4-bbfb59e466ad.png">

And make them permanent until they’re not    

<img width="565" alt="Last login Sat May 014708 on ttys001" src="https://user-images.githubusercontent.com/38410965/116009723-2e703280-a5e9-11eb-91d0-aba4d4d8b34d.png">

#

> Alright. So, add the USB to the Raspberry, err, add rules so that Raspberry Pi can recognize the stick. That’s fairly easy.  Put the stick in.  And the kernel’s message buffer with the `dmesg` command will give you all the device drivers that are running on the Raspberry Pi, and here at the bottom, you can see there’s the Movidius stick. 
And here’s the Raspberry Pi and the stick there ontop of the Donkey car.  This is the back of the car.  This is the camera. 

**Add USB rules so Raspberry Pi recognizes the Stick**    
1.	Add current user “pi” to users group    

<img width="566" alt="pi@raspberrypi ~" src="https://user-images.githubusercontent.com/38410965/116009732-392ac780-a5e9-11eb-822c-61092e9ff763.png">

2. USB rules    

<img width="689" alt="pi@raspberrypi" src="https://user-images.githubusercontent.com/38410965/116009744-48117a00-a5e9-11eb-8277-759498ff78c4.png">

3. Put the stick in:    

<img width="412" alt="Pasted Graphic 14" src="https://user-images.githubusercontent.com/38410965/116009749-51024b80-a5e9-11eb-8cd6-c53e97adc292.png">

#

> OK. So, build and run a face detection model.  We’re going to make a build directory for the pre-trained model.  They call the model “samples” because these are Intel’s, you know, pre-trained models that they’re allowing you to look at.  Alright. 
This “CXX” is c++, and the Intel demo doesn’t have this “cpp” on the end, which caused about 4 or 5 hours of issues for me.  So, just remember that. And it’s not a c file.  It’s a c++ file. 
There you go.       

### Build / Run Face detection model    

**Make a build directory for the pre-trained model**    
Build the object detection sample     
- using cmake    
- calling that sample file    

(The code here is different from Intel’s demo:     
	samples/ can hold c, c++, and python.    
	This code specifies DCMAKE_CXX_FLAGS     
	for cpp and so folder you append “/cpp”.    
  
<img width="645" alt="stevedepp - pi@raspberrypi ~projectsbuild - ssh pi@192 168 1 135 - 91x58" src="https://user-images.githubusercontent.com/38410965/116009755-5a8bb380-a5e9-11eb-8d3e-948849e78ea4.png">

#

> You download one of the pre-trained face detection models.  There’s a bunch of models that come with, and they’re loaded onto your file directory.  The “bin” file has the weights, and the “xml” has the network topology.      

### Build / Run Face detection model (cont)    

**Download a pre-trained face detection model:**     
- [x] bin with weights    
- [x] xml with network topology  

<img width="627" alt="4521, 104 107 21 37" src="https://user-images.githubusercontent.com/38410965/116009768-6a0afc80-a5e9-11eb-9b3a-b40364cee974.png">

#

> Alright. So, you run one of the sample models which is the face detection model, and you give it the path for the image.  Now, in this case, this did not work, but here’s bringing an image over, or rather sending an image over from my MacBook to the Raspberry. 
Here’s the image.  It’s a woman in Bhutan.  I think she was drinking, err, eating some of the red beans.  She was quite drunk that day.   
But anyway, so, that didn’t work.   
So, I did some searching on Google and found this message, which basically just said backdate the models that you’re using because they’re not ready for prime time yet.  So, I went back to 2019.     

### Build / Run Face detection model (cont)    

**Run the sample with model and path to input image (this won’t work)**    
https://www.raspberrypi.org/documentation/remote-access/ssh/scp.md    

<img width="657" alt="Desktop" src="https://user-images.githubusercontent.com/38410965/116009787-75f6be80-a5e9-11eb-83d2-cd0d33b60673.png">

#

> So, using the new models.  

### Build / Run Face detection model (do over)    

**Download a pre-trained face detection model:**     
- [x] bin with weights    
- [x] xml with network topology    

<img width="680" alt="pi@raspberrypi ~projectsbuild" src="https://user-images.githubusercontent.com/38410965/116009797-8018bd00-a5e9-11eb-9072-c0d88a9d7277.png">

#

> And the model runs! 

### Build / Run Face detection model (do over)    

**A good sign!**  

<img width="529" alt="- pi@raspberrypi ~projectsbuild •" src="https://user-images.githubusercontent.com/38410965/116009808-89a22500-a5e9-11eb-8036-8e1f0bb01ed5.png">

#

> I bring the bitmap file over.  So, this is just how you do that.  You’re going and getting it from (to) the Raspberry Pi from the MacBook.
This is the bounding box. 

### Bring the bmp file over    
https://www.raspberrypi.org/documentation/remote-access/ssh/scp.md
￼
<img width="567" alt="Last login Sat May 9 123320 on tty001" src="https://user-images.githubusercontent.com/38410965/116009830-96bf1400-a5e9-11eb-87f0-fb7ff899addd.png">

And there she is ...   

<img width="424" alt="image" src="https://user-images.githubusercontent.com/38410965/116009846-b5bda600-a5e9-11eb-8825-32fd541da69d.png">

#

> Now, you can actually use the Raspberry Pi camera.  Those were all pictures that I had taken myself. You can use the Raspberry Pi camera for exactly the same methods.  The way you, when you’re headless, the way you set up the config is through these menu items.  So this is me setting up the camera.   
And then you take a photo with this, this command (`raspistill -o test shot.jpg`), and you bring it back over with this.
Later on, I go through a video, but it didn’t really work out. So, I’m not going to present that here. 

### Lets use the raspberry pi camera    
￼
<img width="572" alt="(env) pi@raspberrypi-projectsbuild $ sudo raspi-confioll" src="https://user-images.githubusercontent.com/38410965/116009857-c2da9500-a5e9-11eb-8a4a-f19105813fb9.png">

Interfacing options    

<img width="572" alt="Raspberry Pi 4 Model B Rev 1 2" src="https://user-images.githubusercontent.com/38410965/116009863-c837df80-a5e9-11eb-8047-bef4ac134ea7.png">

Camera on

<img width="567" alt="Raspberry Pi Software Configuration Tool (raspi-config)" src="https://user-images.githubusercontent.com/38410965/116009869-d0901a80-a5e9-11eb-8b38-aa77b854d7f9.png">

Lights, camera, ...

<img width="535" alt="(env) pi@raspberrypi-" src="https://user-images.githubusercontent.com/38410965/116009880-dab21900-a5e9-11eb-95ed-c4534f38ddbe.png">

<img width="539" alt="pi0192 168 1 135's password" src="https://user-images.githubusercontent.com/38410965/116009883-e00f6380-a5e9-11eb-8112-80e34a5dcb65.png">

... action

#

> So, here is the bounding box.  You can barely see the bounding box around my face, but it worked, and thank you very much. 

### Will this generate bonding boxes?    

<img width="568" alt="INFO InferenceEngine" src="https://user-images.githubusercontent.com/38410965/116009935-1fd64b00-a5ea-11eb-82c1-0884ed8ad5d5.png">

<img width="566" alt="(968,720)-(1175,1065) batch" src="https://user-images.githubusercontent.com/38410965/116009930-1baa2d80-a5ea-11eb-9575-f800a746bb22.png">

It does thank you for watching!

<img width="535" alt="image" src="https://user-images.githubusercontent.com/38410965/116009911-00d7b900-a5ea-11eb-86af-1f1efdd2bb28.png">

